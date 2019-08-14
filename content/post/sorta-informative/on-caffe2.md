+++
autoThumbnailImage = true
categories = ["sorta informative"]
coverImage = "http://res.cloudinary.com/rosinality/image/upload/v1492734059/covers/coffee"
coverSize = "partial"
date = "2017-04-25T15:28:52+09:00"
hasMath = false
isCJKLanguage = true
keywords = ["caffe2", "pytorch", "deep learning frameworks"]
tags = ["caffe2", "pytorch", "deep learning frameworks"]
thumbnailImagePosition = "top"
title = "Caffe2에 대해"

+++

PyTorch랑 장기적으로 백엔드를 통합한다니까 관심이 생겨서 Caffe2를 좀 들여다봤음. Caffe를 써본 적은 없음. protocol buffer 파일을 만들어서 돌린다는 것만 아는 정도? 가장 먼저 써봤던 프레임워크는 Torch였고 그 이후에 TensorFlow가 나와서 그걸 써왔기 때문에...

보니까 Caffe와 동일하게 Caffe2도 파이썬 라이브러리는 protocol buffer를 생성하기 위한 라이브러리임. 물론 텐서플로와 같은 경우에도 파이썬은 거의 그래프를 만들기 위한 것이기 때문에 비슷하다고 할 수 있을 것 같긴 한데. 어쨌든 파이썬으로 protobuf를 생성하고(문자열로 찍어볼 수도 있음) 그걸 C++로 만들어진 백엔드에 입력해서 실제 실행은 백엔드에서 돌아가는 구조. 이런 형태의 정적 그래프를 쓰는 프레임워크들의 본래 목표이자 특징이기도 하지만 입력이 정해진 형식의 그래프로 한정되어 있기 때문에 최적화와 분산 처리가 쉽고(쉽다고 할 수 있고) 입력은 protobuf로 제한되어 있으니 파이썬으로 인한 오버헤드를 제거할 수 있다는 것이 장점일 것.

이런 구조라는 걸 보니까 PyTorch하고 통합하는 것도 생각보다 매끄러울 수 있겠다는 생각도 듦. PyTorch로 디버깅, 테스팅하고 그래프를 정적으로 고정하고 나면 그걸 protobuf로 번역해서 Caffe2 백엔드로 넘겨 트레이닝하거나 배포하는 것도 가능할 듯. 좀 더 interop이 잘 되면 텐서를 공유하면서 동적인 처리는 PyTorch에서 한다거나 하는 것도 가능할 것 같음.

약간 두 가지를 잘 하는 도구 하나보다는 한 가지를 잘 하는 도구 두 개가 낫다는 발상이긴 함. 물론 두 접근 다 장단점이 있긴 하지만. 어쨌든 PyTorch에 빠진 입장에서는 Caffe2가 PyTorch로 만든 모델을 배포할 수 있는 도구가 될 수 있다면 긍정적이라고 봄.

여담이지만 PyTorch/Caffe2나 TensorFlow를 보면 구글과 페이스북의 개발 스타일의 차이가 좀 드러나는 것이 아닌가 하는 생각도 함.