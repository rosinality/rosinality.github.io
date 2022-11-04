+++
autoThumbnailImage = true
categories = ["sorta informative"]
coverImage = "http://res.cloudinary.com/rosinality/image/upload/v1492734059/covers/attractor.jpg"
coverSize = "partial"
date = "2017-04-21T10:51:13+09:00"
hasMath = false
isCJKLanguage = true
keywords = ["interpretability", "nonlinear model", "generalized addtive model", "gradient boosting", "partial dependence plot"]
tags = ["interpretability", "nonlinear model", "generalized addtive model", "gradient boosting", "partial dependence plot"]
thumbnailImagePosition = "left"
title = "비선형 모형의 해석가능성"

+++

해석하기 어려운 블랙박스 모형이라고 하면 대충 어떤 것이 있을까? 아마 대표적인 것이 트리 앙상블일 것이다. 그런데 트리 앙상블이 왜 해석하기 어려운가? 반대로 해석하기 쉬운 모형이란 어떤 모형인가? 선형 모형은 해석이 쉽다. 선형 모형에서는 변수의 증감에 따라 계수만큼 선형으로 응답 변수가 변화한다. 트리 앙상블과 같은 비선형 모형에서는 이런 해석이 어려운가? 당연히 선형 모형에서처럼 간단하진 않다. 그런데 변수의 변화에 따라 응답 변수가 어떻게 변화하는가를 해석하는 건 비선형 모형에서도 별로 어렵지 않다.

![GAM Smoother](http://res.cloudinary.com/rosinality/image/upload/v1492734059/interpretability/california4.png)
![PDP](http://res.cloudinary.com/rosinality/image/upload/v1492734059/interpretability/pdp.png)

GAM의 Smoother와 GBDT의 PDP 플롯

선형 모형까지는 아니지만 이 정도면 각 변수의 효과를 해석하기 그렇게 어려운 것도 아니다. 간단히 생각해보면 다른 변수들을 고정시키고 한 변수를 변화시키면서 응답 변수가 어떻게 변화하는지를 관찰하는 건 어떤 모형에서나 가능한 것이다.

사실 GBDT 같은 블랙박스 모형을 해석하기 어렵게 하는 건 각 변수의 개별적인 효과를 판단하기 어렵다는 것보단 GBDT가 알아서 상호작용을 찾아내 반영하는 모형이라는 점이 더 크다. 상호작용이 해석을 어렵게 하는 것은 선형 모형에서도 마찬가지다. 2-way 상호작용이야 간단하지만 3-way라면? 4-way라면? 5-way라면? 상상만 해도 난감해지는 일이다.

![PDP Interaction](http://res.cloudinary.com/rosinality/image/upload/v1492734059/interpretability/pdp-interaction.png)

물론, 대충 어떤 상호작용이 중요한 것인지 감이 있으면 PDP를 써서 해석을 하는 것도 그렇게 어려운 일은 아니다

그러니 이론적 배경이 있어 상호작용 등을 선형 모형 등의 모형에 직접 기술하는 것이나 그런 상호작용을 알아서 발견해내는 블랙박스 모형에서, 이론적 배경 혹은 변수 중요도(Variable Importance) 등을 사용해 상호작용의 성질을 탐색하는 것이나 비슷한 일이라고 볼 수 있을 것이다. 그렇다면 Breiman이 지적하는 것처럼 데이터에 대해 최대한 정확한 정보를 제공할 수 있는 블랙박스 모형을 사용한 뒤 이론적 정보 등을 가지고 모형을 해석하는 방향으로 접근하는 것이 적절한 일일 수도 있다.