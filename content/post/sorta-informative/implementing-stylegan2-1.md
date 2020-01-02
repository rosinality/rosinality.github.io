---
title: "StyleGAN 2 바닥에서부터 구현하기"
date: 2019-12-28T23:41:55+09:00
draft: true
hasMath: true
---

Progressive GAN[^1], StyleGAN[^2], StyleGAN 2[^3]으로 이어지는 시리즈의 모델은 그 압도적인 샘플 퀄리티로 GAN의 발전에 중요한 영향을 미쳤다. 이번에 StyleGAN 2를 구현하면서 모델과 학습 루프의 구현 방식에 흥미로운 지점들이 꽤 있다는 생각을 했다. (커스텀 커널 구현, 분산 학습 환경, 그래디언트 패널티 등.) 이 모델을 뜯어보면서 사용한 트릭들과 그 트릭들이 등장한 연구들을 짚어보고 하나하나 구현해보면 GAN에 대해 훑어볼 수 있는 기회도 될 수 있을 것 같았고, 딥 러닝 모델의 구현 및 학습에 대해서 생각해볼 수 있는 것들이 많겠다 싶었다.

그래서 이제 그 작업을 시작해보려 한다.

## 왜 나는 걱정을 멈추고 GAN을 사랑하게 되었는가?

2014년에 등장한 GAN[^4]은 이제 가장 중요한 생성 모델 중 하나가 되었다. 물론 GAN이 이런 지위에까지 오른데에는 수많은 연구자들의 수많은 노고가 필요했다. 생성 모델들은 대체로 꼭 하나씩 문제가 있다:

1. Variational Autoencoder: 샘플 퀄리티가 만족스럽지 않다. Posterior Collapse.
2. Flow: 사용할 수 있는 모델에 제한이 있고 막대한 크기의 모델이 필요하다.
3. Autoregressive Model: 샘플링에 시간이 많이 걸리고 모델 크기도 작지 않다.
4. GAN: 트레이닝이 어렵고 Mode collapse가 발생하는 경향이 높다, 샘플의 확률을 구하는 작업을 하기 어렵다.

GAN은 높은 샘플 퀄리티를 보여줄 수 있는 포텐셜이 있지만 당장 학습시키는 것이 만만치 않았다. DCGAN이 막 나왔던 즈음에 GAN 트레이닝을 해봤던 사람들이라면 잘 알고 있을 것이다. 지금은 많이 나아졌지만 여전히 문제 없이 쉽게 된다고 말할 수 있는 정도는 아닌 것 같다. 이 문제를 해소하기 위해 정말 많은 연구들이 필요했다. DCGAN[^5], Improved Techinques[^6], WGAN[^7], WGAN-GP[^8], Hinge Loss[^9], TTUR[^10], R1 Penalty[^11], Spectral Normalization[^12], Projection Discriminator[^13], Self Attention[^14], BigGAN[^15]. 널리 쓰이는 트릭들만 꼽아도 그 수가 만만치 않다.

Progressive GAN[^1]은 이런 트릭과 도구들을 기반으로 Curriculum learning[^16]을 GAN 학습에 성공적으로 도입한 사례다. Curriculum learning은 문제의 난이도를 점진적으로 증가시키면서 모델을 학습시키는 방법이다. Progressive GAN에서는 점진적으로 이미지의 크기를 늘려가는 방식으로 GAN 학습에 Curriculum learning을 도입했다.

