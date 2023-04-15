# ML_jieun



## 1. CNN



### CNN1



**코드 실행 결과**

```
이 노래의 예상되는 장르는 blues 입니다.
32/32 - 0s - loss: 3.4569 - accuracy: 0.5235 - 41ms/epoch - 1ms/step
테스트 정확도: 0.5235235095024109
```

으로 정확도는 `0.5235..`이지만 테스트파일의 실제 장르가 blues이므로 데이터의 장르 예측에는 성공했다.



### CNN2



CNN1에서 모델 아키텍처 변경으로 Conv2D 레이어의 필터 개수를 16에서 32, 32에서 64, 64에서 128로 늘리고, Dense 레이어의 개수를 1개에서 2개로 늘렸습니다. 또한, 두 번째 Dense 레이어 뒤에 Dropout 레이어를 추가하여 overfitting을 방지하도록 했다.



**코드 실행 결과**

```
이 노래의 예상되는 장르는 blues 입니다.
32/32 - 0s - loss: 3.3821 - accuracy: 0.6156 - 53ms/epoch - 2ms/step
테스트 정확도: 0.6156156063079834
```

으로 정확도는 `0.6156..`이지만 테스트파일의 실제 장르가 blues이므로 데이터의 장르 예측에는 성공했다.







## 2. KNN



### knn1



**코드 실행 결과**

```
예측한 음악 장르: metal
정확도: 64.50%
```

으로 정확도는 `64.50%`지만 테스트파일의 실제 장르는 blues로 데이터의 장르 예측에는 실패했다.





### knn2



* knn1의 코드에서 교차 검증을 사용하여 정확도를 높이고, 그리드 검색을 사용하여 최적의 k값을 찾아 수정해보았다.

**코드 실행 결과**

```
최적 k 값: 5
예측한 음악 장르: metal
정확도: 64.50%
교차 검증된 정확도: 66.75%
```

으로 정확도는 `64.50%`, 교차 검증된 정확도는 `66.75%` 테스트파일의 실제 장르는 blues로 데이터의 장르 예측에는 실패했다.





## 3. RandomForestClassifier



* `knn2`의 코드에서 모델을 변경하여, `RandomForestClassifier`로 모델을 생성하고, 그리드 검색을 사용하여 최적의 하이퍼파라미터를 찾아 정확도를 높이는 시도를 해 보았다.



**코드 실행 결과**

```
최적의 하이퍼파라미터: {'max_depth': None, 'min_samples_leaf': 1, 'min_samples_split': 5, 'n_estimators': 200}
예측한 음악 장르: classical
정확도: 76.00%
교차 검증된 정확도: 78.62%
```

으로 정확도는 `76.00%`, 교차 검증된 정확도는 `78.62%` 테스트파일의 실제 장르는 blues로 데이터의 장르 예측에는 실패했다.







**features_3_sec.csv 데이터로 변경 후 코드 실행 결과**

```
최적의 하이퍼파라미터: {'max_depth': 20, 'min_samples_leaf': 1, 'min_samples_split': 2, 'n_estimators': 200}
예측한 음악 장르: classical
정확도: 88.14%
교차 검증된 정확도: 85.82%
```

으로 정확도는 `88.14%`, 교차 검증된 정확도는 `85.82%` 테스트파일의 실제 장르는 blues로 데이터의 장르 예측에는 실패했다.











## 4. xgboost



* `RandomForestClassifier`를 사용한 모델링에서 `XGBoost`를 사용하여 바꾸어보았다.
* `XGBoost`는 분류 및 회귀 분석에 모두 사용이 가능하며, 고차원의 특성과 대량의 데이터에 대해 높은 성능을 발휘하여 높은 정확도와 빠른 실행 속도를 보장한다.

* `XGBoost`는 `Gradient Boosting` 알고리즘을 기반으로 하며, 여러 개의 결정 트리를 사용하여 모델을 구성하므로 `RandomForestClassifier`보다 성능이 우수할 것이란 예측을 했다.
* 또한 ` XGBoost`는 하이퍼파라미터 튜닝을 통해 모델의 성능을 더욱 개선할 수 있다. 
  `GridSearchCV`와 같은 교차 검증 기법을 사용하여 최적의 하이퍼파라미터를 자동으로 찾을 수 있다.



###  xgboost1



**코드 실행 결과**

```
최적의 하이퍼파라미터: {'learning_rate': 0.1, 'max_depth': None, 'min_child_weight': 2, 'n_estimators': 200}
예측한 음악 장르: classical
정확도: 75.50%
교차 검증된 정확도: 77.25%
```

으로 정확도는 `75.50%`, 교차 검증된 정확도는 `77.25%` 테스트파일의 실제 장르는 blues로 데이터의 장르 예측에는 실패했다.





###  xgboost2



**코드 실행 결과**

```
최적의 하이퍼파라미터: {'learning_rate': 0.09796599427179664, 'max_depth': None, 'min_child_weight': 3, 'n_estimators': 243}
예측한 음악 장르: classical
정확도: 90.14%
교차 검증된 정확도: 88.39%
```

으로 정확도는 `90.14%`, 교차 검증된 정확도는 `88.39%` 테스트파일의 실제 장르는 blues로 데이터의 장르 예측에는 실패했다.