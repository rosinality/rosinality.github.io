+++
autoThumbnailImage = true
categories = ["sorta-informative"]
coverImage = "http://res.cloudinary.com/rosinality/image/upload/v1492734059/covers/batches.jpg"
coverSize = "partial"
date = "2017-04-21T16:18:05+09:00"
hasMath = false
isCJKLanguage = true
keywords = ["neural network", "deep learning", "batch normalization"]
tags = ["neural network", "deep learning", "batch normalization"]
thumbnailImagePosition = "top"
title = "배치 정규화 2"

+++

batch normalization의 문제 의식은 뉴럴넷에서 하나의 레이어의 출력은 이전의 레이어의 출력에 의해 영향을 받기에, 깊은 뉴럴넷에서는 이런 "영향"들이 누적되는 경향이 있다는 것이었다. 그러니 이전 레이어들의 파라미터들을 바꾸면 그 영향이 다시 쭉 누적되고, 그러면 다음 레이어에서는 그 변화에 맞춰 파라미터를 바꿔야 한다. 그러니까 한 레이어의 파라미터에 대한 그래디언트가 이전 레이어의 출력에 크게 영향을 받는다는 것이고, 이게 학습 속도를 느리게 만든다는 것이었다. (높은 learning rate을 쓰기도 어렵고.)

이런 문제를 해결하기 위해서 레이어의 출력을 whitening하는 방법을 생각할 수 있다. 그런데 이건 계산이 너무 많이 필요해서 힘들다. 그래서 제대로 whitening하는 대신 각 히든 유닛에 대해서 개별적으로 평균과 분산이 0, 1이 되도록 정규화(normalize)하도록 한다. 그런데 모든 트레이닝 데이터에 대해서 평균과 분산을 구해서 정규화하긴 힘드니까(사실상 불가능하다) 각 배치에 대해서 평균과 분산을 구해서 평균과 분산을 추정해버리자. 이게 batch normalization의 발상이었다.

그런데 이렇게 하니까 아주 바람직한 부수 효과가 동반됐다. 배치 크기는 대체로 많아봤자 몇백 개 수준인데 그걸로 평균과 분산을 추정하니까 노이즈가 엄청나게 발생했다. 노이즈가 발생하는 것이 나쁜가? 아니 오히려 바람직하다. batch normalization을 썼더니 학습 속도가 빨라질 뿐만 아니라 테스트 에러도 더 낮아진 것이다. 노이즈가 일반적으로 뉴럴넷을 강건하게 만든다는 것을 생각해보면 당연한 결과다. 그래서 이후 dropout은 좀 덜(?) 중요해지게 됐다.

어쨌든 그래서 이후 batch normalization은 CNN에서는 표준이 됐다. 학습 속도도 빨라지고 성능도 좋아지는데 쓰면 안 되는 상황이 아닌 이상 쓰는 것이 당연하다.

그렇지만 batch normalization은 우아한 방법은 아니다. 배치로 평균과 분산을 추정하기에 배치 크기에 제약이 생겼다. 배치 크기가 작으면 작을수록 추정에 의한 노이즈가 커지고 너무 커지면 이게 또 학습이 어려워지는 것이다...거기다 배치로 구한 평균과 분산을 moving average로 누적해서 달고 다녀야 한다.

이런 우아하지 못함(?)을 개선하기 위해 layer normalization이나 weight normalization이 제안된 것이다. 위와 같은 문제에 대해선 훨씬 우아하다고 할 수 있겠지만, 그리고 layer normalization 같은 경우엔 RNN에 적용해 성능이 좋아지기도 하지만, 결정적인 문제는 batch normalization이 강점을 보이는 이미지 입력에 대한 CNN에서는 batch normalization 정도의 성능을 보여주지 못하고 있다는 것이다. (이미지가 아닌 경우에는 layer normalization을 적용하는 경우가 보인다.) 뭐 그러니까 아직까지는 batch normalization을 대체할 방법은 없다고 봐야할 것이다.