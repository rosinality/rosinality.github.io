+++
keywords = ["tel aviv", "eccv 2022", "machine learning"]
tags = ["tel aviv", "eccv 2022", "machine learning"]
categories = ["travel"]
isCJKLanguage = true
hasMath = false
coverImage = "https://res.cloudinary.com/rosinality/image/upload/v1667440604/tel-aviv/20221023_175224.jpg"
coverSize = "partial"
autoThumbnailImage = true
thumbnailImagePosition = "top"
date = 2022-11-04T17:51:06+09:00
title = "텔 아비브와 ECCV 2022 여행기 2"
+++

1. [텔 아비브와 ECCV 2022 여행기 1]( {{< ref "post/tel-aviv-1.md" >}})
2. 텔 아비브와 ECCV 2022 여행기 2
3. [텔 아비브와 ECCV 2022 여행기 3]( {{< ref "post/tel-aviv-3.md" >}})
4. [텔 아비브와 ECCV 2022 여행기 4]( {{< ref "post/tel-aviv-3.md" >}})
5. [텔 아비브와 ECCV 2022 여행기 5]( {{< ref "post/tel-aviv-5.md" >}})
6. [텔 아비브와 ECCV 2022 여행기 6]( {{< ref "post/tel-aviv-6.md" >}})
7. [텔 아비브와 ECCV 2022 여행기 7]( {{< ref "post/tel-aviv-7.md" >}})

<!--start-summary-->

