# ANORMALY DETECTION IN TIME SERIES WITH ROBUST VARIATIONAL QUASI-RECURRENT AUTOENCODERS

[paper link](https://ieeexplore.ieee.org/abstract/document/9835268?casa_token=qM7YMrxC3nwAAAAA:u612PIVhZ7OSH9BlkP3-b3oqpe8URi_QleplMr7NEo13RkpiJ0BHZi4XLC6RqqpABlQpMqRxlzo)

### 문제

본 논문에서는 time series unsupervised 데이터에서 anormaly를 효과적으로 탐지하기 위한 variational quasi-recurrent autoencorders(VQRAE)를 제안한다.

<p align="center"><img src="kieu2022anomaly_1.png"></p>

기존의 unsupervised 데이터를 학습하기 위한 방법에는 autoencorder(AE)가 있다. autoencorder는 bottleneck 형태의 네트워크 layer를 통해 데이터를 압축하고
다시 복원하는 과정에서 데이터의 특성(latent variable)을 학습하는 것을 목표로 한다. autoencorder는 데이터의 특성을 학습하는 encording 네트워크를
학습하기 위해 decording과정을 연결하여 데이터를 복원한다.

<p align="center"><img src="kieu2022anomaly_2.png"></p>

variational autoencorder(VAE)는 마찬가지로 encorder와 decorder로 구성되어 있지만 데이터의 분포를 학습해
데이터를 새롭게 생산할 수 있는 decording 네트워크를 학습하기 위해 encording과정을 연결한다.
VAE에서는 encorder가 데이터를 통해 latent variable을 학습할 때 가우시안 분포로 가정된 평균과 표준편차를 생성한다.
이때 표준편차에 평균0, 표준편차 1의 가우시안 분포로부터 샘플링된 값을 곱해주고 이를 encorder의 아웃풋 평균과 더해 decorder로 입력한다.
decorder에서는 가우시안 분포의 샘플링 노이즈를 포함한 이 값을 원래의 데이터로 복원하도록 학습한다.
backpropagation과정에서 미분 가능하도록 reparameterization trick을 사용 z = μ + σ * sample(N(0,1)).
추론단계에서는 decorder만을 사용.

recurrent autoencorder(RAE)는 ffn을 사용한 AE와 달리 sequence data에서 temporal dependency를 학습하기 위해 rnn을 사용하였다.

<p align="center"><img src="kieu2022anomaly_3.png"></p>

variational RAE(VRAE)는 time series데이터에서 anormaly detection을 위해 고안된 sota.
VRAE의 한계점으로 학습데이터에서는 anomaly를 제외하고 사용하고, recursive구조 때문에 computation cost가 높음, 구조적 문제로 bi-directional 학습 불가라는 단점이 있다.

본 논문에서 제안하는 variational quasi-recurrent autoencorders(VQRAE)는 학습데이터에 anomaly를 포함하여 fully unsupervised learning이며, 
non-recursive mechanism 및 bi-directional computation이 가능하다.

### 방법

<p align="center"><img src="kieu2022anomaly_4.png"></p>

VQRAE는 RAE와 달리 recurrent state(h)의 계산이 latent variable에 의존하지 않으며, 양 방향으로 존재해 매 시점에서 전체 input sequence 정보를 이용해
latent variable을 학습 가능하다. 논문에서 도입된 quasi-recurrent neural network는 t-1 및 t 시점의 정보만을 사용하기 때문에
recursive 구조에 대한 문제 해결(병렬 계산) 및 temporal dependency 학습이 가능하다.

encorder(qnet)에서 input sequence s를 통해 hidden state h를 계산하고, s와 h를 이용해 양방향 정보를 가지는 a를 계산, a를 이용해 latent representation z계산.
z에서 평균과 표준편차를 계산한다. 여기서는 가우시안 분포가 아니라 복잡한 분포를 학습하기 위해 non-linear mapping function을 사용한다.

decorder(pnet)에서는 h,z를 이용해 output s에 대한 representation을 생성한다.

### 공헌

temporal dependency를 고려하면서 non-recursive한 구조 고안. computational cost를 감소시키면서 bi-direction한 학습이 가능하다.
여기서 설명하지는 않았지만 robust한 objective function을 통해 fully unsupervised learning이 가능하다.

### 의견

본 연구는 실험에서도 다양한 분포의 anomaly데이터에 대해 robust한 성능을 보였기 때문에 아주 좋은 방법이라고 생각. 특히 quasi-rnn구조와 non-linear mapping 등
네트워크의 성능을 향상시킬 수 있는 다양한 구조를 도입하고 목적함수를 적절하게 사용했다.
