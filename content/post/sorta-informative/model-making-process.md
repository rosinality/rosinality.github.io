+++
autoThumbnailImage = true
categories = ["sorta informative"]
coverImage = "http://res.cloudinary.com/rosinality/image/upload/v1492734059/covers/brussels-forest"
coverSize = "partial"
date = "2017-05-08T22:31:57+09:00"
hasMath = false
isCJKLanguage = true
keywords = ["machine learning", "model making", "underfit", "overfit"]
tags = ["machine learning", "model making", "underfit", "overfit"]
thumbnailImagePosition = "top"
title = "머신 러닝 모델을 만들기"

+++

머신 러닝을 하는데 성능이 잘 안 나온다는 질문이 종종 보여서, 모델 성능 평가의 왕도를 소개해봄. 사실 Deep Learning book의 챕터 11에 나오는 내용.

전처리를 하고 데이터의 특성을 살펴보고 하는 탐색 과정이 끝나면 본격적으로 머신 러닝 알고리즘을 데이터에 적용하게 됨. 이후 모형의 성능을 평가하게 되는데 결국 underfit이냐 overfit이냐를 가지고 따지게 됨.

우선적으로 봐야 하는 것은 학습 데이터에 대해서 성능이 충분히 나오는가 하는 것. 학습 데이터에 대해서도 성능이 안 나오는 경우가 underfit. 가능한 문제는 몇 가지가 있는데, 우선 데이터의 질이 좋지 않은 경우, 문제 자체가 풀기 어려운 경우 (예를 들어 데이터에 정보가 별로 없는 경우), 모델의 표현력이 충분하지 않은 경우. 모델의 표현력이 충분하지 않다면 모델의 표현력을 높여야 하고(혹은 feature engineering을 하거나), 데이터의 질이 좋지 않다면 데이터의 질을 개선해야 하고, 가지고 있는 데이터가 문제를 푸는데 적절하지 않다면 다른 데이터를 사용해야 함.

이 과정에서 모형을 디버깅하는 것도 중요함. 아예 안 돌아가는 방식으로 모형을 구현해버린 경우가 있음. 이걸 테스트하는 가장 쉬운 방법 중 하나는 아주 적은 수의 데이터에 대해서 모형을 학습시켜보는 것. 충분한 표현력을 가진 모형이라면 이런 경우에 cost를 0에 접근시킬 수 있음. 이게 안 된다고 하면 모형에 문제가 있거나 표현력이 부족한 것.

그러고 나면 이제 테스트 데이터에 대해서 성능이 충분히 나오는가를 평가함. (정확하게 말하면 이 단계에서는 validation set에 대해서 평가하고 최종 성능은 test set에 대해서 평가해야 함.) 성능이 충분히 나온다면 잘 된 것. 성능이 충분하지 않다면 overfit이 발생한 것.

overfit이 발생한 경우에 해법은 데이터를 더 모으거나 regularization을 사용하는 것. 데이터를 더 모으는 것이 데이터를 쉽게 모을 수 있다면 가장 좋겠지만 그렇지 않은 경우에는 regularization을 위해 하이퍼 파라미터를 튜닝하는 작업을 거치게 됨.

몇 가지 take home message는,

1. 안 풀리는 문제는 안 풀림.
2. 데이터가 없으면 문제를 풀기 어려움.
3. 데이터를 쉽게 모을 수 있다면 데이터를 모으는 것이 최선.
4. 모형의 성능 평가는 체계적으로.