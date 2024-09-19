+++
keywords = ["machine learning"]
tags = ["machine learning"]
categories = ["sorta informative"]
isCJKLanguage = true
hasMath = true
coverImage = "https://res.cloudinary.com/rosinality/image/upload/f_auto,q_auto/v1/covers/transformer"
coverSize = "partial"
autoThumbnailImage = true
thumbnailImagePosition = "top"
date = 2023-11-03T18:27:16+09:00
title = "트랜스포머 모델 선택의 기원에 대하여"
draft = true
+++

트랜스포머는 이제 너무나 유명한 모델이고 아마 딥 러닝 모델 중에서 트랜스포머보다 많은 설명이 작성된 모델 또한 없을 것 같다. 그런 상황에서 트랜스포머의 디자인에 대한 글을 또 쓰는 것이 의미가 있을까?

그렇지만 조금 다르게 트랜스포머라는 모델의 디자인적 선택의 기원과 유래, 혹은 반드시 그 아이디어에서 차용한 것은 아니더라도 유사함을 발견할 수 있는 과거의 사례들을 짚어보면 재미있지 않을까 싶었다. 트랜스포머도 이제 발표된지 6년이 넘어가는 오래된 모델이니 디자인적 유래를 소개하는 것은 그보다 더 오래된, 딥 러닝 판에서는 까마득히 오래된 시점의 일들을 소개하는 것이 될 듯 싶다. 그러니 옛 이야기를 듣는 것처럼 생각할 수도 있지 않을까.

주의사항 한 가지. 여기서 소개하는 기원이나 이전 아이디어 같은 경우는 대부분 내 기억과 익숙함에 의존하는 것이기에 실제로 최초라고 보장할 수는 없다. 사실 최초의 것을 찾아내려고 노력했다기보다는 오히려 트랜스포머와 보다 인접한 시점 혹은 더 유사하거나 가까운 것을 골랐다고 하는 것이 맞을 듯 싶다.

단적으로 말하면 트랜스포머 디자인과 관련된 그저 하고 싶은 이야기를 하려는 것이다.

# Self Attention

Hard attention[^1]의 사례를 먼저 가져올 수도 있겠지만 softmax를 사용하는 일반적인 soft attention에 대해서는 Bahdanau[^2]의 전설적인 논문에서 시작해도 큰 문제는 없을 듯 싶다. 이때는 $\operatorname{tanh}$를 activation으로 사용하는 작은 뉴럴 네트워크를 attention score로 사용했다. $\operatorname{softmax}(v\operatorname{tanh}(Wx))$ 같은 식으로. 트랜스포머에서처럼 dot product를 사례로는 Luong[^3]의 논문을 들 수 있을 것 같다. 사실 여기에는 dot product 뿐만 아니라 attention의 여러 가능한 디자인에 대한 ablation이 있다. RNN 시절이기도 해서 attention을 어느 위치에서 계산해야 하는가 하는 것도 중요한 디자인적 선택이었다.

그렇다면 self attention의 시작은 무엇일까? Attention Is All You Need에서 인용하고 있는 것처럼, 트랜스포머가 등장하기 직전에 self attention이라고 볼 수 있는 동일 시퀀스 내에서 attention을 계산하는 방법들이 등장하기 시작했다. 이 때의 아이디어는 LSTM이 시퀀스를 고정된 크기의 상태 벡터로 압축해나가면서 먼 거리에 있는 단어들을 적절하게 다루거나 반영하는 것이 어려울 수 있다, 즉 원거리에 있는 단어들 사이의 관계를 모델링하기 어려울 수 있다는 아이디어에서 시작했다. 인코더 RNN으로 입력 시퀀스를 압축해서 나온 상태 벡터 하나만으로는 긴 텍스트를 다루는 것이 어렵다는 아이디어에서 attention이 시작되었다는 것을 생각하면 인코더와 디코더 사이 뿐만 아니라 인코더나 디코더 내에서도 그 문제를 해소할 필요가 있다는 아이디어로 이어졌다고 볼 수도 있겠다.

어쨌든 여기까지는 attention만으로도 충분할 수 있다는 과감함까지는 이르지 못했고 LSTM을 attention이 적절히 보강해줄 수 있을 것이라는 단계의 결과였다.

# Multi-Head Attention

트랜스포머 self attention의 주요한 특징은 dot product attention이라는 것과 함께 여러 attention (head)를 결합한 attention이라는 것일 것이다. attention 하나가 아니라 여러 attention을 결합하자는 아이디어는 A Structured Self-Attentive Sentence Embedding[^7]에서 유사한 시도를 찾아볼 수 있을 듯 싶다. 트랜스포머에서처럼 보통 attention은 특정한 부분, 다시 말해 토큰을 가져오도록 학습이 되므로 여러 토큰을 가져와서 결합할 수 있으려면 여러 개의 attention이 필요할 수 있다는 아이디어였다.

# Skip Connection



[^1]: Mnih, V., Heess, N., & Graves, A. (2014). Recurrent models of visual attention. Advances in neural information processing systems, 27. [https://arxiv.org/abs/1406.6247](https://arxiv.org/abs/1406.6247)
[^2]: Bahdanau, D., Cho, K., & Bengio, Y. (2014). Neural machine translation by jointly learning to align and translate. arXiv preprint arXiv:1409.0473. [https://arxiv.org/abs/1409.0473](https://arxiv.org/abs/1409.0473)
[^3]: Luong, M. T., Pham, H., & Manning, C. D. (2015). Effective approaches to attention-based neural machine translation. arXiv preprint arXiv:1508.04025. [https://arxiv.org/abs/1508.04025](https://arxiv.org/abs/1508.04025)
[^4]: Cheng, J., Dong, L., & Lapata, M. (2016). Long short-term memory-networks for machine reading. arXiv preprint arXiv:1601.06733. [https://arxiv.org/abs/1601.06733](https://arxiv.org/abs/1601.06733)
[^5]: Parikh, A. P., Täckström, O., Das, D., & Uszkoreit, J. (2016). A decomposable attention model for natural language inference. arXiv preprint arXiv:1606.01933. [https://arxiv.org/abs/1606.01933](https://arxiv.org/abs/1606.01933)
[^6]: Paulus, R., Xiong, C., & Socher, R. (2017). A deep reinforced model for abstractive summarization. arXiv preprint arXiv:1705.04304. [https://arxiv.org/abs/1705.04304](https://arxiv.org/abs/1705.04304)
[^7]: Lin, Z., Feng, M., Santos, C. N. D., Yu, M., Xiang, B., Zhou, B., & Bengio, Y. (2017). A structured self-attentive sentence embedding. arXiv preprint arXiv:1703.03130. [https://arxiv.org/abs/1703.03130](https://arxiv.org/abs/1703.03130)