+++
categories = ["sorta informative"]
date = "2017-04-21T01:05:02+09:00"
hasMath = false
isCJKLanguage = true
tags = ["neural network", "deep learning", "batch normalization"]
title = "배치 정규화"
coverImage = "http://res.cloudinary.com/rosinality/image/upload/v1492734051/covers/cover10.jpg"
coverSize = "partial"
autoThumbnailImage = true
thumbnailImagePosition = "top"

+++

배치 정규화는 엄청나게 효과적인 방법이지만 또 사람들이 그렇게 우아한 방법이라고 생각하지 않는 방법이기도 한 듯 하다. 생각해보면 평균을 미니 배치로 추정한다는 것까지는 몰라도 그걸로 롤링 평균을 계산해서 테스트할 때 사용한다거나 하는 것이 아주 깨끗하지는 않긴 하다.

그래서 배치 정규화를 대체하기 위한 방법도 여럿 등장했다. Layer Normalization은 RNN에서는 쓸만하다고 하지만 CNN에서는 Batch Norm에 미치지 못한다고 저자들도 이야기하고 있다. Weight Normalization은 트레이닝 속도는 Batch Norm과 비슷한 정도까지 도달했지만 테스트셋 에러에서는 썩 좋은 결과를 보여주지 못했다.

Batch Norm은 각 레이어에서 평균과 분산으로 스케일링을 해주는 동시에 평균, 분산을 미니 배치를 통해 계산하기에 필연적으로 노이즈를 포함시키게 되고, 또 이 노이즈가 정규화에 도움을 준다는 특징을 갖는다. 단위를 표준화시켜 학습 속도를 가속하는 것은 다른 방법으로도 가능할 수 있다. 그러나 노이즈를 통해 정규화하는 것까지 동시에 성취하기는 쉽지 않을 것이다.