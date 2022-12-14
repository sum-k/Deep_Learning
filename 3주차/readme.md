# 3주차

신경망이 잘 작동하기 위한 실질적인 측면

머신러닝 문제 해결법

## ♥ Train/dev/test sets

- 적은 데이터(100 ~ 10000)의 경우, 60:20:20
- 큰 데이터(1,000,000)의 경우, 98:1:1
- 더 커지면 99.5:2.5:2.5 혹은 99.5:0.4:0.1

- Make sure devand test come from same distribution
- Not having a test set might be okay. (only dev set.)

⇒ 훈련, 개발, 테스트 세트를 설정하는 것은 반복을 더 빠르게 할 수 있도록 하며, 알고리즘의 편향과 분산을 더 효율적으로 측정할 수 있도록 한다.

⇒ 알고리즘을 개선하기 위해 효율적으로 선택된 방법!

## ♥ Bias/Variance

| Train set error | 1% | 15% | 15% | 0.5% |  |
| --- | --- | --- | --- | --- | --- |
| Dev set error | 11% | 16% | 30% | 1% |  |
| (human → 0%) | high variance | high bias | high variance & high bias |  low variance & low bias |  |
| (Bayes error → 15%) |  | low variance |  |  |  |

최소한 훈련 데이터에서 얼마나 알고리즘이 적합한지 감을 잡을 수 있다. : 편향 문제

훈련 세트 → 개발 세트 : 오차가 얼마나 커지는가? : 분산 문제

⇒ **베이즈 오차가 꽤 작고 훈련 세트와 개발 세트가 같은 확률 분포에서 왔다**는 가정 하에 이뤄짐

## ♥ Basic “recipe” for machine learning

1. **편향(bias) 문제 - 훈련 세트의 성능**
    - **Bigger network** : 더 많은 은닉 층(hidden layer) 혹은 은닉 유닛(hidden unit)을 갖는 네트워크 선택
    - **Train longer** : 더 오랜 시간 훈련 시키기
    - (**NN architecture search)** : 다른 발전된 최적화 알고리즘 사용하기
2. **분산(variance) 문제 - 개발 세트의 성능**
    - **More data** : 데이터를 더 얻는 것
    - **Regularization**
    - (**NN architecture search)**

⇒ 정규화(Regularization) 

약간의 편향-분산 트레이드오프가 있다.(편향 증가)

## ♥ Regularization

: 높은 분산으로 신경망이 데이터를 과대적합하는 문제가 의심될 때, 가장 처음 시도하는 방법 

더  많은 훈련 데이터를 얻는 것  → 많은 비용

정규화(Regularization) → 과대적합을 막고, 신경망의 분산을 줄이는 데 도움

### ex) Logistic regression

- 비용함수 J를 최소화는 것
- $J(w, b) = \frac{1}{m}\sum_{i=1}^mL(\hat{y}^{(i)}, y^{(i)}) + \frac{\lambda}{2m}||w||_2^2$
- 가중치 행렬이 너무 커지지 않도록 막기 위해 추가적인 항을 더해줌
- **L2 regularization** : $||w||_2^2 = \sum_{j=1}^{n_x}w_j^2=w^Tw$
- L1 regularization : $\frac{\lambda}{2m}\sum_{j=1}^{n_x}|w_j|=\frac{\lambda}{2m}||w||_1$ ⇒ w will be sparse(희소), w벡터 안에 0이 많아짐
- $\lambda$ : 정규화 매개변수(regularization parameter), 하이퍼파라미터

매개변수 w만 정규화하는 이유? 

→ 보통 매개변수 w는 꽤 높은 차원의 매개변수 벡터이기 때문에(b는 하나의 숫자)

→ 거의 모든 매개변수는 b가 아닌 w에 있기 때문에 마지막 항(b)를 넣어도 실질적인 차이는 없을 것

### ex) Neural Network

신경망에서 L2 규제 적용하기

- 비용함수 $J(w^{[1]}, b^{[1]}, … , w^{[L]}, b^{[L]}) = \frac{1}{m}\sum_{i=1}^mL(\hat y^{(i)}, y^{(i)}) + \frac{\lambda}{2m}\sum_{l=1}^L||w^{[l]}||_F^2$
- **Frobenius norm**(행렬의 원소 제곱의 합) : $||w^{[l]}||_F^2=\sum_{i=1}^{n^{[l]}}\sum_{j=1}^{n^{[l-1]}}(w_{ij}^{[l]})^2, \\ \\ w^{[l]} : (n^{[l]},n^{[l-1]})$, 은닉층 개수
- 가중치 행렬이 너무 커지지 않도록 막기 위해 추가적인 항(**Frobenius norm**)을 더해줌
- “weight decay” : 경사하강법을 수행할 때, 1보다 작은 값을 곱해주기 때문

