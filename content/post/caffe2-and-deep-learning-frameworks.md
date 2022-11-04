+++
autoThumbnailImage = true
categories = ["thoughts"]
coverImage = "http://res.cloudinary.com/rosinality/image/upload/v1492734059/covers/caffe2"
coverSize = "partial"
date = "2017-04-25T15:23:34+09:00"
hasMath = false
isCJKLanguage = true
keywords = ["caffe2", "pytorch", "tensorflow", "deep learning frameworks", "open source"]
tags = ["caffe2", "pytorch", "tensorflow", "deep learning frameworks", "open source"]
thumbnailImagePosition = "left"
title = "Caffe2와 딥 러닝 프레임워크"

+++

몰랐는데 Caffe2도 페이스북 쪽에서 기여한 모양(https://caffe2.ai 밑에 Facebook Open Source라고 큼직하게 박혀 있음.) PyTorch가 있는데 Caffe2는 왜? 라는 생각이 들 수 있는데 https://www.reddit.com/…/n_facebook_releases_new_deep_lear…/ 여길 보면 PyTorch는 연구에, Caffe2는 배포에 집중하고 backend는 통합해서 연동할 수 있게 하려는 구상인 듯. 이런 걸 깔끔하게 하는 건 엄청나게 어려운 일이겠지만 어쨌든 두 프레임워크의 개발 풀이 커질 수 있는 방향이라는 측면에서는 긍정적이라고 생각함.

결과적으로 구글은 TensorFlow, 마소는 CNTK, 아마존은 MxNet, 페이스북은 PyTorch에 Caffe2를 갖게 됐음. 물론 자기들 클라우드를 팔기 위한 이유도 있겠지만 자기들이 주도권을 가지고 있는 프레임워크를 갖고 싶은 이유도 큰 것 같음.

글이 텐서플로를 공개한 이유 중 하나가 구글이 자기들의 MapReduce 구현을 묶어놨더니 하둡이 업계 표준이 되어버려서 하둡을 배운 직원을 고용해서 내부 프레임워크를 가르쳐야 했던 문제가 있었기 때문이라고 함. 반대로 생각해보면 텐서플로를 하둡처럼 업계 표준으로 만들고 그 프레임워크의 개발 주도권을 구글 자신이 갖는 것을 목표로 했다고도 할 수 있음. 아주 경계할 일이라고까지 생각하진 않지만 그렇다고 아주 바람직한 일도 아니라고 생각함.

Yoshua Bengio가 이전에 텐서플로에 대해서 제3자에게 기여해서 중립적인 오픈소스 프로젝트로 돌리는 게 낫지 않겠냐고 했다는데 이런 측면에 대한 우려가 있었을 것이라고 봄. (하나의 기업이 프레임워크에 대한 주도권을 쥐는 것에 대한 문제.) 요즘 텐서플로에 대한 PR에 대해서 말이 좀 나오는 걸 보면 그런 문제가 조금 드러난 것이라고 보임.

그런 측면에서 널리 쓰이는 중립적인 오픈소스 프레임워크가 나타나기 힘들다면(물론 일단 Theano를 빼고) 여러 프레임워크를 선택할 수 있는 선택지가 존재하는 것도 그런 잠재적인 문제에 대한 하나의 대안적 방법이지 않을까 싶음.