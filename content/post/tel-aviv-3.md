+++
keywords = ["tel aviv", "eccv 2022", "machine learning"]
tags = ["tel aviv", "eccv 2022", "machine learning"]
categories = ["travel"]
isCJKLanguage = true
hasMath = false
coverImage = "https://res.cloudinary.com/rosinality/image/upload/v1667440604/tel-aviv/20221024_182236.jpg"
coverSize = "partial"
autoThumbnailImage = true
thumbnailImagePosition = "top"
date = 2022-11-07T11:49:04+09:00
title = "텔 아비브와 ECCV 2022 여행기 3"
+++

1. [텔 아비브와 ECCV 2022 여행기 1]( {{< ref "post/tel-aviv-1.md" >}})
2. [텔 아비브와 ECCV 2022 여행기 2]( {{< ref "post/tel-aviv-2.md" >}})
3. 텔 아비브와 ECCV 2022 여행기 3
4. [텔 아비브와 ECCV 2022 여행기 4]( {{< ref "post/tel-aviv-4.md" >}})
5. [텔 아비브와 ECCV 2022 여행기 5]( {{< ref "post/tel-aviv-5.md" >}})
6. [텔 아비브와 ECCV 2022 여행기 6]( {{< ref "post/tel-aviv-6.md" >}})
7. [텔 아비브와 ECCV 2022 여행기 7]( {{< ref "post/tel-aviv-7.md" >}})

<!--start-summary-->

