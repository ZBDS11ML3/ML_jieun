
# Xgboost



### **Introduction**

> Among the 29 challenge winning solutions 3 published at Kaggle’s blog during 2015, 17 solutions used XGBoost. Among these solutions, eight solely used XGBoost to train the model, while most others combined XGBoost with neural nets in ensembles.
> \- XGBoost: A Scalable Tree Boosting System, Tianqi Chen, Carlos Guestrin (KDD2016)

XGBoost의 논문에서는 2015년동안 Kaggle에 게시된 29번의 대회중에서 XGBoost를 사용한 17개의 솔루션이 우승을 거머쥐었다고 합니다.이 솔루션 중 8개는 XGBoost만을 사용하여 모델을 교육한 반면,대부분의 다른 솔루션은 XPBoost를 앙상블의 신경망과 결합했다고 합니다.
관련 논문은 [**여기를 클릭**](https://arxiv.org/pdf/1603.02754.pdf)하세요.



### **XGBoost까지의 흐름**



![](https://github.com/ZBDS11ML3/ML_jieun/blob/main/0.Confusion_matrix/img.jpg)



`Decision Trees`를 `Bagging`이라는 앙상블기법을 이용하여 성능을 높였고, 여기에 `Random`성을 부여하여 `Random Forest`를 만들었습니다. 이 후에는 `Stumps Tree`를 베이스로하는 `Adaptive Boosting`이 있었고, `Gradient`를 이용해서 `Boosting`을 하였습니다. **XGBoost**(e**X**treme **G**radient **Boost**ing)는 `Gradient`의 방법을 따라가지만, 더 많은 데이터를 한번에 다룰 수 있고 더 빠르게 처리할 수 있습니다.





* `XGBoost`는 `로지스틱 회귀(Logistic Regression)`, `랜덤 포레스트(Random Forest)`, `의사결정나무(Decision Tree)`, `K-최근접 이웃(KNN)`과 비교하여 높은 예측 성능, 과적합 방지 기능, 병렬 처리 등 여러 가지 장점을 가지고 있습니다. 이러한 이유로 다양한 데이터셋과 문제에서 우수한 성능을 발휘하며, 기계 학습 경연 대회에서도 많이 사용되는 알고리즘 중 하나입니다.

* 그러나 `XGBoost`는 해석력이 떨어지며, 복잡한 하이퍼파라미터, 노이즈에 대한 민감성, 상대적으로 긴 학습 시간 등 몇 가지 단점도 가지고 있습니다.

  

  * **해석력이 떨어진다는 것은?**
    * 해석력이 떨어진다는 것은 모델의 결과를 이해하고 설명하기 어렵다는 것을 의미합니다. 즉, 모델이 어떻게 예측을 수행하는지 명확하게 파악하거나 특성 간의 관계를 직관적으로 이해하기 어렵다는 것입니다.
    * 예를 들어, `로지스틱 회귀`의 경우, 모델은 각 특성의 가중치(계수)를 학습하여 예측을 수행합니다. 이 가중치는 특성 간의 관계를 직접 해석할 수 있어 설명력이 높습니다. 그러나 `XGBoost`와 같은 앙상블 모델의 경우, 여러 개의 기본 모델(예: `의사결정나무`)이 결합되어 예측을 수행하므로 결과를 해석하기 어렵습니다. 이렇게 복잡한 구조 때문에 모델이 어떤 특성을 중요하게 생각하고, 어떻게 예측을 수행하는지 직관적으로 이해하기 어려운 것을 말합니다.
    * 해석력이 높은 모델은 예측 결과를 설명하고, 특성 간의 관계를 파악하는 데 도움이 됩니다. 이러한 이유로 해석력이 높은 모델은 의사 결정 과정에서 쉽게 사용할 수 있습니다. 그러나 해석력이 떨어지는 모델은 예측 성능이 높아도 결과를 설명하는 데 어려움이 있을 수 있습니다. 이 때문에 사용자가 모델 결과에 대한 신뢰성을 평가하기 어려울 수 있으며, 모델이 잘못된 예측을 하는 원인을 찾기 어렵습니다.



## 장점

* **높은 예측 성능**
   `XGBoost`는 그래디언트 부스팅 방식을 효율적으로 구현하여 다른 알고리즘에 비해 높은 예측 성능을 보입니다. 이로 인해 다양한 데이터셋과 문제에서 우수한 성능을 발휘합니다.
* **규제화(Regularization)**
   `XGBoost`는 L1 (Lasso) 규제와 L2 (Ridge) 규제를 모두 포함하고 있습니다. 규제화는 모델이 과적합되는 것을 방지하는 데 도움이 되는 기술입니다.
* **자동 가지치기(Pruning)**
   `XGBoost`는 의사결정나무를 구축할 때 자동 가지치기 기능을 제공합니다. 이를 통해 트리의 복잡도를 줄이고 과적합을 방지할 수 있습니다.
* **병렬 처리(Parallel Processing)**
   `XGBoost`는 학습 및 예측 과정에서 병렬 처리를 지원하여 대용량 데이터셋에도 빠르게 적용할 수 있습니다.
* **유연성**
   `XGBoost`는 사용자 정의 목적 함수와 평가 지표를 지원하므로 다양한 문제에 적용할 수 있습니다.



## 단점

* **복잡도**
  `XGBoost`는 다른 알고리즘에 비해 하이퍼파라미터가 많아 튜닝이 어려울 수 있습니다. 이로 인해 모델의 성능을 최적화하기 위한 시간과 노력이 필요합니다.
* **해석력**
   `XGBoost`는 앙상블 기법을 사용하기 때문에 의사결정나무나 로지스틱 회귀와 같은 모델보다 해석력이 떨어질 수 있습니다. 복잡한 모델 구조로 인해 결과를 이해하고 설명하기 어렵습니다.
* **노이즈에 민감**
   `XGBoost`는 노이즈가 있는 데이터셋에 대해 민감할 수 있습니다. 이는 모델이 과적합되거나 불안정한 결과를 생성할 수 있습니다.
* **상대적으로 긴 학습 시간**
  `KNN`이나 `로지스틱 회귀`와 비교했을 때, `XGBoost`는 학습 시간이 상대적으로 길 수 있습니다. 이는 모델을 순차적으로 학습하기 때문에 발생하는 문제입니다.







## 다른 모델들과의 비교



### **로지스틱 회귀(Logistic Regression)**와 비교:

* **장점**:
  `XGBoost`는 앙상블 기반으로 높은 예측 성능을 제공합니다. 로지스틱 회귀보다 복잡한 문제와 비선형 관계를 더 잘 처리할 수 있습니다.
  `XGBoost`는 규제화, 가지치기 등 과적합을 방지하는 기능이 있어 일반화 성능이 좋습니다.
* **단점**:
  `XGBoost`는 로지스틱 회귀에 비해 해석력이 떨어집니다. 로지스틱 회귀는 계수를 직접 해석할 수 있어 설명력이 높습니다.
  `XGBoost`의 학습 시간이 로지스틱 회귀보다 길 수 있습니다.

### **랜덤 포레스트(Random Forest)**와 비교:

* **장점**:
  `XGBoost`는 규제화를 포함하여 과적합을 방지하고 일반화 성능을 높이는 기능이 있습니다.
  `XGBoost`는 병렬 처리를 지원하여 대용량 데이터셋에서도 빠르게 학습할 수 있습니다.
* **단점**:
  `XGBoost`는 랜덤 포레스트보다 하이퍼파라미터가 많아 튜닝이 어려울 수 있습니다.
  랜덤 포레스트와 비교하여 `XGBoost`는 노이즈에 민감할 수 있습니다.

### **의사결정나무(Decision Tree)**와 비교:

* **장점**:
  `XGBoost`는 앙상블 기반으로 높은 예측 성능을 제공하며, 과적합을 방지하는 기능이 있습니다. 의사결정나무에 비해 더욱 안정적인 성능을 보입니다.
  `XGBoost`는 병렬 처리를 지원하여 대용량 데이터셋에서도 빠르게 학습할 수 있습니다.
* **단점**:
  `XGBoost`는 의사결정나무에 비해 해석력이 떨어집니다.
  `XGBoost`의 학습 시간이 의사결정나무보다 길 수 있습니다.

### **K-최근접 이웃(KNN)**과 비교 :

* **장점**:
  `XGBoost`는 앙상블 기반으로 높은 예측 성능을 제공하며, `KNN`에 비해 복잡한 문제와 비선형 관계를 더 잘 처리할 수 있습니다.
  `XGBoost`는 대용량 데이터셋에서도 빠르게 학습할 수 있는 반면, `KNN`은 학습 시간이 거의 없지만, 예측 시간이 길어질 수 있습니다.
* **단점**:
  `XGBoost`는 `KNN`에 비해 해석력이 떨어집니다. `KNN`은 비교적 직관적인 이웃 거리를 기반으로 분류하거나 회귀를 수행합니다.
  `XGBoost`의 학습 시간이 `KNN`에 비해 길 수 있습니다.` KNN`은 학습 시간이 거의 필요하지 않지만, 예측 시간이 길어질 수 있습니다.
