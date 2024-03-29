
# 그 외, 소소한 생각들

이렇게 나열하니 무언가 대단한 가르침이나 격언인 것 같다. 실은 그저 내 경험을 간결하게 요약해보려는 시도일 뿐이다. 고작해야 $N = 1$일 뿐이다.

### The Bitter Lesson

http://www.incompleteideas.net/IncIdeas/BitterLesson.html (한국어 역: https://newsight.tistory.com/302)

혹시 읽어보지 않은 이들이 있다면 꼭 읽어보라고 권하고 싶다. The Bitter Lesson은 AI/ML을 통틀어 논한 것이지만 딥 러닝에 국한해서도 동일하게 적용되는 것처럼 보인다. 단순하고, 학습과 탐색에 기반하고, 더 큰 모델, 더 많은 데이터, 더 강력한 연산력에 기반한 방법이야말로 더 장기적으로 성공적이며, 더 유지보수하기 쉽다. 하나의 모델에 대해 수많은 튜닝을 하는 방법들이 등장하지만 장기적으로 의미 있는 도구는 그리 많지 않다. 우리가 생각하기에 좋은 방법처럼 느껴지는 것을 결합하거나 튜닝하기 위해 집착하는 것은 별로 좋지 않다. 혹은 의도적으로 그러지 않으려 시도하는 것도 가능할 것 같다.

### 언제나 큰 문제부터 찾기

모델이 잘 작동하지 않으면 보통 행여나 작은 디테일들, 소소한 하이퍼파라미터 등의 차이에서 기인한 것이 아닐까 추측하기 쉽다. 어쩌면 사람은 스스로 큰 실수를 저질렀을 것이라기보단 작은 디테일을 커버하지 않았다고 생각하고 싶어하는 것 같다. 모델이 예상대로 학습하지 않거나 작동하지 않는다면 언제나 큰 실수가 있지 않은지를 먼저 생각해야 한다.

### 데이터로 해결할 수 있는 것이라면 데이터가 가장 저렴할 수 있다

성능이 문제라면 작은 튜닝과 소소한 개선으로 점진적인 성능 향상을 꾀하기 전에 추가적인 데이터를 사용할 수 있는지를 먼저 고려하자. 기존 모델을 약간씩 개선하는 것보다는 새로운 문제를 푸는 것이 더 가치있을 수 있다.

### 단기적인 해결이 아닌 장기적으로 유용한 대안을

혹은 최소한 단기적인 해결이 장기적인 해결책에 방해가 되거나 자원의 낭비가 되지 않도록 고려해야 한다.

### 어쩌면 학습 기반 모델을 쓰는 것이 더 저렴하다

위의 생각과 연결되는 것이라고도 할 수 있겠다. 어떤 문제가 주어지고 그 문제를 휴리스틱이나 알고리즘으로 풀 수 있닥소 생각하면 으레 그쪽이 선호되기 마련이다. 혹은 이런 이야기가 격언처럼 돌아다니기도 한다. 예를 들면 휴리스틱을 사용하면 풀 수 있는 문제를 다들 학습 기반 모델로 풀려고 하는 것이 문제다와 같은 식으로. 그러나 이것은 이 문제가 단발성으로 끝날 때에 한정된 것이다. 앞으로 문제의 요구 사항이 늘어난다면, 더 나아가 그 요구사항이 휴리스틱으로 커버하기 어려운 것이라면 휴리스틱보다는 학습 기반 모델이 더 명료하고 더 유지보수하기 쉬울 수 있다. 따라서 앞으로 어떤 예외와 요구사항과 코너 케이스가 발생할 수 있는가에 대해 고려해야 한다.

### 전체 도메인에서 쉬운 일부 케이스로 국한하는 것을 조심할 것

전체 문제나 도메인을 모두 포괄하는 것은 까다로운 일이고, 그 문제를 조금 축소한다면 난이도가 훨씬 쉬워지는 경우가 많다. 대강 대체 이런 케이스까지 커버할 필요가 있겠어라고 생각하고 문제를 좀 더 쉽게 풀고자 하는 것은 강력한 유혹이다. 그러나 그 코너 케이스가 장기적으로 중요한 문제가 될 수 있다는 것을 고려해야 한다. 오히려 더 광범위하고 더 넓은 문제, 도메인에 적용될 가능성을 생각해보는 것 또한 의미가 있다.

### 모델과 사랑에 빠지지 말 것

내가 선호하는 방법, 만들어놓은 모델에 집착하지 말 것. 가장 효율적이고 효과적인 방법과 모델을 우선할 것. 각자의 모델들이 경쟁하는 상황을 경계하고 모두의 작업과 개선물들이 반영될 수 있는 형태로 작업할 수 있도록 협업을 설계할 것.

### 다른 이들에게 필요한 것을 공개할 것

사람들은 왕왕 자신에게 필요한 요청 사항들에 대해서는 공개적으로 발언하면서 다른 이들에게 유용하거나 필요한 정보들에 대해서는 공개하지 않는 경우가 있다. 구체적으로는 업무적 진행 사항들과 의사 결정에 대한 정보가 공유되지 않는 것이다. 업무가 사적이거나 1대 1 의사소통만으로 진행되거나 혹은 개인적인 판단만으로 중요한 결정이 진행될 수도 있다.

다만 다른 사람들에게 필요한 정보를 먼저 공유하는 것은 상당히 어색한 일이다. 이건 HCI 실험 등에서 사용되는 Think Aloud (https://en.wikipedia.org/wiki/Think_aloud_protocol) 처럼 생각해볼 수도 있을 것 같다. 즉 작업을 진행하면서 떠오르는 생각, 추측들, 의사결정들을 생각으로 그치는 것이 아니라 직접 발언하는 것이다.