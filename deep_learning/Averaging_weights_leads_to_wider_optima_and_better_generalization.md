# Averaging weights leads to wider optima and better generalization
[paper link](https://arxiv.org/abs/1803.05407)

### 문제

기존의 Fast Geometric Ensembling(FGE)는 weight space의 인접한 local minima를 앙상블 하는 기법을 제안하였다.
FGE는 model space에서의 앙상블보다 weight space에서의 앙상블이 더 유효하다는 것을 시사한다.
FGE는 일정 주기마다 learning rate를 키우는 piecewise linear cyclical learning rate기법을 사용한다.
본 논문의 저자는 기존의 시간축으로 모델을 앙상블하는 방법에서 여러개의 모델을 저장하는 것이 아닌(FGE의 local minima)
모델의 weight를 누적(running average)시켜 나가는 Stochastic Weight Averaging(SWA)를 제안한다.


### 방법

SWA는 모델학습의 cycle length마다 현재 시점의 모델 weight를 누적하여 업데이트한다. 

### 공헌

기존의 n개의 weight에 해당하는 모델을 저장하고 n번의 추론을 통해 앙상블을 하는 방법과 달리,
SWA는 누적된 하나의 모델만을 사용하므로 communication overhead가 거의 존재하지 않는다.
또한 SWA의 누적연산에는 시간과 메모리 cost가 매우 적다.

### 의견

기존의 FGE의 weight space averaging을 살리고, 시간 및 연산에서 효율적인 방법으로 개선한 점이 장점.
