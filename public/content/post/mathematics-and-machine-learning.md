+++
autoThumbnailImage = true
categories = ["thoughts"]
coverImage = "http://res.cloudinary.com/rosinality/image/upload/v1492734059/covers/field-of-math"
coverSize = "partial"
date = "2017-04-25T15:20:18+09:00"
hasMath = false
isCJKLanguage = true
keywords = ["machine learning", "mathematics", "scikit-learn"]
tags = ["machine learning", "mathematics", "scikit-learn"]
thumbnailImagePosition = "left"
title = "머신 러닝과 수학, 그리고 머신 러닝에 입문하기"

+++

데이터 분석에 무슨 종류의 수학이 필요한가 생각해보면, 미적분이나 선형대수는 기본이라고 할 수 있고. 실해석, 측도론, 확률론/확률과정론, 함수해석, 그리고 이것들을 하기 이전 혹은 이후에 위상수학이 필요하고. 물론 최적화나 정보이론도 필요하다. Michael Jordan의 read list나 머신 러닝 추천 도서 같은 걸 보면 여기다 통계학 책들을 얹어놓은 형태로 구성되어 있다. 요즘은 미분기하학도 종종 등장한다. 정보기하 때문이기도 하고 매니폴드의 특성에 대해서 다루는 경우도 종종 있기 때문에. 신호처리는 당연히(?) 신호 다루는 영역에서는 필수고 전통적인 컴퓨터 비전 쪽에서는 기하학을 많이 다뤘다. 통계역학 같은 것도 여러모로 도움이 된다고 하여 공부할 것을 권하기도 한다. 이전의 머신 러닝 커리큘럼들을 찾아보면 실제로 이런 수학들 중 많은 부분을 커버하고 있었다. 요즘은 딥 러닝이 떠서 좀 달라지지 않았을까 싶기도 하다.

보면 응용 분야일 수록 오히려 기초적인 학문에 대한 이해가 도움이 되는 것 같다. 당연한 것이 남들이 잘 모르는 걸 알고 있으면 그건 강점이 될 수 있으니까.

그렇지만 겔만의 표현대로 일단 운전할 것을 가르치면, 그러면 나중에 궁금해서건 필요해서건 내연기관의 작동 방법을 배울 수 있을지도 모른다.

사실 운전하는 것을 배우는 것도 쉬운 것은 아니다. 병렬분산처리를 제대로 하려면 MPI는 아니더라도 일단 자바/스칼라를 배워야 하고 요즘 유행하는 GPGPU 컴퓨팅을 직접 구현해서 하려면 C/C++에 CUDA나 OpenCL을 배워야 한다. (전산하는 사람들이 하는 것처럼 프로그래밍을 배우자면 당연히 알고리즘, 자료구조 등등이 필요하지만 일단 그런 또 다른 기초는 빼고 생각한다고 하면.)

그렇지만 이런 본격적인 종류의 운전을 배우지 않더라도, 파이썬이나 R 프로그래밍을 할 수 있으면 할 수 있는 것이 꽤 많고 배울 수 있는 것이 꽤 많지 않을까? pandas나 scikit-learn을 써보면 데이터를 어떻게 다루고 전처리해야 하는지, 어떤 방법들이 있으며 그 방법들의 논리는 무엇이고 또 그런 방법들의 장단점은 무엇인지, 어떤 문제와 어떤 데이터에 쓸 수 있는 방법들이 어떤 것이 있는지, 그리고 머신 러닝과 데이터 분석의 베스트 프랙티스는 어떤 것인지(그러니까 언더피팅/오버피팅이 무엇이며 어떻게 대처해야 하는지, train/valid/test 셋을 분리하고 cross-validation을 사용하는 것 같은 기초적인 것부터도) 등등을 알 수 있고 사실 그런 지식들을 합치면 작은 것은 아닐 것이라고 생각한다. 그리고 많은 사람들이 이런 식으로 데이터 분석을 접하지 않았을까?

그런 것들을 접하고 나면, 머신 러닝에 애정(?)이 있다면 그 방법들에 대해서 배우고 또 필요한 수학에 대해서 접할 수 있게 될 것이다. 뭐 그런 정도의 애정이 없다고 해도 실용적인 지식이라도 남으면 여기저기 쓸 수 있는 곳이 많이 있지 않을까. 거기다 요즘은 scikit-learn 이전에 tensorflow를 접하고 선형 회귀나 랜덤 포레스트 이전에 뉴럴넷을 접하는 사람들이 적지 않은 것 같은데, 그러면 그런 실용적인 지식들도 나름 중요한 기초로 여겨지게 될 지도 모르겠다.