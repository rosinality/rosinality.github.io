+++
keywords = ["tel aviv", "eccv 2022", "machine learning"]
tags = ["tel aviv", "eccv 2022", "machine learning"]
categories = ["travel"]
isCJKLanguage = true
hasMath = false
coverImage = "https://res.cloudinary.com/rosinality/image/upload/v1667440604/tel-aviv/20221026_225913.jpg"
coverSize = "partial"
autoThumbnailImage = true
thumbnailImagePosition = "top"
date = 2022-11-07T16:16:11+09:00
title = "텔 아비브와 ECCV 2022 여행기 5"
+++

1. [텔 아비브와 ECCV 2022 여행기 1]( {{< ref "post/tel-aviv-1.md" >}})
2. [텔 아비브와 ECCV 2022 여행기 2]( {{< ref "post/tel-aviv-2.md" >}})
3. [텔 아비브와 ECCV 2022 여행기 3]( {{< ref "post/tel-aviv-3.md" >}})
4. [텔 아비브와 ECCV 2022 여행기 4]( {{< ref "post/tel-aviv-3.md" >}})
5. 텔 아비브와 ECCV 2022 여행기 5
6. [텔 아비브와 ECCV 2022 여행기 6]( {{< ref "post/tel-aviv-6.md" >}})
7. [텔 아비브와 ECCV 2022 여행기 7]( {{< ref "post/tel-aviv-7.md" >}})

<!--start-summary-->

