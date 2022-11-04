+++
keywords = ["machine learning", "ml pipeline", "configuration system"]
tags = ["machine learning", "ml pipeline", "configuration system"]
categories = ["sorta-informative"]
isCJKLanguage = true
hasMath = false
draft = false
coverImage = "https://res.cloudinary.com/rosinality/image/upload/v1618043855/config_ngnhlp.png"
coverSize = "partial"
autoThumbnailImage = true
thumbnailImagePosition = "top"
date = 2021-05-22T20:27:53+09:00
title = "머신 러닝 시스템에서 설정 관리하기"
+++

머신 러닝 코드, 특히 실험적 목적이 강한 코드에서 가장 중요한 문제 중 하나가 설정을 관리하는 것이라고 본다. 머신 러닝 모델에는 수많은 하이퍼파라미터가 존재하고 그 하이퍼파라미터 각각이 설정 항목이 된다. 그 외에 또한 설정이 필요한 데이터, 로깅, 평가 등 부수적인 항목들이 많이 추가된다. (예를 들어 detectron2에는 기본적으로 200개 가량의 설정 항목이 존재한다. https://github.com/facebookresearch/detectron2/blob/master/detectron2/config/defaults.py 여기에 개별 모델마다 설정이 추가된다.) 이 많은 설정 사항들을 어떻게 감당할만하게 관리할 것인가?

이 이하는 이 문제에 대해 개인적으로 탐색해봤던 시도들을 정리한 것이다. 물론 더 정석적이고 이상적인 방법(또한 더 뻥셔널한 방법)이 있을 것이다. 그런 방법이 있다면 알려주시면 좋겠다.

기본적으로는, 설정이 존재하지 않는 형태의 코드에서 시작해보자. 예를 들어 다음과 같은 식이다.

```python
optimizer = optim.Adam(model.parameters(), lr=3e-4) # Karpathy's learning rate
```

대충 돌아가는지 체크해보는 정도의 목적에는 이 정도로도 충분하다. 나는 대체로 첫 코드는 이런 식으로 만든다. 이 이후 learning rate를 조절해보고 싶다는 생각이 들 수 있다. 흔히 쓰이는 방법 중 하나는 명령행 인자를 추가하는 것이다.

```python
parser.add_argument('--lr', type=float, default=3e-4)
args = parser.parse_args()
optimizer = optim.Adam(model.parameters(), lr=args.lr)
```

실제로 많은 공개된 머신 러닝 코드가 이런 식으로 동작하고 있다. 어느 정도 수준까지는 쓸만하지만, 두 가지 문제가 있겠다.

1. 설정 인자의 수가 증가하면 감당하기 어렵다. 명령행 인자로 넘기기도 어렵고 이 과정에서 실수하지 않기도 어렵다.
2. 매 실험마다 사용한 인자의 내역을 남기고 관리하기 어렵다.

물론 이 두 문제는 쉘 스크립트를 만드는 것으로 해결할 수 있고, 이렇게 처리하고 있는 코드도 많다. 환경 변수를 쓰고 환경 변수를 기록하는 경우도 많이 있다. 다만 이 시점까지 왔다면 본격적인 설정 파일을 사용하는 좀 더 우아한 방법을 채택할 수 있겠다.

```python
# default.conf
training {
    lr: 3e-4
}

# train.py
optimizer = optim.Adam(model.parameters(), lr=conf.training.lr)
```

# 설정 파일

## 설정 포맷

설정 파일을 사용하는 것을 받아들인다고 할 때 한 가지 선택하게 되는 것은 대체 어떤 포맷을 사용하는 것이 이상적인가 하는 것일 것이다. 파이썬에서 쓰기 쉬운 포맷 중 인기 있는 포맷을 꼽아보자면 다음과 같을 것 같다.

1. INI
2. JSON
3. YAML
4. TOML

이들 중 머신 러닝 코드 베이스에서 가장 인기있는 것은 YAML일 듯 싶다. 단...개인적으로 YAML은 선호하지 않는다. 스펙이 지나치게 많은 문법 설탕을 포함하고 있고, 설정 파일 포맷에서 의미있는 들여쓰기를 사용한다는 것은 과도하고 실수를 유발하는 측면이 있다고 본다.

다른 선택지도 크게 좋지는 않은 것 같다. JSON은 주석을 지원하지 않고, TOML은 건전한 포맷이지만 머신 러닝 코드에서 발생하는 수준의 설정을 관리하기에는 지원하는 기능이 적다. INI는 더 말할 것도 없고. 또한 머신 러닝 코드에서는 위 설정 포맷들이 보통 지원하지 않지만 유용하거나 혹은 반드시 필요한 기능이 하나 있는데, 바로 설정 파일을 병합하는 것이다. 설정 파일 병합을 사용하면 기본적인 설정을 설정 파일로 기록하고 거기에 실험 혹은 모델 특정적으로 필요한 설정들을 추가하는 방식으로 설정을 관리할 수 있다.

detectron2의 예를 들면, R-CNN + FPN의 베이스 설정이 있고(https://github.com/facebookresearch/detectron2/blob/master/configs/Base-RCNN-FPN.yaml), 백본을 바꿔서 실험하는 경우에는 이 베이스 설정을 불러와 설정을 변경하는 방식(https://github.com/facebookresearch/detectron2/blob/master/configs/COCO-Detection/faster_rcnn_R_101_FPN_3x.yaml) 으로 되어있다. 이 접근을 사용하면 설정의 중복을 피할 수 있고 설정을 변경하는 과정에서 특정 설정 파일에서 변경한 내역을 다른 설정 파일에 적용하지 않아 발생하는 실수를 감소시킬 수 있다. (물론 베이스 설정의 변화가 다른 모든 설정에 파급된다는 이슈가 있지만, 보통 전자에 비해서는 덜 위험한 문제로 보인다.) 그래서 detectron2의 경우처럼 이러한 설정 병합을 YAML 위에 올려서 사용하는 경우가 많다.

위 선택지에 비해서는 인기가 없지만 나름 지명도가 있는 포맷들이 있다.

5. HOCON
6. JSONNET

여기서 내가 선호하는 것은 HOCON이다. 둘 다 설정 병합을 지원하고 substitution 같은 추가적인 기능을 지원한다. 다만 일반적으로 사용하기에는 HOCON이 좀 더 간결하다. HOCON의 설정 병합 방식은 한쪽 설정으로 다른 설정을 대체하는 것이 아니라 두 설정을 합치는 방식(공집합)이라 좀 문제가 되기는 하는데...어쨌든 편리성을 고려하면 감수할만하다고 생각한다.

## 설정 검증

설정 파일을 사용한다면 또 한 가지 중요한 부분이 설정이 제대로 되어있는지를 체크하는 장치가 필요하다는 것이다. 예를 들어 정수가 들어가야할 곳에 실수가 들어간다거나 설정 키 이름에 오타를 내서 설정이 실제로는 적용되지 않는다거나 하는 문제를 미연에 방지할 수 있는 프로세스가 필요한 것이다. 단순히 실행하다 잘못된 값이 들어가서 종료되는 형태의 문제라면 괜찮겠지만 머신 러닝 코드의 특성상 한참 돌다가 문제가 생긴다거나 혹은 문제가 생겼는지도 알 수 없는 상태에서 모델의 성능만 저하된다거나 하는 경우가 생기기 마련이다.

scala의 경우에는 PureConfig (https://github.com/pureconfig/pureconfig) 등이 이를 위한 인기있는 방법인 것 같다. 파이썬의 경우에도 Cereberus (https://docs.python-cerberus.org/en/stable/) 같은 도구가 있었지만, 최근 가장 인기있는 라이브러리는 파이썬에 추가된 타입 어노테이션을 적극적으로 활용하는 pydantic (https://pydantic-docs.helpmanual.io/)인 것 같다. pydantic은 원칙적으로 데이터 검증을 위한 라이브러리라기보다는 데이터 파싱을 위한 라이브러리이지만, 좀 더 강력한 데이터 제약 조건을 걸면 충분히 검증을 위해서도 사용할 수 있다.

예를 들어, Adam optimizer를 위한 다음과 같은 pydantic 모델을 만들 수 있다.

```python
class Adam(BaseConfig):
    lr: float = 0.001
    betas: Tuple[float, float] = (0.9, 0.999)
    eps: float = 1e-8
    weight_decay: float = 0
    amsgrad: StrictBool = False

    class Config:
        extra = "forbid"
```

위와 같은 모델을 사용해서 betas 대신 이름을 beta로 입력해서 betas 설정이 적용되지 않는다거나 하는 실수를 방지할 수 있다. 파이썬에서 타입 어노테이션이 인기를 얻으면서 이 방식 또한 점점 더 인기를 얻고 있는 것 같다. 다만 함수나 클래스 정의와 별개로 이런 스키마를 따로 정의한다는 것도 번거로운 일이다. 약간 더 작업을 해서 함수 및 클래스의 정의와 타입 어노테이션으로부터 pydantic 모델을 만들어주는 데코레이터를 정의해볼 수도 있겠다.

```python
@config_model(name="swin_transformer")
class SwinTransformer(nn.Module):
    def __init__(
        self,
        image_size: Tuple[StrictInt, StrictInt],
        n_class: StrictInt,
        depths: Tuple[StrictInt, StrictInt, StrictInt, StrictInt],
        dims: Tuple[StrictInt, StrictInt, StrictInt, StrictInt],
        dim_head: StrictInt,
        n_heads: Tuple[StrictInt, StrictInt, StrictInt, StrictInt],
        dim_ffs: Tuple[StrictInt, StrictInt, StrictInt, StrictInt],
        window_size: StrictInt,
        drop_ff: StrictFloat = 0.0,
        drop_attn: StrictFloat = 0.0,
        drop_path: StrictFloat = 0.0,
    ):
        ...
```

## 설정 분기

계속 Adam만 쓸 것이라면 상관이 없겠지만 optimizer를 바꿔보고 싶은 경우가 생길 수도 있다. optimizer 뿐만 아니라 백본을 바꿔본다거나 하는 경우는 흔히 등장할 것이다. 가장 기본적인 방법은 설정을 받아 if문으로 분기하는 것이다.

```python
if conf.optimizer == 'adam':
    optimizer = optim.Adam(model.parameters(), lr=conf.training.lr)

elif conf.optimizer == 'sgd':
    optimizer = optim.Adam(model.parameters(), lr=conf.training.lr)

else:
    ...
```

이것도 어느 정도는 쓸만한 방법이겠지만, 선택지의 수가 늘어나고 각 선택지마다 추가적인 설정을 요구한다면 문제는 복잡해진다.

```python
if conf.optimizer == 'adam':
    optimizer = optim.Adam(model.parameters(), lr=conf.training.lr, betas=conf.betas, weight_decay=conf.weight_decay)

elif conf.optimizer == 'sgd':
    optimizer = optim.Adam(model.parameters(), lr=conf.training.lr, momentum=conf.momentum, nesterov=conf.nesterov, weight_decay=conf.weight_decay)

elif conf.optimizer == 'rmsprop':
    optimizer = optim.Adam(model.parameters(), lr=conf.training.lr, momentum=conf.momentum, weight_decay=conf.weight_decay)

else:
    ...
```

설정의 숫자가 늘어나면서 각 설정 파라미터 사이의 혼동도 증가한다. momentum은 sgd를 위한 momentum인가 adam의 beta1을 momentum으로 표기한 것인가? rmsprop의 momentum과 sgd의 momentum은 이름이 같지만 이 둘을 같은 의미로 분류해도 되는 것일까? 설정에는 어떻게 설명해야 할까? `# momentum for sgd, rmsprop, ...`이라고 주석을 달야아 할까?

pydantic을 사용해서 다음과 같이 접근해볼 수 있다.

```python
class SGD(BaseConfig):
    type: StrictStr

    lr: float
    momentum: float = 0.0
    dampening: float = 0.0
    weight_decay: float = 0.0
    nesterov: StrictBool = False

    class Config:
        extra = "forbid"

    @validator("type")
    def check_type(cls, v):
        if v != "sgd":
            raise ValueError("Optimizer type not match for sgd")

        return v

    def make(self, params):
        return optim.SGD(params, lr=self.lr,
            momentum=self.momentum,
            dampening=self.dampening,
            weight_decay=self.weight_decay,
            nesterov=self.nesterov)

class Adam(BaseConfig):
    type: StrictStr

    lr: float = 0.001
    betas: Tuple[float, float] = (0.9, 0.999)
    eps: float = 1e-8
    weight_decay: float = 0
    amsgrad: StrictBool = False

    class Config:
        extra = "forbid"

    @validator("type")
    def check_type(cls, v):
        if v != "adam":
            raise ValueError("Optimizer type not match for adam")

        return v

    def make(self, params):
        return optim.Adam(params, lr=self.lr,
            betas=self.betas,
            eps=self.eps,
            weight_decay=self.weight_decay,
            amsgrad=self.amsgrad)

class Training(BaseConfig):
    optimizer: Union[SGD, Adam]

# default.conf
optimizer: {
    type: sgd
    momentum: 0.9
}

# train.py
conf = Training(**config)
optimizer = conf.optimizer.make(model.parameters())
```

타입 체크와 validation을 사용해서 개별 optimizer에 대한 설정을 격리하고 type이라는 설정 파라미터로 optimizer를 지정할 수 있게 되었다. 다만 이건 너무 복잡하지 않은가? 다른 방법으로 흔히 사용되는 것이 registry이다. detectron2, mmdet, fairseq 등에서 흔히 찾아볼 수 있다.

```python
@BACKBONE_REGISTRY.register()
def build_resnet_backbone(cfg, input_shape):
    ...
```

(https://github.com/facebookresearch/detectron2/blob/master/detectron2/modeling/backbone/resnet.py)

registry에 각 함수/클래스의 정의와 이름 사이의 매핑이 저장되기 때문에 config에 지정된 이름에 상응하는 객체를 registry에서 불러와 사용할 수 있다. 그런데 pydantic을 사용하는 접근 또한 이렇게 함수/클래스에 데코레이터를 사용하는 방식을 채택해봤으니, 여기에 registry 개념을 추가해서 스키마를 자동으로 생성하고 type 지정에 따라 해당하는 객체를 불러오는 방식으로 개선해볼 수 있겠다.

```python
def get_models(namespace):
    names = CONFIG_REGISTRY[namespace].keys()
    for i, name in enumerate(names):
        model = get_model(name, namespace)

        if i == 0:
            models = Union[model]

        else:
            models = Union[models, model]

    return models

# swin_transformer.py
@config_model(name="swin_transformer", namespace="model")
class SwinTransformer(nn.Module):
    def __init__(
        self,
        image_size: Tuple[StrictInt, StrictInt],
        n_class: StrictInt,
        depths: Tuple[StrictInt, StrictInt, StrictInt, StrictInt],
        dims: Tuple[StrictInt, StrictInt, StrictInt, StrictInt],
        dim_head: StrictInt,
        n_heads: Tuple[StrictInt, StrictInt, StrictInt, StrictInt],
        dim_ffs: Tuple[StrictInt, StrictInt, StrictInt, StrictInt],
        window_size: StrictInt,
        drop_ff: StrictFloat = 0.0,
        drop_attn: StrictFloat = 0.0,
        drop_path: StrictFloat = 0.0,
    ):
        ...

# config.py
import swin_transformer

Arch = get_models("model")

# default.conf
arch: {
    type: swin_transformer
    image_size: [224, 224],
    n_class: 1000
    depths: [2, 2, 18, 2]
    dims: [96, 192, 384, 768]
    dim_head: 32
    n_heads: [3, 6, 12, 24]
    dim_ffs: [384, 768, 1536, 3072] # dims * 4
    window_size: 7
    drop_path: 0.3
}

# train.py
model = conf.arch.make()
```

이런 형태의 접근을 취한 경우도 꽤 보인다. (좀 다르긴 하지만) 대표적으로는 thinc (https://thinc.ai) 의 접근이 이와 유사하다.

## 더 단순하고 유연하게

여기까지만 해도 꽤 쓸만한 수준이 된 것 같고 이런 방식을 채택해 성공적으로 사용되고 있는 프레임워크들이 있지만, 여전히 문제가 좀 있다. 어쨌든 데코레이터를 정의해놓아야 한다는 것도 나쁘지는 않지만 불편한 점이고, registry에 등록하려면 registry 데코레이터가 정의된 파일이 실행되어야 하기 때문에 개별 파일들을 모두 import 해야한다는 것이다. 따라서 __init__.py 등에 import를 해놓아야 한다는 것이 문제가 된다. 번거롭고 config 사용을 위해서 이러한 정의를 import 해야한다는 것이 실수를 유발하며, import 자체가 실행 시간에 오버헤드를 발생시킨다는 점이 거슬린다.

여기서 hydra (https://hydra.cc) 의 방법을 참고해볼 수 있겠다. hydra는 설정 대상이 되는 객체를 어노테이션 해서 등록해놓고 호출하는 대신 import 경로를 지정해서 설정을 불러오는 시점에 import하여 실행하는 방법을 취한다. (https://hydra.cc/docs/patterns/instantiate_objects/overview)

```python
# default.conf
arch: {
    type: models.swin_transformer.SwinTransformer
    image_size: [224, 224],
    n_class: 1000
    depths: [2, 2, 18, 2]
    dims: [96, 192, 384, 768]
    dim_head: 32
    n_heads: [3, 6, 12, 24]
    dim_ffs: [384, 768, 1536, 3072] # dims * 4
    window_size: 7
    drop_path: 0.3
}

# instance.py
class Instance(dict):
    @classmethod
    def __get_validators__(cls):
        yield cls.validate

    @classmethod
    def validate(cls, v):
        v_new = validate(v)
        instance = cls(v_new)

        return instance

    def make(self):
        return instantiate(self)

# config.py
class ImageNetConfig(BaseModel):
    arch: Instance
```

type에 import 경로를 지정해주면, 설정을 불러오는 시점에 대상 객체를 import 해서 객체의 타입 어노테이션을 사용해 설정 파일을 검증하고 객체를 생성하는 방식이다. 지금까지는 이 방법이 설정 파일을 관리하는 괜찮은 방법인 것 같다. 즉 hydra가 파이썬 환경에서는 가장 괜찮은 도구가 될 것 같다. 다만 Hydra는 YAML에 크게 의존해서 YAML을 선호하지 않는 입장에서는 비슷한 다른 도구를 쓰고 있다.

## 설정 주입하기

설정을 불러오는 것 뿐만 아니라 설정을 어떻게 개별 객체에 넘겨줄 것인가 또한 중요한 문제이다. 머신 러닝 모델을 만들다 보면 다음과 같은 상황이 흔히 발생한다.

```python
class MultiHeadedLocalAttention(nn.Module):
    def __init__(
        self, dim, n_head, dim_head, input_size, window_size, shift, dropout=0
    ):
        ...

class PositionwiseFeedForward(nn.Sequential):
    def __init__(self, in_dim, dim=None, out_dim=None, activation=nn.SiLU, dropout=0):
        ...

class TransformerLayer(nn.Module):
    def __init__(
        self,
        dim,
        n_head,
        dim_head,
        dim_ff,
        input_size,
        window_size,
        shift,
        activation=nn.SiLU,
        drop_ff=0,
        drop_attn=0,
        drop_path=0,
    ):
        ...

class SwinTransformer(nn.Module):
    def __init__(
        self,
        image_size: Tuple[StrictInt, StrictInt],
        n_class: StrictInt,
        depths: Tuple[StrictInt, StrictInt, StrictInt, StrictInt],
        dims: Tuple[StrictInt, StrictInt, StrictInt, StrictInt],
        dim_head: StrictInt,
        n_heads: Tuple[StrictInt, StrictInt, StrictInt, StrictInt],
        dim_ffs: Tuple[StrictInt, StrictInt, StrictInt, StrictInt],
        window_size: StrictInt,
        drop_ff: StrictFloat = 0.0,
        drop_attn: StrictFloat = 0.0,
        drop_path: StrictFloat = 0.0,
    ):
        ...
```

개별 모듈들의 설정이 누적되어, 이 모듈들을 사용하는 상위 단계의 모듈들은 개별 모듈의 설정을 넘겨받아야 한다. 이것이 누적되면 인자의 수가 어마어마하게 증가한다. 예를 들어 torchvision의 Mask R-CNN 구현은 30개가 넘는 인자를 받는다. (https://github.com/pytorch/vision/blob/master/torchvision/models/detection/mask_rcnn.py) 결국에는 모든 세부 설정을 지정하는 것을 포기하고 중요한 설정 몇 가지만 설정 가능하게 만드는 방향으로 타협하는 경우도 많다.

이 문제에 대해 가장 흔히 쓰이는 방법은 conf 객체에 이 옵션들을 전부 몰아넣고 각 모듈들이 conf 객체만 인자로 받게 만드는 것이다.

```python
class MultiHeadedLocalAttention(nn.Module):
    def __init__(self, conf):
        ...

class PositionwiseFeedForward(nn.Sequential):
    def __init__(self, conf):
        ...

class TransformerLayer(nn.Module):
    def __init__(self, conf):
        ...

class SwinTransformer(nn.Module):
    def __init__(self, conf):
        ...
```

널리 쓰이긴 하지만 이 방법에는 중요한 문제가 있다. 개별 모듈에서 conf 객체의 어떤 항목을 사용하는지 확인하기 어렵고, 개별 모듈을 떼어내 사용하려면 conf 객체에서 사용하는 항목들을 찾아내 conf 객체를 만들어야만 한다.

이에 대한 대안으로 gin (https://github.com/google/gin-config) 과 같은 방법이 있다.

```python
@gin.configurable
class MultiHeadedLocalAttention(nn.Module):
    def __init__(
        self, dim, n_head, dim_head, input_size, window_size, shift, dropout=0
    ):
        ...

@gin.configurable
class PositionwiseFeedForward(nn.Sequential):
    def __init__(self, in_dim, dim=None, out_dim=None, activation=nn.SiLU, dropout=0):
        ...

@gin.configurable
class TransformerLayer(nn.Module):
    def __init__(
        self,
        dim,
        drop_path=0,
    ):
        ...

# train.py
gin.parse_config_file('default.gin')
```

이런 형태가 된다. gin으로 설정 파일을 불러오면 설정 파일의 항목들이 `gin.configurable` 데코레이터가 적용된 객체의 인자에 바인딩 된다. 즉 설정을 직접 넘겨주지 않아도 객체를 호출할 때 바인딩된 설정이 적용되는 것이다. 좋은 방법이지만 전역적으로 설정을 객체들에게 바인딩한다는 것이 썩 내키지 않았다. 너무 까다로운가? 그렇지만, 다른 방법이 없을까?

문제를 돌려서 생각하면, 하위 모듈들을 생성하기 위해 상위 모듈에서 하위 모듈의 인자를 모두 넘겨받는 것 자체가 적절하지 않은 것 같다. 상위 모듈이 하위 모듈을 생성하는 것이 아니라 하위 모듈을 넘겨받아 상위 모듈 내에서 활용하는 방식으로 바꿀 수 있지 않을까?

```python
class MultiHeadedLocalAttention(nn.Module):
    def __init__(
        self, dim, n_head, dim_head, input_size, window_size, shift, dropout=0
    ):
        ...

class PositionwiseFeedForward(nn.Sequential):
    def __init__(self, in_dim, dim=None, out_dim=None, activation=nn.SiLU, dropout=0):
        ...

class TransformerLayer(nn.Module):
    def __init__(self, attention, ff):
        ...

layer = TransformerLayer(MultiHeadedLocalAttention(...), PositionwiseFeedForward(...))
```

상위 모듈의 인자가 계속해서 증가하는 것을 회피할 수 있었다. 추가적으로 다양한 모듈을 선택할 수 있는 형태가 되었다. `MultiHeadedLocalAttention`이 아니라 `MultiHeadedAttention`을 인자로 넘겨주면 local attention이 아닌 global attention을 사용하는 형태로 모델을 전환할 수 있는 것이다.

그렇지만 여전히 어딘가에서는 설정을 사용해 모듈들을 생성해서 넘겨줘야 한다. 그리고 이러한 위계구조가 반복적으로 중첩될 수도 있다. 이 중첩된 구조와 설정 파일을 어떻게 연결할 수 있을까?

그런데 위에서 hydra의 사례를 보면 객체들을 특별한 registry 등록 없이도 생성하는 형태로 설정을 구조화할 수 있었다는 것을 볼 수 있었다. 그렇다면 설정 파일을 사용해서 개별 객체, 모듈들을 생성한 다음 상위 객체에 넘겨주는 방법은 어떨까? 재귀적으로 설정을 순회해서 이 과정을 자동화하는 것 또한 가능할 것이다.

```python
class Instance(dict):
    @classmethod
    def __get_validators__(cls):
        yield cls.validate

    @classmethod
    def validate(cls, v):
        v_new = instance_traverse(v, recursive=True)
        instance = cls(v_new)

        return instance

    def make(self):
        return instance_traverse(self, recursive=True, instantiate=True)
```

실제로 어떻게 순회해서 객체를 생성하는가 하는 부분은 길어서 생략했지만, 이런 접근을 사용하면 다음과 같은 형태의 설정이 가능하다.

```python
class Model(BaseModel):
    mlp: Instance

# default.conf

mlp: {
    __target: torch.nn.ModuleList
    __validate: false
    modules: [
        {
            __target: torch.nn.Linear
            in_features: 5
            out_features: 7
        },
        {
            __target: torch.nn.ReLU
        },
        {
            __target: torch.nn.ModuleList,
            __validate: false,
            modules: [
                {
                    __target: torch.nn.Linear,
                    in_features: 5,
                    out_features: 9,
                    bias: false
                },
                {
                    __target: torch.nn.SiLU
                }
            ]
        }
    ]
}

# train.py
model = Model(**config)
model.mlp.make()
```

생성된 객체는 다음과 같다.

```python
ModuleList(
  (0): Linear(in_features=5, out_features=7, bias=True)
  (1): ReLU()
  (2): ModuleList(
    (0): Linear(in_features=5, out_features=9, bias=False)
    (1): SiLU()
  )
)
```

결과적으로는 declarative하게 모델을 정의하는 형태가 되었다. 그렇다면 위 방법을 채택해 문제의 SwinTransformer를 정의해보겠다. 추가적으로 특정 모듈을 직접 생성해서 넘기는 대신 설정에 지정된 파라미터만 `functools.partial`로 바인딩하고 넘겨서 모듈에서 추가적인 인자를 넘겨주게 만들었다. 물론 설정에 지정된 파라미터에 대해서는 pydantic을 사용해 타입 체크와 검증을 수행한다.

```python
# swin_transformer.py
class MultiHeadedLocalAttention(nn.Module):
    def __init__(
        self, dim, n_head, dim_head, input_size, window_size, shift, dropout=0
    ):
        ...

class PositionwiseFeedForward(nn.Sequential):
    def __init__(self, in_dim, dim=None, out_dim=None, activation=nn.SiLU, dropout=0):
        ...

class TransformerLayer(nn.Module):
    def __init__(self, attention, ff):
        ...

class SwinTransformer(nn.Module):
    def __init__(
        self,
        image_size: Tuple[StrictInt, StrictInt],
        n_class: StrictInt,
        attention,
        ff,
        depths: Tuple[StrictInt, StrictInt, StrictInt, StrictInt],
        dims: Tuple[StrictInt, StrictInt, StrictInt, StrictInt],
        n_heads: Tuple[StrictInt, StrictInt, StrictInt, StrictInt],
        dim_ffs: Tuple[StrictInt, StrictInt, StrictInt, StrictInt],
        drop_path: StrictFloat = 0.0,
    ):

# default.conf
arch: {
    __target: models.swin_transformer.SwinTransformer
    attention: {
        __target: models.swin_transformer.MultiHeadedLocalAttention
        __partial: true
        dim_head: 32
        window_size: 7
        dropout: 0.0
    }
    ff: {
        __target: models.layer.PositionwiseFeedForward
        __partial: true,
        dropout: 0.0
        activation: {
            __target: torch.nn.SiLU,
            __partial: true
        }
    }
    image_size: [224, 224]
    n_class: 1000
    depths: [2, 2, 18, 2]
    dims: [96, 192, 384, 768]
    n_heads: [3, 6, 12, 24]
    dim_ffs: [384, 768, 1536, 3072]
    drop_path: 0.3
}

# train.py
swin = model.arch.make()
```

개별 모듈의 자잘한 설정은 `functools.partial`에 바인딩되어 상위 모듈로 넘어가고, 모듈 레벨이 아닌 모델 전체에 대해 적용되는 인자들은 따로 설정해서 바인딩된 함수에 넘겨줄 수 있게 만들었다.

여기까지가 단순하고 실수를 막는 설정 관리 방법을 찾으려는 시도의 결과이다. 더 나은 방법이 있을 것이고, 이 방법의 문제와 한계가 분명히 있을 것이다. 나 또한 더 나은 방법을 찾아보려 계속 시도하게 될 것이다. 다만 지금까지 탐색해왔던 방법에 대한 기록들이 비슷한 문제에 접근해보려는 이들에게 참고 사항 정도는 될 수 있기를 바란다.