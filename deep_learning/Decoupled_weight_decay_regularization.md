# Decoupled weight decay regularization
[paper link](https://arxiv.org/abs/1711.05101)

### 문제

본 논문은 adaptive gradient method인 adam의 성능이 SGD보다 떨어지는 상황에 대한 분석을 통해
adam이 general하게 좋은 성능을 낼 수 있는 방법을 제안한다. 자세하게, 
일반적으로 딥러닝 라이브러리에서 weight decay를 수행할 때 코드는 L2 regularization으로 구현이 되어있는데,
SGD의 경우 weight decay와 동일한 결과를 보이지만, adam의 경우 L2 regularization의 일반화(generalization) 
성능이 weight decay보다 하락한다. 이를 해결하기 위해 decoupled weight decay regularization을 제안한다.

### 방법

SGD의 경우 L2 regularization의 손실함수를 미분했을 때 weight decay와 동일하게 작동한다.
이때의 L2 regularization을 위한 파라미터 lambda는 learning rate에 의존적이다.
adam의 경우 L2 regularization의 손실함수를 미분했을 때 파라미터 크기에 따라 gradient를 조절하기 위한
adaptive변수가 존재하기 때문에 weight decay와 동일하지 않다. 
adaptive변수로 인해 파라미터 lambda의 decay rate가 더 작아진다고 한다.
즉, weight를 덜 줄이게 된다는 얘기인데 regularization의 주 목적은 weight를 줄여 입력변수에 대한 민감도를 줄여야 하기 때문에
weight의 크기를 줄이는것(일반화)가 중요하다.
adaptive변수가 스칼라x단위행렬일 경우 동일하게 되지만 불가능.
따라서 본 논문에서는 기존의 L2 regularization 식에 별도의 wieght decay 변수를 분리하여(decoupled) 추가한 adamW를 제안한다.

### 공헌

adaptive gradient method인 adam에서 decoupled weight를 추가하여 일반화 성능을 강화시킨 adamW를 제안하였다. 
기존 adam보다 좋은 성능을 보인다.
decoupled weight를 사용했기 때문에 learning rate와 weight decay 변수가 독립적으로 작용한다.

### 의견

딥러닝의 성능에 있어서 일반화 성능은 중요한 것 같다. 특히 단순히 좋은 성능의(더 잘 수렴하는) 모델보다는,
좋은 일반화 성능을 끌어내기 위한 연구가 많은 것 같다. 