![카푸치노](https://res.cloudinary.com/rosinality/image/upload/c_scale,h_0.5/v1667528721/tel-aviv/20221026_080253.jpg)

카푸치노와 함께한 아침.

![샥슈카와 크로아상](https://res.cloudinary.com/rosinality/image/upload/c_scale,h_0.5/v1667528721/tel-aviv/20221026_081426.jpg)

전혀 안 어울리는 조합이지만 샥슈카가 꽂혀서 이런 괴상한 짓도 해봤다.

![비가 온 텔 아비브 풍경 1](https://res.cloudinary.com/rosinality/image/upload/c_scale,h_0.5/v1667528721/tel-aviv/20221026_082935.jpg)

![비가 온 텔 아비브 풍경 2](https://res.cloudinary.com/rosinality/image/upload/c_scale,h_0.5/v1667528721/tel-aviv/20221026_083100.jpg)

![비가 온 텔 아비브 풍경 3](https://res.cloudinary.com/rosinality/image/upload/c_scale,h_0.5/v1667528721/tel-aviv/20221026_083103.jpg)

![비가 온 텔 아비브 풍경 4](https://res.cloudinary.com/rosinality/image/upload/c_scale,h_0.5/v1667528721/tel-aviv/20221026_092849.jpg)

![비가 온 텔 아비브 풍경 5](https://res.cloudinary.com/rosinality/image/upload/c_scale,h_0.5/v1667528721/tel-aviv/20221026_092853.jpg)

![비가 온 텔 아비브 풍경 6](https://res.cloudinary.com/rosinality/image/upload/c_scale,h_0.5/v1667528721/tel-aviv/20221026_092859.jpg)

이 날은 비가 왔다. 많이 내리지는 않을까 싶었는데 잠깐 내리다가 그쳤다.

![3D-Aware Indoor Scene Synthesis with Depth Priors 1](https://res.cloudinary.com/rosinality/image/upload/c_scale,h_0.5/v1667528721/tel-aviv/20221026_100017.jpg)

![3D-Aware Indoor Scene Synthesis with Depth Priors 2](https://res.cloudinary.com/rosinality/image/upload/c_scale,h_0.5/v1667528721/tel-aviv/20221026_100017.jpg)

[3D-Aware Indoor Scene Synthesis with Depth Priors](https://arxiv.org/abs/2202.08553). NeRF rendering에 의존하지 않고 3D 생성 모델 구성하기 1. 이쪽은 depth 정보를 활용하는 방향이다. generator에서 depth 또한 생성하게 만들고 discriminator에 depth 입력을 사용하고 또한 rgb에서 depth를 예측하게 만드는 방식. depth는 depth estimation으로 추출해서 사용하는 paired 세팅.

![Generative Multiplane Images: Making a 2D GAN 3D-Aware](https://res.cloudinary.com/rosinality/image/upload/c_scale,h_0.5/v1667528721/tel-aviv/20221026_101813.jpg)

[Generative Multiplane Images: Making a 2D GAN 3D-Aware](https://arxiv.org/abs/2207.10642). NeRF rendering에 의존하지 않고 3D 생성 모델 구성하기 1. 이쪽은 포스터 파트에서 소개.

![How stable are Transferability Metrics evaluations?](https://res.cloudinary.com/rosinality/image/upload/c_scale,h_0.5/v1667528721/tel-aviv/20221026_105433.jpg)

[How stable are Transferability Metrics evaluations?](https://arxiv.org/abs/2204.01403). 파인튜닝 없이 모델 weight 체크포인트의 성능 순위를 매기는 메트릭들에 대한 벤치마크. 포스터에서처럼 가장 좋은 소스 데이터셋/가장 좋은 아키텍처를 고르는 상황에 따라 더 나은 메트릭이 다르다고. 어제 나온 PACTrans에 대해서는 어떻게 평가하는지 물어봤더니 구글 리서치 내에서도 논문이 쏟아지는 상황이라 그런 연구가 있는지 모르는 상황에서 제출했다고 한다. 혹시 이후에 테스트해보지는 않았는지 물어봤는데 아직이라고. 구글 레벨에서도 더 나은 체크포인트를 파인튜닝 없이 찾아볼 수 있는 연산 효율성이 중요한 것인가 싶기도 하고, 또 다른 의미로는 더 나은 체크포인트를 찾으려고 한다는 것 자체가 흥미로운 부분이다 싶기도 하다.

![Generative Multiplane Images: Making a 2D GAN 3D-Aware](https://res.cloudinary.com/rosinality/image/upload/c_scale,h_0.5/v1667528721/tel-aviv/20221026_105656.jpg)

[Generative Multiplane Images: Making a 2D GAN 3D-Aware](https://arxiv.org/abs/2207.10642). 2D GAN에서 이미지 하나와 여러 장의 알파 채널 마스크를 생성하게 한 다음 알파 채널과 생성 이미지를 조합해서 multiplane 이미지를 만들고 이 이미지의 조합으로 렌더링된 이미지를 생성하는 3D 생성에 대한 접근. NeRF rendering을 거치지 않으니 샘플링 속도가 빠르다. 어쩐지 성능 스코어 언급이 없어서 물어보니 EG3D와도 경쟁력이 있다고 언급. 다만 논문 스코어를 찾아보니 FID 등이 좀 밀리긴 하는 듯.

![FurryGAN: High Quality Foreground-aware Image Synthesis](https://res.cloudinary.com/rosinality/image/upload/c_scale,h_0.5/v1667528721/tel-aviv/20221026_104759.jpg)

[FurryGAN: High Quality Foreground-aware Image Synthesis](https://arxiv.org/abs/2208.10422).

생성된 이미지의 배경을 바꿀 수 있는 쉬운 방법 -> foreground 객체에 대한 fine-grained mask를 확보하는 것. 결과적으로 alpha composite로 최종 결과물을 만들 수 있게 foreground, background, alpha mask를 잘 생성하도록 모델에 강조하는 것이 요점. salient object detection으로 풀면 어떤 결과가 나오는지 궁금했는데 시도해보지는 않았다고. 아마도 이 연구 쪽이 더 낫지 않을지?

![Vector Quantized Image-to-Image Translation](https://res.cloudinary.com/rosinality/image/upload/c_scale,h_0.5/v1667528721/tel-aviv/20221026_103711.jpg)

[Vector Quantized Image-to-Image Translation](https://arxiv.org/abs/2207.13286). style-content disentangle과 style/content 교차, consistency를 사용하는 image2image, 거기에 vq-vae content encoding을 사용. 오랜만에 보는 형태의 접근이었다. style-content disentanglement를 강제하는 방법에 대해 물어봤는데 여기서는 adain 사용과 consistency loss 사용으로 대처한 듯.

![Text2LIVE](https://res.cloudinary.com/rosinality/image/upload/c_scale,h_0.5/v1667528721/tel-aviv/20221026_105311.jpg)

[Text2LIVE](https://arxiv.org/abs/2204.02491). 원본 이미지 + 편집 레이어를 조합하는 식으로 이미지를 편집하는 방법. 원본 이미지와 편집 레이어에 대한 결합을 CLIP 임베딩으로 텍스트와 loss를 걸어 학습시키고, 편집 레이어는 그린 스크린 위에 올린 후 green screen 프롬프트를 추가한 CLIP 임베딩으로 학습. CLIP을 학습시키면서 그린 스크린 이미지도 많이 봐서 되는 것 같다고.

![Any-resolution Training for High-resolution Image Synthesis](https://res.cloudinary.com/rosinality/image/upload/c_scale,h_0.5/v1667528721/tel-aviv/20221026_111121.jpg)

[Any-resolution Training for High-resolution Image Synthesis](https://arxiv.org/abs/2204.07156). 여러 해상도의 이미지로 구성된 데이터셋을 집어넣어 학습해도 고해상도의 이미지를 생성할 수 있는 모델. 핵심은 패치를 크롭해서 real sample을 만들고 크롭 파라미터를 generator에 입력으로 주는 것. StyleGAN 3를 기반으로 했다기에 antialiasing에서 이슈가 생길만한 부분은 없었는가 물으니 특별히 문제는 없었다고 한다.

![FCAF3D: Fully Convolutional Anchor-Free 3D Object Detection](https://res.cloudinary.com/rosinality/image/upload/c_scale,h_0.5/v1667528721/tel-aviv/20221026_103948.jpg)

[FCAF3D: Fully Convolutional Anchor-Free 3D Object Detection](https://arxiv.org/abs/2112.00322). 포인트 클라우드에 대한 object detection. 포인트 클라우드에 대한 sparse convolution과 rotation parametrization이 주요 기여 포인트.

그 외 눈에 띄었던 포스터들.

![Robust Visual Tracking by Segmentation](https://res.cloudinary.com/rosinality/image/upload/c_scale,h_0.5/v1667528721/tel-aviv/20221026_104434.jpg)

![A Sketch Is Worth a Thousand Words: Image Retrieval with Text and Sketch](https://res.cloudinary.com/rosinality/image/upload/c_scale,h_0.5/v1667528721/tel-aviv/20221026_104506.jpg)

![Tracking Every Thing in the Wild](https://res.cloudinary.com/rosinality/image/upload/c_scale,h_0.5/v1667528721/tel-aviv/20221026_105859.jpg)

![Learning Local Implicit Fourier Representation for Image Warping](https://res.cloudinary.com/rosinality/image/upload/c_scale,h_0.5/v1667528721/tel-aviv/20221026_111745.jpg)

![학회 쿠키](https://res.cloudinary.com/rosinality/image/upload/c_scale,h_0.5/v1667528721/tel-aviv/20221026_110053.jpg)

간식으로 놓여있어서 하나 집어먹어 봤는데 짜기만 했다.

![학회 점심](https://res.cloudinary.com/rosinality/image/upload/c_scale,h_0.5/v1667528721/tel-aviv/20221026_122234.jpg)

점심으로 나온 것. 안에 채운 것은 생선살이다. 바닷가라서 그런지 해산물 요리가 많기도 했다. 프레첼처럼 이 메뉴도 학회 단골이었다.

![학회장 바깥 파라솔](https://res.cloudinary.com/rosinality/image/upload/c_scale,h_0.5/v1667528721/tel-aviv/20221026_135358.jpg)

점심 시간에 밖에 나와서 널부러져봄. 그런데 널부러져 있기엔 햇볕이 너무 뜨겁고 좋은 지점은 이미 다 선점한 사람들이 있었다.

![만난 한국인 연구자 1](https://res.cloudinary.com/rosinality/image/upload/c_scale,h_0.5/v1667528721/tel-aviv/20221026_132444.jpg)

![만난 한국인 연구자 2](https://res.cloudinary.com/rosinality/image/upload/c_scale,h_0.5/v1667528721/tel-aviv/20221026_132723.jpg)

이 햇볕을 배경으로 ordinal regression을 연구하는 분과 depth estimation을 연구하는 분을 만나 잠깐 이야기를 했다.

[EdgeViTs: Competing Light-weight CNNs on Mobile Devices with Vision Transformers](https://arxiv.org/abs/2205.03436)