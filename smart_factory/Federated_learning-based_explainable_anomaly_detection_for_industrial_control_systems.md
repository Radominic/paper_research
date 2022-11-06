# FEDERATED LEARNING-BASED EXPLAINABLE ANOMALY DETECTION FOR INDUSTRIAL CONTROL SYSTEMS

[paper link](https://ieeexplore.ieee.org/abstract/document/9770834)

### 문제

IoT기반 스마트팩토리들은 수많은 보안 위협을 받는 산업 중 하나이다.
이에 분산 이상탐지 시스템 아키텍쳐들은 높은 탐지 퍼포먼스와 새로운 데이터 페턴에 대해 빠르게 학습하고, 
IoT 환경에 맞게 경량화 되어야 한다. 기존의 이상탐지를 위한 대부분의 솔루션은 이러한 요구사항들을 충족시키지 못했다.
또한, 이상발생의 이유에 대한 해석 가능성은 거의 고려되지 않았다.
본 논문에서는 연합학습 및 Variational autoencorder(VAE)를 기반으로 하는
Federated learning-based Explainable Anomaly Detection(FedEX) 아키텍처를 제안하여 이러한 문제들을 해결한다.

### 방법

<p align="center"><img src="../resource/huong2022federated_1.png"></p>

본 논문에서 제안하는 FedeX의 구조는 일반적인 연합학습의 구조를 따른다.

<p align="center"><img src="../resource/huong2022federated_2.png"></p>

FedeX는 입력으로 받는 데이터에 대해 VAE를 통해 representation을 학습한다. 일반적인 VAE기반 anomaly detection 모델에서와 같이
이상 데이터에 대해서는 정상 데이터의 representation과 비교하여 SVDD 분류기를 통해 분류한다.
또한 이상치에 대한 설명을 위해 입력데이터와 VAE모델의 representation정보를 통해 KernelSHAP를 사용하여 입력데이터의 영향을 확인할 수 있다.
SHapley Additive exPlanations(SHAP)는 데이터의 조합에 대한 실험을 통해, 각 변수들이 미치는 영향도를 확인하는 기법이다.

### 공헌

스마트팩토리에서 중요한 이상탐지 task를 위해 설명가능한 AI를 도입하여 문제를 해결하였다.

### 의견

실제 스마트팩토리에서 발생하는 데이터들이 다변량 데이터인지에 따라 활용여부가 결정된다. 변수가 적을수록 영향도 파악이 쉽기 때문에
SHAP를 위한 추가적인 cost가 필요하지 않다. VAE의 경우 단순한 네트워크를 사용하였다고 하지만 복잡도와 성능간에는 trade-off 가 있을 것이며,
네트워크의 크기가 커진다면 IoT환경에 적합하지 않을 수 있다.
