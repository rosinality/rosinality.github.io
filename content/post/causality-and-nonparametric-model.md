+++
autoThumbnailImage = true
categories = ["thoughts"]
coverImage = "http://res.cloudinary.com/rosinality/image/upload/v1492734059/covers/domino.jpg"
coverSize = "partial"
date = "2017-04-21T10:29:01+09:00"
hasMath = false
isCJKLanguage = true
keywords = ["causality", "causal inference", "nonparametric model"]
tags = ["causality", "causal inference", "nonparametric model"]
thumbnailImagePosition = "left"
title = "인과관계와 비모수 모형"

+++

인과 그래프 모형 같은 경우는 전형적인 데이터의 생성 과정을 기술하는 모형이지만 동시에 알고리즘적 모형에서 흔히 발견할 수 있는 비모수적 함수 추정이 결합되어 있다. 예컨대 Pearl은 인과 그래프에 부합하는 구조방정식을 비모수적인 것으로 가정한다. A가 B와 C에 인과적 영향을 미치는 방향성은 기술되어야 하지만 영향을 미칠 때 영향을 미치는 방식은 비모수적으로 추정되어야 한다는 것이다. 왜? A가 B에 인과적 영향을 미친다고 해서 그 영향을 미치는 방식이 선형일 것이라는 보장은 없으니까. (그리고 상호작용을 그래프에 그려넣기 힘들다는 난점도 해결된다. profit!)

무언가를 설명한다는 것은 일반적으로 인과적 관계를 밝혔음을 의미한다. 실험을 하는 것이 아니라면 인과적 관계를 밝히기 위해선 인과 모델링을 해야 하고 그건 데이터를 생성하는 인과적 관계를 지정한다는 것을 의미한다. 그렇지만 그렇게 인과적 관계를 모델링했다면 정확한 정보를 얻기 위해선 - 물론 관계가 선형인 즐거운 경우가 생각보다 많긴 하지만 - 알고리즘적 모델이 유용할 때가 있다. Breiman이 지적한 두 문화의 문제는 인과 관계를 밝히는 것이 목적인 경우에는 대충 이런 식으로 종합될 수 있을 거라는 생각을 잠깐 해봤다.