![Progressive GAN Curriculum Learning](https://res.cloudinary.com/rosinality/image/upload/v1577623784/stylegan2/pggan1.png)
Progressive GAN의 학습 과정

작은 크기의 이미지는 정보가 적고 단순하기 떄문에 학습이 안정적이니, 비교적 안정적인 학습 과정에서 문제의 난이도를 높여가면 한 번에 어려운 과제를 학습시키는 것보다 학습이 용이하다는 아이디어이다. 실제로 Progressive GAN은 안정적으로 높은 품질의 1024 × 1024 이미지 생성에 성공했다.

![Progressive GAN Training Fade-in](https://res.cloudinary.com/rosinality/image/upload/v1577623784/stylegan2/pggan2.png)

이미지의 크기를 점진적으로 높여가기 위해서 이전 크기의 이미지를 업샘플링/다운샘플링한 이미지와 그 업샘플링/다운샘플링된 이미지에 새로 추가된 컨볼루션 레이어를 적용한 이미지를 선형 결합하고, 점진적으로 추가된 컨볼루션의 비율을 높여가는 식으로 학습해나간다. 16 × 16 이미지에서 32 × 32 이미지로 넘어가는 과정을 생각해보면 이런 형태가 된다:

<div>
$$
y_{32 \times 32} = (1 - \alpha) \mathrm{Up}_{2 \times}( y_{16 \times 16} ) + \alpha \mathrm{Conv}(\mathrm{Up}_{2 \times}(y_{16 \times 16})), 0 \leq a \leq 1
$$
</div>

그리고 여기에 몇 가지 트릭들이 추가적으로 사용된다.

### Minibatch Standard Deviation

Minibatch Standrad Deviation은 Salimans et al.[^6]에서 제안된 방법이다. GAN 학습에 문제가 발생하면 generator가 생성하는 샘플의 다양성이 감소하거나 아예 한 점으로 축소되는 경우가 발생하는데(Mode collapse) 이러한 경향을 줄이기 위한 방법이다. 이를 줄이기 위해 discriminator가 미니 배치 내 샘플들을 독립적으로 보는 것이 아니라 샘플들을 결합한 정보를 활용할 수 있게 만드는 것이다.

Progressive GAN에서는 비교적 간단한 방법을 활용했다. 미니 배치의 특징Feature들에 대한 통계량, 이 경우엔 표준편차를 구해서 discriminator에 추가적인 특징으로 입력해준다. 이렇게 되면 generator 샘플의 표준편차가 실제 샘플의 표준편차와 유사해지도록, 즉 다양성이 높아지도록 학습해나가는데 도움이 된다.

### Equalized Learning Rate

<div>
$$
v_{t + 1} \gets \beta_2 v_t + (\beta_2 - 1)(\frac{\partial L}{\partial W_t})^2 \\
W_{t + 1} \gets W_t - \frac{\eta}{\sqrt{v_{t + 1} + \epsilon}}\frac{\partial L}{\partial W_t}
$$
</div>

<div>
$$
v_{t + 1} \gets \beta_2 v_t + (\beta_2 - 1)(\alpha\frac{\partial L}{\partial W_t})^2 \\
W_{t + 1} \gets W_t - \frac{\eta}{\sqrt{v_{t + 1} + \epsilon}}\alpha\frac{\partial L}{\partial W_t}
$$
</div>

<div>
$$
aW_{t + 1} \gets \alpha W_t - \frac{\eta\alpha}{\sqrt{v_{t + 1} + \epsilon}}\frac{\partial L}{\partial W_t}
$$
</div>

[^1]: https://arxiv.org/abs/1710.10196
[^2]: https://arxiv.org/abs/1812.04948
[^3]: https://arxiv.org/abs/1912.04958
[^4]: https://arxiv.org/abs/1406.2661
[^5]: https://arxiv.org/abs/1511.06434
[^6]: https://arxiv.org/abs/1606.03498
[^7]: https://arxiv.org/abs/1701.07875
[^8]: https://arxiv.org/abs/1704.00028
[^9]: https://arxiv.org/abs/1705.02894
[^10]: https://arxiv.org/abs/1706.08500
[^11]: https://arxiv.org/abs/1801.04406
[^12]: https://arxiv.org/abs/1802.05957
[^13]: https://arxiv.org/abs/1802.05637
[^14]: https://arxiv.org/abs/1805.08318
[^15]: https://arxiv.org/abs/1809.11096
[^16]: https://dl.acm.org/citation.cfm?id=1553380