## ♥ Why regularization reduces overfitting

정규화에서 $\lambda$를 크게 만들어 가중치 행렬 w를 0에 상당히 가깝게 설정할 수 있다.  

따라서 많은 은닉 유닛을 0에 가까운 값으로 설정해 은닉 유닛의 영향력을 줄인다.  

그런 경우에 더 간단하고 작은 신경망이 될 것이다.

- 은닉 유닛의 영향력을 0에 가깝게 줄이기
- 로지스틱 회귀에 가까운 네트워크 만들기
- 간단한 네트워크는 과대적합 문제가 덜 일어난다.

## ♥ Dropout regularization

## ♥ Understanding dropout

## ♥ Other regularization methods

## ♥Normalizing inputs

신경망의 훈련을 빠르게 할 수 있는 기법

1. 평균을 빼기(0으로 만들기)
    
    0의 평균을 갖게 될 때까지 훈련 세트를 이동하는 것
    
2. 분산을 정규화하기(1으로 만들기)

⇒ 비용함수는 평균적으로 대칭적인 모양을 갖게 되며, 어디서 시작하든 경사하강법을 사용해 최솟값으로 바로 갈 수 있다. (학습률이 높다)

입력 특성이 매우 다른 크기를 갖는다면, 그를 정규화하는 것이 중요하다.

정규화는 어떤 해도 가하지 않기 때문에 되도록 하는 것이 좋다.

## ♥ Vanishing/exploding gradients

매우 깊은 신경망을 훈련시키는 것의 문제 → 미분값 혹은 기울기가 아주 작아지거나 커질 수 있다.

(가중치 행렬이 1.5의 값) 깊은 신경망에서 L의 값이 크다면, y의 예측값도 매우 커질 것!

(0.5 의 값) y의 예측값이 매우 작아질 것!

- 가중치 $w^{[l]}$ 이 단위행렬보다 조금 더 크다면, 매우 깊은 네트워크의 경우 활성값은 폭발
- 가중치 $w^{[l]}$ 이 단위행렬보다 조금 작다면, 활성값은 감소

⇒ 깊은 신경망에서 활성값이나 경사가 L에 대한 함수로 기하급수적으로 증가하거나 감소한다면 값들이 아주 커지거나 작아져 훈련을 시키는 것이 어려워진다.

## ♥ Weight initialization for deep networks

```python
w = np.random.randn(shape) * np.sqrt(1/n^[l-1]) # tanh 활성화 함수
# ReLU 활성화 함수의 경우 np.sqrt(2/(n^[l-1]*n^[l]))
# 층 l은 해당 층의 각 유닛에 대해 n^[l-1]의 입력을 갖는다.
```

- 각각의 가중치 행렬 w를 1보다 너무 커지거나 작아지지 않게 설정해서 너무 빨리 폭발하거나 소실되지 않게 한다.
- z의 값이 너무 크거나 작아지지 않도록! $w_i$의 분산을 1/n으로 설정!
- 가중치 행렬의 초기화 분산에 대한 기본 값 제공

## ♥ Numerical approximation of gradients

깊은 네트워크를 훈련시킬 때 신경망을 더 빨리 훈련시키는 또 다른 기법 - 경사 검사

**경사의 계산을 수치적으로 근사하는 방법

- f가 $(\theta-\epsilon,\ \theta+\epsilon)$ 인 점에서 삼각형 계산
- 더 큰 삼각형에서 너비 분의 높이를 구하는 것이 $\theta$ 에서의 도함수를 근사하는 데 더 나은 값을 제공한다.
- 삼각형의 높이 $f(\theta+\epsilon)-f( \theta-\epsilon)$, 너비 $2\epsilon$
- $\frac{f(\theta+\epsilon)-f( \theta-\epsilon)}{2\epsilon}$ 값이 $g(\theta)$와 매우 가까워짐
- → $g(\theta)$ 가 함수 f의 올바른 도함수를 구현하고 있다.

