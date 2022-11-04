+++
categories = ["thoughts"]
date = "2017-04-21T01:16:36+09:00"
hasMath = false
isCJKLanguage = true
tags = ["deep learning", "neural network", "interpretability"]
title = "딥 러닝 모형의 해석"
coverImage = "http://res.cloudinary.com/rosinality/image/upload/v1492734059/covers/interpret.jpg"
coverSize = "partial"
autoThumbnailImage = true
thumbnailImagePosition = "left"

+++

딥 러닝은 이론적 근거가 부족하고 해석이 어렵다는 등등의 평가를 흔히 받는다. 이건 통계학쪽 뿐만 아니라 머신 러닝 커뮤니티쪽에서도 (과거에는) 마찬가지였던 모양이다. 르쿤이 이론적 근거가 부족하다는 비판에 대해 아니 잘 돌아가는데 뭐가 문제냐! 라고 한 판 한 적이 있다는 이야기를 들은 적이 있는데 레퍼런스는 못 찾겠다.

사실 이론적 근거가 없다 못해 이론적으로는 말이 안 되는 것 같은 문제들도 여럿 있다. 아마 대표적인 것이 loss 함수의 non-convex함일 것이다. 뉴럴넷의 loss 함수는 대체로 non-convex 하기 때문에 local minima가 global minima가 아니며 따라서 global minima가 아닌 엉뚱한 local minima에 빠질 가능성이 있다. 물론 이게 큰 문제는 아닐 거라는 직관은 있다(예컨대 뉴럴넷의 그 수많은 파라미터들에 대해서 minima가 발생하기는 쉽지 않다는 등의). 최근에는 그와 관련한 증명도 제안되기도 했지만 그런 증명이 있기 이전에도 사람들은 non-convex함이 큰 문제가 아닐 거라고 가정하며 써 왔고 또 좋은 퍼포먼스를 내는데는 큰 문제가 아니었다.

해석 가능성에 대해서도 마찬가지다. 물론 모형이 해석 가능해서 나쁠 것은 없다. 그렇지만 모형이 해석 가능한 것보다 좋은 성능을 내는 것이 먼저라고 생각하는 사람들이 딥 러닝을 쓰고 있는 것일 것이다. https://www.quora.com/How-important-is-interpretability-for-a-model-in-Machine-Learning

어쨌든 딥 러닝은 머신러닝 커뮤니티에서도 특히 모형의 성능이 가장 큰 근거가 되고 있는 영역이라고 볼 수 있을 것 같다. 그리고 딥 러닝은 그런 성능적 기대치에 걸맞는 성능을 보여주고 있다. 물론 딥 러닝이 지금보다 훨씬 더 나은 성능을 보여주기 위해선 breakthrough가 여럿 더 필요할 수 있다. 그런데 그런 상황에서도 뉴럴넷이 아닌 다른 알고리즘이 이미지 분류나 언어 모형 같은 과제에 대해서 뉴럴넷보다 나은 성능을 보여주기는 어려울 것이다. 힌튼의 표현을 빌리자면 딥 러닝의 핵심은 데이터 자체에서 과제에 적절한 특징 추출 방식을 학습하는 것이기에, 딥 러닝이 동작하기 시작하면 다른 알고리즘은 딥 러닝을 따라잡기 어렵다.