![호텔 조식](https://res.cloudinary.com/rosinality/image/upload/c_scale,h_0.5/v1667528721/tel-aviv/20221023_075419.jpg)

호텔 조식. 첫 날은 빵만 종류별로 가져왔다.

이 날부터 ECCV 워크샵 & 튜토리얼이 있어서 참석했다.

![워크샵 가는 길 바닷가](https://res.cloudinary.com/rosinality/image/upload/c_scale,h_0.5/v1667528721/tel-aviv/20221023_090431.jpg)

워크샵은 본 학회와는 달리 다비드 인터컨티넨탈 호텔에서 열렸다. 꽤 걸리는 거리에 있긴 했는데 (50분 정도?) 호기롭게 걸어서 가보는 것에 도전했다. 호텔 가는 길에 해변이 쭉 이어져 있어서 가는 도중 서핑하는 이들을 꽤 볼 수 있었다.

![워크샵 가는 길 공사 현장](https://res.cloudinary.com/rosinality/image/upload/c_scale,h_0.5/v1667528721/tel-aviv/20221023_095054.jpg)

텔 아비브에서 신기했던 것 중 하나는 사방에서 공사를 하고 있다는 것과 새 건물과 낡은 건물이 같은 공간 같은 지점에 공존하고 있다는 것이었다. 끊임 없이 개발 중이라는 이야기를 들었다.

![워크샵 가는 길 호텔 앞 모스크](https://res.cloudinary.com/rosinality/image/upload/c_scale,h_0.5/v1667528721/tel-aviv/20221023_095057.jpg)

호텔 앞에는 모스크가 하나 있었다. 그리고 이런 기후 조건에서면 으레 볼 수 있는 야자 가로수.

![워크샵 가는 길 호텔 앞 모스크](https://res.cloudinary.com/rosinality/image/upload/c_scale,h_0.5/v1667528721/tel-aviv/20221023_095847.jpg)

ECCV 등록 현장. 등록 코너에서는 늘 그렇긴 하지만 여기서부터 인구 밀도가 범상치 않다.

처음 들어간 워크샵은 Computational Aspects of Deep Learning. 대체로 연산 최적화에 대한 주제였다.

![워크샵 1 - Quantization](https://res.cloudinary.com/rosinality/image/upload/c_scale,h_0.5/v1667528721/tel-aviv/20221023_102043.jpg)

Quantization에서 모델 weight에 허용하는 Degree of Freedom에 대한 주제.

![워크샵 2 - Binary Neural Network](https://res.cloudinary.com/rosinality/image/upload/c_scale,h_0.5/v1667528721/tel-aviv/20221023_104306.jpg)

Binary Neural Network를 위한 Quantization 방법에 대한 주제.

![워크샵 - 다과](https://res.cloudinary.com/rosinality/image/upload/c_scale,h_0.5/v1667528721/tel-aviv/20221023_105852-Edit.jpg)

모자이크기 너무 심했나? 호텔 공간을 빌려 사용하다보니 인구 밀도가 너무 높아서 어쩔 수 없었다. 역시 워크샵에서 남는 것은 쿠키 밖에 없다.

![워크샵 - Computer Vision in the Wild 1](https://res.cloudinary.com/rosinality/image/upload/c_scale,h_0.5/v1667528721/tel-aviv/20221023_112054.jpg)

ECCV 2022 워크샵의 특징 혹은 아쉬운 점 하나는 대부분의 워크샵이 버추얼로 진행됐다는 것. 굳이 워크샵 현장에 나오지 않아도 인터넷으로 스트리밍이 가능했다. 관심이 갔던 워크샵 중 하나인 Computer Vision in the Wild는 그래서 호텔 로비에 앉아서 들었다. 마침 찍힌 타이밍은 OWL-ViT([https://arxiv.org/abs/2205.06230](https://arxiv.org/abs/2205.06230))와 UViM([https://arxiv.org/abs/2205.10337](https://arxiv.org/abs/2205.10337)). OWL-ViT는 본 학회에서도 포스터 발표를 했다. OWL-ViT는 본 학회 파트에서 소개하도록 하고, UViM은 이전에 남긴 메모를 재활용하자면:

> 레이블을 vq-vae로 제한된 길이의 discrete code로 인코딩한 다음 이 코드와 이미지를 사용해 비전 과제를 수행하는 모델을 만들고, autoregressive 모델로 이미지에서 discrete code를 생성한 다음 이 코드를 사용하는 방식의 모델. 다양한 비전 과제를 동일한 구조로 통합했습니다. 오라클을 사용하는 접근이 이렇게 다시 등장하네요.

![워크샵 - Computer Vision in the Wild 2](https://res.cloudinary.com/rosinality/image/upload/c_scale,h_0.5/v1667528721/tel-aviv/20221023_113004.jpg)

웰빙 워크샵의 현장. 물론 여러 세션이 있었는데 기억에 남는 것은 Competition에서 언급된 요즘 Object Detection에는 DINO([https://arxiv.org/abs/2203.03605
](https://arxiv.org/abs/2203.03605
))가 깡패라는 이야기.

![점심 시간 공원](https://res.cloudinary.com/rosinality/image/upload/c_scale,h_0.5/v1667528721/tel-aviv/20221023_124221.jpg)

점심 시간. 호텔 바로 앞이 공원이라 거기서 먹었다. 사진도 안 찍었는데 학회에서 받은 고기 샌드위치 맛은 그냥 그랬다. 70 셰켈이었는데. (1 셰켈 = 대충 400 원 정도.)

![Flamingo 저자](https://res.cloudinary.com/rosinality/image/upload/c_scale,h_0.5/v1667528721/tel-aviv/20221023_163745.jpg)

오후 세션. Self Supervised Learning 워크샵에서 마지막에 Flamingo ([https://arxiv.org/abs/2204.14198](https://arxiv.org/abs/2204.14198)) 저자가 나와서 Contrastive Learning에서 Generative Learning으로 넘어가게된 경로를 소개했다. Contrastive Learning이 하기는 더 쉽지만 (더 구체적으로는 Contrast를 만드는 것이 쉽다라는 느낌) 다양한 활용 방식이라는 측면에서 Generative Model이 가지는 장점이 더 컸기 때문이었다고 했다.

![저녁 거리](https://res.cloudinary.com/rosinality/image/upload/c_scale,h_0.5/v1667528721/tel-aviv/20221023_174405.jpg)

![동네 골목, SUZANA](https://res.cloudinary.com/rosinality/image/upload/c_scale,h_0.5/v1667528721/tel-aviv/20221023_175216.jpg)

![SUZANA](https://res.cloudinary.com/rosinality/image/upload/c_scale,h_0.5/v1667528721/tel-aviv/20221023_175224.jpg)

ECCV에 참석하신 회사의 다른 분들을 만나 저녁을 같이 했다. SUZANA라는 레스토랑.

![SUZANA](https://res.cloudinary.com/rosinality/image/upload/c_scale,h_0.5/v1667528721/tel-aviv/20221023_182155.jpg)

내가 주문한 것은 Chicken fillet on burgul majadra. 굉장히 이국적인 이름에 (정확히 어떻게 발음하는지 모르겠다) 굉장히 이국적인 모양새지만 맛은 놀랍게도 그럭저럭 평범한 볶음밥 같은 것이 났다.

![Goldstar 맥주](https://res.cloudinary.com/rosinality/image/upload/c_scale,h_0.5/v1667528721/tel-aviv/20221023_184327.jpg)

어쩌다보니 이 맥주를 많이 마신 듯. 이스라엘 맥주인데 이름이 Goldstar다. 럭키 금성 아님.

![고양이의 존재감 1](https://res.cloudinary.com/rosinality/image/upload/c_scale,h_0.5/v1667528721/tel-aviv/20221023_183037.jpg)

![고양이의 존재감 2](https://res.cloudinary.com/rosinality/image/upload/c_scale,h_0.5/v1667528721/tel-aviv/20221023_183951.jpg)

![고양이의 존재감 3](https://res.cloudinary.com/rosinality/image/upload/c_scale,h_0.5/v1667528721/tel-aviv/20221023_183953_0.jpg)

하여간 이 동네 고양이들은 사람을 별로 무서워하지 않는다. 참석한 분 한 분의 가방 위에 올라가서 자리를 잡고 호시탐탐 음식을 노리던 고양이 하나. 테이블 밑으로도 아랑곳하지 않고 돌아다니는 고양이도 또 한 마리 있었다. 여기서 가방 위에 터를 잡고 있었던 고양이는 테이블 밑에서 기습한 고양이에게 일격을 맞고 달아났다.

![고양이 두 마리](https://res.cloudinary.com/rosinality/image/upload/c_scale,h_0.5/v1667528721/tel-aviv/20221023_184339.jpg)

![고양이 퇴치 물총](https://res.cloudinary.com/rosinality/image/upload/c_scale,h_0.5/v1667528721/tel-aviv/20221023_184553.jpg)

스태프에게 어떻게 할 수 없느냐고 하니 얼마 뒤에 (대체 왜 가지고 있는지 모르겠지만) 물총을 하나 가져왔다. 이 테이블 뿐만 아니라 주위 테이블 모두 터져버린 장면 하나.