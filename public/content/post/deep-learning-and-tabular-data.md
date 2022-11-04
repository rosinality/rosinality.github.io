+++
autoThumbnailImage = true
categories = ["thoughts"]
coverImage = "http://res.cloudinary.com/rosinality/image/upload/v1492734059/covers/table.jpg"
coverSize = "partial"
date = "2017-04-21T16:11:42+09:00"
hasMath = false
isCJKLanguage = true
keywords = ["deep learning", "data analysis", "tabular data", "machine learning"]
tags = ["deep learning", "data analysis", "tabular data", "machine learning"]
thumbnailImagePosition = "left"
title = "딥 러닝과 표 형태의 데이터"

+++

전통적 통계적 모델링의 대상인 표 형태의 데이터tabular data에 대해서는 딥 러닝이 힘을 못 쓴다(?)는 말을 흔히 한다. 사실 이건 딥 러닝이 이미지나 텍스트 처리에서 워낙 무지막지한 성능을 보여주기 때문에 그에 비해서 덜 인상적이라는 의미가 크고, 비정형이 아닌 정형의, 표 형태의 데이터에 대해서 당연히 그럭저럭 괜찮은 성능을 보여주는 경우가 많다. 다만 앙상블 트리 같은 모형들이 그런 데이터에 대해서는 더 나은 성능을 보여주는 경우가 많다. 아니 보면 거의 대부분인 듯 싶다.

왜 그런가? 여기에 대해 이론적 분석을 한 연구가 있는지는 모르겠다. 어쩌면 비교적 저차원의 함수 추정에는 앙상블 트리 모형 같은 모형이 더 적합한 것일지도 모른다. 그러나 이미지나 텍스트 같은 고차원의 괴상한 데이터에는 그런 괴상함을 상대할 수 있는 가정들을 반영할 수 있고 레이어의 중첩을 통해 지수적인 표현력 증가를 얻을 수 있는 뉴럴넷 혹은 딥 러닝이 적합한, 혹은 유일하게 가능한 방법인 것일 수도 있다.

위와 같은 사실을 다르게 말하면 딥 러닝이 보여주는 강력한 예측 능력이 기존의 통계적 접근에 위협이 된다면, 당연히 기존의 통계적 모델링이 일반적으로 다뤄왔던 데이터에 대해 딥 러닝 수준의 예측 능력을 보여주는 다른 머신 러닝 알고리즘 또한 위협적이라고 해야 할 것이다. 그런데 그런 머신 러닝 알고리즘은 딥 러닝이 2000년대 중반 이후 본격적으로 주목을 받기 이전부터 주목을 받아왔는데, 그런 알고리즘들이 지금까지 통계적 모델링에 큰 위협이 되지 않았다면 딥 러닝도 통계적 모델링에 큰 위협이 되지 않을 것이라고 봐도 좋을 것이다.