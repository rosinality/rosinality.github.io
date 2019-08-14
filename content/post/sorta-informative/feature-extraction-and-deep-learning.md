+++
autoThumbnailImage = true
categories = ["sorta informative"]
coverImage = "http://res.cloudinary.com/rosinality/image/upload/v1492734059/covers/imagenet.jpg"
coverSize = "partial"
date = "2017-05-08T22:41:37+09:00"
hasMath = false
isCJKLanguage = true
keywords = ["feature extaction", "deep learning", "machine learning"]
tags = ["feature extaction", "deep learning", "machine learning"]
thumbnailImagePosition = "top"
title = "특징 추출(Feature Extraction)과 딥 러닝"

+++

https://sinews.siam.org/Details-Page/deep-deep-trouble

뉴럴넷 연구를 하던 사람들이 오랜 겨울을 지나왔던 것처럼 이미지 처리에서, 이젠 전통적인 방법이라고 불리는 방법들을 연구하던 사람들의 고민이 깊은 모양이다.

뉴럴넷이 왜 이미지 문제에서 (뉴럴넷이 또 강력한 성능을 보여주고 있는 텍스트 등의 시퀀스 처리 문제 등은 일단 빼고) 강력한 성능을 보여주는가? 이미지 분류를 위한 정석적인 CNN 구조를 생각해보자. CNN의 가장 윗단은 그냥 linear classifier일 뿐이다. 그 밑에 있는 전체는 feature extractor다. feature extractor는 기존의 머신 러닝 방법에서도 계속적으로 써왔던 것이다. 차이가 있다면 뉴럴넷에서는 feature extractor가 데이터를 통해 학습되고, 기존의 방법에서는 우아한 수학적 방법 등을 통해 손으로 설계되었다는 차이가 있을 뿐이다. 그리고 feature extractor가 데이터를 통해 학습된다는 것 자체가 딥 러닝이 강력한 성능을 보여주는 원인이다.

왜 feature extractor를 데이터를 통해 학습한다는 것이 높은 성능을 보장하는가? feature extractor를 학습한다면 linear classifier에 필요한 feature들을 네트워크의 구조가 허용하는 한에서 bias 없이 추출할 수 있다. 그러니까 데이터에서 필요한 정보들을 데이터에 대해서 사람이 부과하는 제약에 의존하지 않고 추출할 수 있다는 것이다. 이를 이유로 Hinton은 뉴럴넷을 동작시킬 수 있다면 전통적인 방법들은 뉴럴넷을 따라올 수 없다고 표현하기도 했다.

반면 기존의 feature extraction 방법들은 사람이 데이터 갖고 있는 이해를 기반으로 데이터에서 유용한 정보들을 추출한다. 예를 들어 이미지에 대한 이해를 기반으로 주위 픽셀값과의 관계가 과제에 유용한다고 판단되었다면 그 관계를 값으로 정의해 classifier를 학습시킨다. 그러나 우리가 이미지 데이터에 대해서 충분히 이해하고 있지 못하고 이미지 데이터에서 끌어낼 수 있는 유용한 feature들을 모두 추출하지 못한다면? 당연히 그렇게 소실된 정보만큼 bias가 발생한다.

따라서 전통적인 방법이 딥 러닝만큼의 성능을 보여주지 못한다는 것은 우리가 데이터를 충분히 이해하고 있지 못하다는 의미라고 볼 수 있다. 즉 우리의 prior가 충분하지 않다는 것이 bias를 만들어낸다.

딥 러닝 모형의 내부에서 일어나는 일들을 이해하기 어려운 것도 이러한 문제와 상통한다. 우리가 이미지에 대해서 충분히 잘 이해하고 있지 못하기에 충분히 좋은 feature extractor를 손으로 설계하고 있지 못한데 딥 러닝 모형에서 학습된 feature extractor를 이해하는 것이 쉬운 일일까? 반대로 손으로 만들어진 feature extractor가 학습된 feature extractor에 범접할 만큼 정교하다면 아마 그 feature extractor를 이해하기는 매우 어려울 것이다.

그런데 우리가 이미지 같은 데이터를 충분히 이해할 수 있는 날이 올까? 오지 않으리라는 보장은 없지만 아주 어려운 일이라는 것은 사실일 것이다. 확률 밀도조차 존재하지 않는 데이터를 이해한다는 것이 쉬운 일은 아닐 테니까.