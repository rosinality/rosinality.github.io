+++
keywords = ["deep learning", "machine learning"]
tags = ["deep learning", "machine learning"]
categories = ["thoughts"]
isCJKLanguage = true
hasMath = false
date = "2017-11-03T10:03:59+09:00"
coverImage = "https://res.cloudinary.com/rosinality/image/upload/v1509636468/candle_kgokhm.jpg"
coverSize = "partial"
autoThumbnailImage = true
thumbnailImagePosition = "left"
title = "앞으로 재미있을지도 모르는 주제들"
+++

LSTM을 대신할 RNN Cell을 설계한다거나 하는 식의 기존의 구조를 개선하는 방안을 고안하는 것은 분명히 중요한 일이기는 하지만 그 자체로는 이전에는 불가능하거나 어려웠던 문제를 해결하기는 어렵다. 성능을 개선하는 정도라고 볼 수 있다.

조금 더 재미있는 것은 어렵거나 불가능했던 문제를 해결할 수 있는 구조나 알고리즘을 설계하는 것이다. 아니면 지금까지는 생각하지 못했던 새로운 문제라거나. 물론 그게 쉬운 일은 아니다.

그렇다면 풀 수 없었던 문제를 풀기 위해선 무엇이 필요할까?

한 가지 재미있는 접근들은 뉴럴 네트워크의 가중치를 생성하는 모형이나 알고리즘들이다. HyperNetworks[^1]에서부터 그 베이지안 확장인 Bayesian HyperNetworks[^2] 같은 것이 그 대표적인 사례이며 Conditional Batch Normalization[^3] 같은 것도 비슷한 경우라고 볼 수 있다. 이러한 알고리즘들은 뉴럴 네트워크를 유연하게 조절할 수 있는 기능을 제공한다는 방안을 제공한다는 것도 중요하지만 뉴럴 네트워크들의 공간을 이해할 수 있는 방향이라는 것이 또한 흥미롭다. 관련해서 재미있는 점 중 하나는 뉴럴 네트워크라는 하나의 함수가 가우시안 프로세스의 샘플로 이해할 수 있다는 사실이다.[^4]

다른 한 가지 방향은 뉴럴 네트워크에 장착할 수 있는 새로운 부품을 만드는 것이다. 예컨대 주의Attention나 외부 메모리External Memory 같은 구조가 그 대표적인 사례라고 할 수 있다. 이런 구조들은 단순히 기존 모델의 부품을 교체해 성능을 향상시키는 것을 넘어 아주 새로운 문제를 풀 수 있게 해준다. 정말로 획기적인 구조는 기존의 방식으로는 학습이 어려울 수도 있고, 따라서 학습 알고리즘도 중요한 문제가 된다.

마지막 방향은 우리가 풀고자 하는 문제와 데이터를 더 잘 이해하게 되는 것이다. LSTM은 장기적 관계를 모델링하는 과제에서 지속적으로 문제를 겪고 있다. 이게 우리가 LSTM으로 학습하려고 하는 데이터의 구조에 의해서 발생하는 문제는 아닐까? p(x1, x2, x3) = p(x1)p(x2|x1)p(x3|x1, x2)와 같이 chain rule로 분해한 방식으로 언어에 대한 생성 모델을 정의하고 학습하는 것이 적절한 문제일까? 이 방향으로도 더 많은 고찰이 필요할 것이다.

아마도 이런 문제들에 대해 앞으로 더 중요해질 수학적 도구는 정보이론과 기하학이지 않을까 생각한다. 데이터와 모델이라는 관계를 정보라는 관점으로 생각하면 정보이론의 문제가 되고 곡률이라는 관점으로 생각하면 기하학의 문제가 되니까. 같은 문제에 대한 서로 다른 관점이지만, 같은 문제이기에 서로의 도구를 쓸 수 있다.

물론 앞으로 어떤 수학이 유용한 도구로 부상할지는 알 수 없는 것이지만.

[^1]: Ha, D., Dai, A., & Le, Q. V. (2016). HyperNetworks. arXiv preprint. [https://arxiv.org/abs/1609.09106]
[^2]: Krueger, D., Huang, C. W., Islam, R., Turner, R., Lacoste, A., & Courville, A. (2017). Bayesian Hypernetworks. arXiv preprint. [https://arxiv.org/abs/1710.04759]
[^3]: de Vries, H., Strub, F., Mary, J., Larochelle, H., Pietquin, O., & Courville, A. (2017). Modulating early visual processing by language. arXiv preprint. [https://arxiv.org/abs/1707.00683]
[^4]: Lee, J., Bahri, Y., Novak, R., Schoenholz, S. S., Pennington, J., Sohl-Dickstein, J. (2017) Deep Neural Networks as Gaussian Processes. arXiv preprint. [https://arxiv.org/abs/1711.00165]

