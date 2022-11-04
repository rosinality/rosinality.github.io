+++
keywords = ["deep learning", "optimization", "learning rate"]
tags = ["deep learning", "optimization", "learning rate"]
categories = ["sorta-informative"]
isCJKLanguage = true
hasMath = false
coverImage = "http://res.cloudinary.com/rosinality/image/upload/v1492734059/covers/cover01.jpg"
coverSize = "partial"
autoThumbnailImage = true
thumbnailImagePosition = "left"
title = "Learning rate 튜닝"
+++

Learning rate는 Ian Goodfellow의 Deep Learning 책에도 나오듯 가장 중요한 하이퍼파라미터라고 할 수 있다. 또 그만큼 중요한 하이퍼파라미터가 바로 learning rate를 어떻게 변화시킬 것인가 하는 learning rate scheduling이다. learning rate의 설정에 따라 전혀 학습이 되지 않을 수도 있고, 그럭저럭 학습이 될 수도 있고, 또는 기대 이상의 결과를 얻을 수도 있다.

