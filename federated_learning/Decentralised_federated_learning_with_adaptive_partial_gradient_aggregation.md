# DECENTRALISED FEDERATED LEARNING WITH ADAPTIVE PARTIAL GRADIENT AGGREGATION

[paper link](https://ietresearch.onlinelibrary.wiley.com/doi/full/10.1049/trit.2020.0082)

### 문제

연합학습은 중앙집중형 학습방식의 문제를 탈피하고자 제안되었지만, 여전히 중앙 서버에서의 모델 aggregation으로 인해 학습에서 모델 업데이트 시 병목현상으로 인한 
큰 지연시간을 겪는다. 따라서 본 논문에는 중앙 서버에서의 모델 aggregation을 제거한 adaptive partial gradient aggregation을 제안한다.

### 방법

<p align="center"><img src="../resource/jiang2020decentralised_1.PNG"></p>

그림의 b에서처럼, 제안하는 방법은 각 device가 가지고 있는 모델을 서버로 전송하지 않고, 각각의 device로 전송한다.
즉, 모델의 일부를 각 device에서 담당하여 aggregation하고 재배포를 하는 방식으로, n등분의 모델을 각각 n개의 device가 담당하여 aggregation할 수 있다.

### 공헌

본 논문에서는 연합학습의 장애물 중 하나인 모델 업데이트시 서버의 병목으로 인한 네트워크 문제를 모델의 p2p방식에 기반한 부분 업데이트를 통해 해결하였다.

### 의견

제안하는 방법은 상당히 효과적이지만 p2p 네트워크는 불안정한 네트워크이기 때문에 각 round마다 노드의 입출이 발생할 수 있다.
이에 따른 실험을 진행한다면 더욱 좋은 논문이 될 것 같다.
