# SHARPNESS-AWARE MINIMIZATION FOR EFFICIENTLY IMPROVING GENERALIZATION

[paper link](https://arxiv.org/abs/2010.01412)

### 문제

training loss의 기울기가 모델의 일반화 성능을 보장하는 경향이 있다. 본 논문은 loss space의 flat minima를 찾는 것이 모델의 generalization 성능을
향상시킨다고 주장한다. 반대로 loss space의 gradient가 sharp할 수록 generalization성능은 떨어진다. 본 논문은 모델의 generalization을 위해
loss space의 flat minima를 찾는 방법 sharpness-aware minimization(SAM)을 제안한다.

### 방법

<img src="resource/foret2020sharpness_1.png">

위 수식은 본 논문에서 제안하는 알고리즘을 표현한 수식이다.
좌항의 데이터 D에 대한 loss는 구할 수 없기 때문에 D의 샘플 S에 대한 loss식으로 upper boundary를 구한다. 이때 찾고자 하는 값 w를 기준으로 ρ범위의
loss를 최대화 하는 식을 세운다. 즉, 현재의 loss 값에서 최대 높이에 해당하는 지점을 찾아 이동시킨다. 이후 우항의 값을 최소화 하는 task를 통해 flat한
loss space로 이동한다. 

<img src="resource/foret2020sharpness_2.png">

위 그림을 통해 직관적인 이해가 가능하다.
$W_{t}$에 해당하는 값을 ε에의해 좌측로 최대화(gradient ascent) 시킨후 $W_{adv}$에서 loss를 최소화시키는 기울기를 찾는다. 그리고 찾은 기울기로 
$W_{t}$를 이동시킨다. 

### 공헌

flat한 loss space를 찾는 SAM을 통해 model의 generalization 성능을 향상시켰다. 다양한 데이터셋(Cifar 10,100, Imagenet, Finetuning, SVHN F-MNIST, Noisy Cifar)에 대하여 일반화 성능을 검증하였다. 
loss의 sharpness와 generalization사이의 관계에 대한 고찰.

### 의견

loss space의 sharpness를 통해 test데이터의 generalization 성능을 향상시킬 수 있다는 점은 새롭다. 하지만 다른 weight space등을 활용한 방법들과
상충되지 않게 적용될 수 있을지 검증이 필요할 것 같다.

