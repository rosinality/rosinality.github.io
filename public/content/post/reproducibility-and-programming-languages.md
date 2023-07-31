+++
categories = ["thoughts"]
date = "2017-04-21T01:18:21+09:00"
hasMath = false
isCJKLanguage = true
tags = ["reproducibility", "programming languages", "pipeline", "data analysis"]
title = "프로그래밍 언어와 재현 가능성"
coverImage = "http://res.cloudinary.com/rosinality/image/upload/v1492734059/covers/pipeline.jpg"
coverSize = "partial"
autoThumbnailImage = true
thumbnailImagePosition = "left"

+++

SPSS와 같은 GUI가 아니라 R과 같은 프로그래밍 언어를 써야 하는 이유가 있는가? (물론 SPSS도 프로그래밍이 가능한 것으로 알고 있다) 라고 하면, 물론 프로그래밍 언어를 사용함으로써 가능한 유연성 같은 것도 큰 장점이라고 하겠지만, 더 중요한 장점 중 하나는 연구 결과의 재현 가능성이 아닌가 한다. 스크립트로 만들어진 데이터 파이프라인과 분석 코드는 그 자체로 결과를 누구나 재현할 수 있는 수단이 된다. 만약 GUI 툴을 사용한다면? 연구 결과를 재현하기 위해서는 엑셀로 이 셀과 이 셀을 갖다 붙이고 이 셀을 이렇게 정리한 다음 GUI 툴로 불러들여서 이 컬럼과 저 컬럼을 가지고 어떤 분석을 사용하는데 옵션은 어떠어떠한 것을 켜야 한다는 식의 장황한 매뉴얼을 작성해야 할 것이다. 이래서는 재현하기 위한 매뉴얼을 작성하기도 어렵고 그걸 따라하기도 쉽지 않다.

그리고 재현 가능성이 낮다는 건 사용자 자신도 실수하기 쉽다는 것과 마찬가지다. 스크립트라면 매번 똑같은 분석을 반복하는 것도 어려운 일이 아니지만 GUI 사용은 인간이 반복 작업을 해야 하니 실수가 끼어들기도 쉽고, 뭔가를 바꿨다고 하면 바꾼 부분이 무엇이고 바꾼 부분으로 인해 그 이후 분석 과정과 결과가 어떻게 달라질 수 있는지 추적하기도 쉽지 않다.

그러니까 한 번, 혹은 몇 번 해보고 버릴 것이 아니라면 프로그래밍 언어를 쓰는 것이, 특히 데이터 전처리부터 데이터 탐색, 분석, 분석 결과에 대한 사후분석까지 순차적인 스크립트의 실행으로 끝낼 수 있는 파이프라인을 만드는 것이 이상적이긴 하다. 아 물론 완성하고 쓸 때까지는 무지무지 귀찮은 작업이긴 하지만...