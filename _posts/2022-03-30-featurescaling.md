---
title: "feature scaling이란"
tags: study
---

작성자 : 최준영


# Feature Scaling

머신 러닝에 사용될 데이터셋들은 대부분 다양한 feature 들을 가지게 됩니다. 그리고 머신러닝 모델은 이 feature들의 패턴과 상관관계를 찾아 의사결정 또는 예측을 하게 됩니다. feature 들은 다양한 정보를 숫자 또는 문자열로 가지며 이 값들은 제각기 다른 단위, 범위를 가집니다. ex) 키(단위 : cm , 범위 : 0~200), 몸무게(단위 : kg, 범위 : 0~150), 재산(단위 : 원, 범위 : -1,000,000,000 ~ +1,000,000,000))

하지만 모델들은 이 숫자들이 무엇을 나타내는지, 단위는 무엇인지 모른채 이들의 패턴들을 분석해서 학습을 하게 됩니다. 그렇기 때문에 feature들이 제각기 다른 범위와 분포를 가지면 문제가 발생할 수 있습니다. 그래서 feature scaling을 통해 feature 들의 크기와 범위들을 조절해 줍니다. 주로 feature scailing에 사용되는 방법은 정규화(Normalizaion)과 표준화(Standardization)이 있고 이 포스팅은 이 둘에 대한 설명을 담고자 합니다.

## Feature Scaling을 왜 하나요?

본격적으로 시작하기 전에 feature scailing을 왜 하는지에 대해서 먼저 알아보도록 하겠습니다. 머신러닝 모델을 학습시키는데는 여러가지 방법(경사강하법 기반 알고리즘, 거리 기반 알고리즘,  트리 기반 알고리즘)들이 있습니다. 

#### 경사강하법(Gradient descent) 기반 알고리즘

linear regression, logistic regression, neural network 등 다양한 모델들이 경사 강하법을 사용해 모델을 학습 시킵니다. 
$$
\theta_{i} :=\theta_i-\eta \frac{\partial}{\partial\theta_i}J(\theta_0,\theta_1)=\theta_i-\eta(h_{\theta}(x)-y)x \qquad (for\quad i=1,2)
$$
여기서 우리는 feature들에 관한 손실함수에 대해 gradient를 구하고 손실함수를 줄이는 방향으로 파라미터들을 업데이트 하게 됩니다. gradient를 계산 하는 과정에서 미분을 하다보면 인풋 데이터 x에 대한 값들이 곱해지게 되는데 만약 이들이 scaling 되어 있지 않다면 학습 과정 중 문제가 발생할 수 있습니다.

#### 거리 기반 알고리즘

KNN, K-means, SVM 같은 경우는 feature들 사이의 거리를 계산해 이를 기반으로 similarity를 결정하고 모델을 학습시켜 나갑니다. 만약 feature들이 scaling이 되지 않은 상태로 키(단위 : cm , 범위 : 0~200), 재산(단위 : 원, 범위 : -1,000,000,000 ~ +1,000,000,000)의 feature를 가지고 있다고 합시다. 그리고 이들을 통해 euclidean distance 를 계산한다고 한다면 재산의 값이 similarity에 큰 영향을 줄 것이라고 예상할 수 있습니다. 그래서 이러한 모델들을 사용할 때 feature scaling을 꼭 해주어야 합니다.

#### 트리 기반 알고리즘

트리 기반 알고리즘들은 매번 노드에서 하나의 feature를 가지고 불순도(impurity)를 최소화 하는 방향으로 학습을 진행합니다. 매번 split을 할 때는 특정한 값을 기준으로 위 아래를 나누기 때문에 feature의 분포와 범위의 영향이 없다고 보아도 무방합니다.

## 정규화(Normalization)

정규화(Normalization)의 목표는 데이터의 모든 feature 들이 비슷한 scale을 가지도록 해주는 것이다. 정규화에는 여러가지 종류가 있지만 여기서는 많이 쓰는 몇 가지만 소개하고 넘어가겠습니다.

#### Min-Max normaliztaion

$$
X'=\frac{X-X_{min}}{X_{max}-X_{min}}
$$

min-max normalization을 진행하기 위해서는 각 feature에 대해 최댓값과 최소값을 찾습니다. 그리고 모든 데이터에 대해서 feature들의 최솟값을 빼고 이를 최댓값과 최솟값의 차이로 나누어줍니다. 최솟값은 0, 최댓값은 1로 변환되고 모든 feature들은 [0,1]의 범위를 가지게 됩니다. 

#### Mean normalization

$$
X'=\frac{X-\mu}{X_{max}-X_{min}}
$$

min-max normalization과 다른 점은 각 feature들에 최솟값을 빼주는 것이 아니라 평균을 빼주는 것입니다. 이 방법을 사용할 경우 값들은 -1과1사이의 값들을 가지고 데이터들의 평균도 0으로 이동하게 됩니다.

## 표준화(Standardization)

$$
X'=\frac{X-\mu}{\sigma}
$$

표준화는 데이터들의 feature들이 정규분포를 가진다는 가정에서 출발해 이들을 평균이 0이고 표준편차가 1 인 표준정규분포로 변환하는 과정입니다. 이 경우 X'의 값의 범위는 정규화처럼 특정한 범위에 속하지 않고 다양한 값들을 가질 수 있습니다. 

경우에 따라 표준편차를 나누는 과정을 빼고 평균만 0으로 옮기거나, 평균 이동 없이 scaling만 사용할 수 도 있습니다.

**여기서는 표준화라고 불렀지만 Z-score Normalization이라고도 하는 것 같습니다.**



## 정규화와 표준화 중 어떤 것을 사용해야 할까?

정규화는 데이터들이 정규분포를 따르지 않는다는 것을 알 때 사용하면 좋습니다. 또는 KNN처럼 데이터들이 정규분포를 따를 필요가 없는 알고리즘들을 사용할 때도 쓰인다고 합니다. 또 neural network에 인풋 데이터로 사진을 넣을 때 전처리 과정에서 사용한다고 합니다.

표준화는 데이터들이 정규분포를 따를 때 사용하면 좋고, 정규화와는 다르게 특정한 범위 안으로 모든 값들을 집어넣지 않기 때문에 특이값(outlier)들이 있을 때 사용하면 좋습니다. 특이값이 있음에도 불구하고 정규화를 사용한다면 특이값 이외의 나머지 값들의 구분이 어렵게 됩니다.