![호텔 조식](https://res.cloudinary.com/rosinality/image/upload/c_scale,h_0.5/v1667528721/tel-aviv/20221024_073959.jpg)

다음 날. 조식 구성의 다양화를 꾀한 장면.

이 날은 대충 Text in Everything 워크샵에 계속 참석했다. ECCV에 온 이유 자체가 이 워크샵에서 챌린지 결과를 발표하기 위함이었으므로.

![Text in Everything](https://res.cloudinary.com/rosinality/image/upload/c_scale,h_0.5/v1667528721/tel-aviv/20221024_095329.jpg)

![Text Spotting Transformers](https://res.cloudinary.com/rosinality/image/upload/c_scale,h_0.5/v1667528721/tel-aviv/20221024_110413.jpg)

이 토크는 Text Spotting Transformers ([https://arxiv.org/abs/2204.01918](https://arxiv.org/abs/2204.01918))에 대한 소개였다. 저자들의 관심은 DETR 같은 프레임워크로 이미지에서 기하학적 대상들을 추출하는 것이었던 것 같다. 이전에는 라인 검출을 했었고 E2E Scene Text Spotting은 폴리곤에 적용해보려는 시도의 일환처럼 보이기도 했다. 대략 구성은 2 stage Deformable DETR 같은 느낌으로 박스를 추출한 다음 이 박스에서 컨트롤 포인트 쿼리를 만들고, 추가적인 컨트롤 포인트 쿼리 임베딩과 조합해서 폴리곤을 구성하는 컨트롤 포인트를 예측하는 디코더 하나, 문자 쿼리 임베딩과 조합해서 텍스트 시퀀스를 예측하는 디코더가 하나 있다. 이 두 디코더에 대해 예측한 박스를 레퍼런스 포인트로 입력한다는 느낌.

![SemiMTR](https://res.cloudinary.com/rosinality/image/upload/c_scale,h_0.5/v1667528721/tel-aviv/20221024_140739.jpg)

SemiMTR ([https://arxiv.org/abs/2205.03873](https://arxiv.org/abs/2205.03873)), Semi-supervised Learning 하나.

![TextTranSpotter 1](https://res.cloudinary.com/rosinality/image/upload/c_scale,h_0.5/v1667528721/tel-aviv/20221024_142937.jpg)

![TextTranSpotter 2](https://res.cloudinary.com/rosinality/image/upload/c_scale,h_0.5/v1667528721/tel-aviv/20221024_142959.jpg)

![TextTranSpotter 3](https://res.cloudinary.com/rosinality/image/upload/c_scale,h_0.5/v1667528721/tel-aviv/20221024_143145.jpg)

![TextTranSpotter 4](https://res.cloudinary.com/rosinality/image/upload/c_scale,h_0.5/v1667528721/tel-aviv/20221024_143237.jpg)

그 다음은 TextTranSpotter ([https://arxiv.org/abs/2202.05508](https://arxiv.org/abs/2202.05508)). 모티베이션인 OCR 데이터가 처음에는 문자 단위였다가 단어 단위 이미지 크롭으로 변화한 것처럼 점점 어노테이션의 단위가 커지고 있는데, 이 다음 단계는 이미지 레벨이 되어야하지 않겠느냐는 것. 즉 이미지와 (특별한 좌표 정보 없이) 이미지 내에 있는 텍스트의 페어가 있을 때 학습할 수 있는 것이 다음 단계라는 것이다. 그래서 텍스트 시퀀스를 포함한 매칭을 사용하는 모델을 고안했다는 흐름.

![OCR-IDL](https://res.cloudinary.com/rosinality/image/upload/c_scale,h_0.5/v1667528721/tel-aviv/20221024_150414.jpg)

다음 주제는 OCR-IDL ([https://arxiv.org/abs/2202.12985](https://arxiv.org/abs/2202.12985)) [IIT-CDIP](https://data.nist.gov/od/id/mds2-2531) 같은 좁은 도메인의 문서가 아니라 산업 현장의 더 넓은 도메인과 시간대의 문서에 대해서 데이터셋을 만들자는 아이디어. Amazon Textract로 텍스트 박스를 추출했다.

![Dessurt 1](https://res.cloudinary.com/rosinality/image/upload/c_scale,h_0.5/v1667528721/tel-aviv/20221024_151445.jpg)

![Dessurt 2](https://res.cloudinary.com/rosinality/image/upload/c_scale,h_0.5/v1667528721/tel-aviv/20221024_151728.jpg)

다음은 Dessurt. ([https://arxiv.org/abs/2203.16618](https://arxiv.org/abs/2203.16618)) 어떻게 보면 지금 OCR 업계의 가장 중요한 주제인 OCR 없이 이미지만 입력으로 받아 그 이미지에 대해서 정보를 추출할 수 있는 모델을 만들려는 시도 중 하나라고 할 수 있겠다. 지금 시점에는 Pix2Struct ([https://arxiv.org/abs/2210.03347](https://arxiv.org/abs/2210.03347))까지 나와있는데 Dessurt의 특징은 최대한 다양한 데이터 소스를 부족한 학습 리소스 내에서 효율적으로 사용하려고 노력했다는 것일 듯.

![Advancing Multimodal Vision-Language Learning](https://res.cloudinary.com/rosinality/image/upload/c_scale,h_0.5/v1667528721/tel-aviv/20221024_160424.jpg)

다음은 [Aishwarya Agrawal](https://www-labs.iro.umontreal.ca/~agrawal/)의 Vision-Language Learning에 대한 토크. OCR과는 약간 다른 주제이긴 했다. 주로 다룬 것은 Rethinking Evaluation Practices in Visual Question Answering: A Case Study on Out-of-Distribution Generalization ([https://arxiv.org/abs/2205.12191](https://arxiv.org/abs/2205.12191))이었다. 주요한 내용은 각 VQA 파인튜닝 데이터셋들에 대해 학습한 Discriminative/Generative 모델이 다른 데이터셋에 대해서 어떤 성능을 보여주는가에 대한 것이었다.

![oCLIP](https://res.cloudinary.com/rosinality/image/upload/c_scale,h_0.5/v1667528721/tel-aviv/20221024_170234.jpg)

다음으로는 챌린지 발표. 정작 우리 발표는 사진이 없고 바이트댄스의 oCLIP ([https://arxiv.org/abs/2203.03911](https://arxiv.org/abs/2203.03911))만 있다. 이 시점에서 시간이 늦기도 했고 (5시 정도?) 워크샵 현장이 상당히 좁고 공조도 별로 쾌적하지 않은데다 이산화탄소 누적이 느껴질 정도였기에 인원이 반 이하로 줄어든 상태이긴 했다. 그래서 나름 무수한 악수의 요청(?)을 기대했는데 반응은 좀 썰렁했다. 뭐 큰 상관은 없지만.

![Dizengoff Street 1](https://res.cloudinary.com/rosinality/image/upload/c_scale,h_0.5/v1667528721/tel-aviv/20221024_175451.jpg)

![Dizengoff Street 2](https://res.cloudinary.com/rosinality/image/upload/c_scale,h_0.5/v1667528721/tel-aviv/20221024_175454.jpg)

이 날은 또 다른 그룹과 저녁 약속이 있어서, 카멜 마켓(Carmel Market)과 디젠고프 거리(Dizengoff Street)을 지나 HaKosem이라는 팔라펠 가게로.

![HaKosem 1](https://res.cloudinary.com/rosinality/image/upload/c_scale,h_0.5/v1667528721/tel-aviv/20221024_182236.jpg)

샤와르마(Shawarma)를 주문했는데 약간 중동의 서브웨이라고 할 수 있을 듯. 주문하면 바로 만들면서 재료나 소스 추가에 대해 물어본다. 솔직히 전혀 모르는 상태라 일단 다 Yes, Yes로 일관. 주문 받는 분이 좀 까다로운 인상에다 까다로운 말투였는데 말투와는 별개로 챙길 것은 다 챙겨주는 스타일이었다. 아시안들이 동네 맛집이라고 찾아와서 헤메고 있는 모습이 조금 안타까웠는지.

![HaKosem 2](https://res.cloudinary.com/rosinality/image/upload/c_scale,h_0.5/v1667528721/tel-aviv/20221024_182307_01.jpg)

소스에 가려 안 보이지만 가장 위에 올라가 있는 것이 팔라펠. 구성은 팔라펠과 닭고기, 후무스 등. 옆에 있는 음료는 Ouzo Rimonade라고 석류 레모네이드라는데 정향 향 같은 것이 꽤 났다. 그래도 그럭저럭 마심. 샤와르마는 이스라엘에 있는 내내 먹은 것 중에서 현지 분위기가 나는 중에 가장 맛있었던 메뉴일 듯 싶다. (현지 분위기가 나는 걸 그렇게 골라 먹진 않았지만.) 거의 국민 음식이어서 그런지 샤와르마를 파는 가게는 거의 거리마다 하나씩 보인다.

그래서 샤와르마가 뭔가 하면 사실 아직도 잘은 모르겠다. 케밥하고 거의 같은 것 같기도 하고. 찾아보니 샤와르마와 케밥이 기원 논쟁을 하고 있는 것을 보니 아마도 명확한 기준을 가지고 구분하기는 좀 어려운 것일지도.