- 도함수를 근사하기 위해 양 쪽의 차이를 이용하는 방법을 사용하면 올바른 구현!
- 이를 역전파의 경사 검사에서 사용한다면 한 쪽의 차이만을 계산하는 것보다 두 배는 느리게 실행된다. 하지만 훨씬 더 정확하기에 가치가 있다!

## ♥ Gradient checking

역전파를 구현할 때,, 역전파를 맞게 구현했는지 확인하는 데 도움을 준다.

시간을 절약하고, 역전파의 구현에 대한 버그를 찾는 데 도움

1. 매개변수 W, b 들을 하나의 큰 벡터 $\theta$로 바꾼다.
    1. 모든 W 행렬을 받아서 벡터로 바꾸고 모두 연결(concentrate)시킨다.
    2. 비용함수 J 를 W, b의 함수로 만드는 대신에 $\theta$의 함수가 되도록 한다.
    3. $J(w^{[1]}, b^{[1]}, … , w^{[L]}, b^{[L]}) = J(\theta)$
2. $dW^{[1]}, db^{[1]}$ … 의 매개변수를 큰 벡터 $d\theta$로 만든다.
    1. $\theta$와 같은 차원
    

Q. $d\theta$가 비용함수 $J(\theta)$의 기울기인가?

### ⇒ Gradient checking (Grad check)

 $J(\theta) = J(\theta_1, \theta_2, ...)$ 

for each i:

$d\theta_{approx}[i] = \frac{J(\theta_1, \theta_2, ... , \theta_{i+\epsilon},...)-J(\theta_1, \theta_2, ... , \theta_{i-\epsilon},...)}{2\epsilon} \\ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \approx  d\theta[i] = \frac{dJ}{d\theta_i}$

→ $d\theta_{approx} \approx  d\theta \ ?$

Check $\frac{||d\theta_{approx} - d\theta ||_2}{||d\theta_{approx}||_2+||d\theta||_2} \approx 10^{-7}, \ \ when \ \ \epsilon = 10^{-7}$
 

⇒ great! 

(유클리드 거리→ 원소 차이를 제곱한 것의 합의 제곱근)

너무 큰 원소가 있는 것은 아닌지 이중 확인 필요!

원소의 차이가 너무 크다면 버그가 있을 수도 있다.

$10^{-3}$  (→ wrong!) 보다 더 작은 값이 나오도록 하는 것이 좋다.

⇒ 신경망의 정전파, 역전파를 구현할 때 경사 검사에서 상대적으로 큰 값이 나온다면, 버그의 가능성을 의심해야 한다.

⇒ 디버깅의 과정을 거친 후 경사 검사에서 작은 값이 나온다면 구현에 대한 자신감을 가져랑

## ♥ Gradient checking implementation notes

- Don’t use in training – only to debug
    - 모든 $d\theta_{approx}[i]$ 값을 계산하는 것은 매우 느리다.
    - 디버깅할 때만 이 값을 계산하고 $d\theta$
     에 가까워지게 한다.
    - 이 과정이 끝나면 경사 검사를 중지하고 모든 반복마다 실행되지 않도록 한다.
- If algorithm fails grad check, look at components to try to identify bug.
    - $d\theta_{approx} \approx  d\theta \$ 
    이 성립하지 않을 경우 서로 다른 i에 대해 검사!
    - 버그의 위치를 알아내는 데 도움을 받을 수 있다.
- Remember regularization.
    - 정규화 항을 기억하기
    - 프로베니우스 규제
- Doesn’t work with dropout.
    - 모든 반복마다 dropout은 은닉 유닛의 서로 다른 부분집합을 무작위로 삭제하기 때문에 이를 사용하기는 어렵다.
    - 드롭아웃의 keep_prop을 1.0으로 설정, 드롭아웃을 하여 구현이 맞기를 바라기!
    - 드롭아웃을 끄고 알고리즘이 최소한 드롭아웃 없이 맞는지 이중 검사하기 위해 경사 검사를 사용하고 드롭아웃을 켜는 것
- Run at random initialization; perhaps again after some training.
    - 무작위적 초기화에서 w와 b가 0에 가까울 때 경사 하강법의 구현이 맞게 된 경우 - 불가능
    - 무작위적인 초기화에서 경사 검사를 실행하기 → 네트워크를 잠시동안 훈련해 w와 b가 0에서 멀어질 수 있는 시간 주기
    - 일정 수의 반복을 훈련한 뒤 다시 경사 검사하기
