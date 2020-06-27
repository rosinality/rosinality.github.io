+++
autoThumbnailImage = true
categories = ["thoughts"]
coverImage = "http://res.cloudinary.com/rosinality/image/upload/v1492734059/covers/uncertainty.jpg"
coverSize = "partial"
date = "2017-04-21T10:35:56+09:00"
hasMath = false
isCJKLanguage = true
keywords = ["bayesian inference", "neural network"]
tags = ["bayesian inference", "neural network"]
thumbnailImagePosition = "left"
title = "베이지안 뉴럴 네트워크"

+++

https://twitter.com/ylecun/status/764033716276428800

인상적인 성능을 내는 뉴럴넷 모형을 학습하려면 (연산능력의 증가와는 별개로) 늘 2-3주는 필요하다는 이야기가 있다. 수백 개의 GPU를 쓰면 모형도 그만큼 복잡해져서 학습에 필요한 시간이 증가한다. 링크한 트윗처럼 2-3주 정도가 사람들이 투자할 수 있는 시간의 최대치이기 때문일 수도 있다.

베이지안 뉴럴넷이 제공하는 장점(불확실성의 반영)이 아주 절실하지 않다면, 최신의 성능을 보여주는 모형을 학습하는데 걸리는 시간보다 학습 시간이 너무 오래 걸려서는 곤란하다. 그러니까 동일한 모형의 베이지안 버전을 학습하는데 걸리는 시간이 기본 모형을 학습하는데 걸리는 시간보다 두 배가 걸린다면 기본 모형의 학습에 2-3주가 걸릴 때 베이지안 뉴럴넷을 학습하는데 4-6주가 걸릴 수도 있고 그건 너무 많은 시간을 투자해야 하는 것이다. 2-3주 안에 학습이 끝나는 베이지안 뉴럴넷을 구성한다면 2-3주 안에 학습할 수 있는 기본적인 모형보다 덜 인상적인 모형이 될 수밖에 없다.

그러니 베이지안 뉴럴넷의 핵심적인 과제는 기존의 모형에 비해서 학습에 너무 긴 시간을 추가적으로 요구하지 않아야 한다일 것이다. 테스트시에도 추가적인 시간이 너무 크게 요구되면 곤란하겠지만 일단 그 문제는 후순위로 둬도 될 것 같다.
그런데 반대로 추가적인 학습 시간을 크게 요구하지 않고도 베이지안 뉴럴넷을 학습시킬 수 있다면 베이지안 모형을 쓰지 않을 이유가 있을까? 기존 모형이 완벽한 성능을 보여주는 것이 아닌 이상.

![Lecun on Bayesian Neural Network](http://res.cloudinary.com/rosinality/image/upload/v1492734059/images/lecun-bayesian-net.jpg)