---
typora-root-url: 0.Confusion_matrix
---

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



1. `extract_features` 함수를 정의하여 음악 파일에서 MFCC, Chroma, Mel, Spectral Contrast, Tonnetz와 같은 오디오 특성을 추출한다.
2. 데이터셋을 불러와 문자열 클래스 레이블을 숫자형으로 변환한다.
3. 특성과 레이블을 분리하고, 데이터를 학습용과 테스트용으로 분리한다. (예: 80% 학습, 20% 테스트)
4. 특성 스케일링을 수행한다 (StandardScaler 사용).
5. XGBoost 분류기를 생성하고 GridSearchCV를 사용하여 하이퍼파라미터 튜닝을 수행한다.
6. 최적의 하이퍼파라미터를 사용하여 XGBoost 분류기를 학습시킨다.
7. 테스트 파일에서 특성을 추출하고, 스케일링된 특성을 사용하여 장르를 예측한다.
8. 테스트 세트에서 정확도를 평가하고 교차 검증을 사용하여 정확도를 평가한다.



**코드 실행 결과**

```
최적의 하이퍼파라미터: {'learning_rate': 0.1, 'max_depth': None, 'min_child_weight': 2, 'n_estimators': 200}
예측한 음악 장르: classical
정확도: 75.50%
교차 검증된 정확도: 77.25%
```

으로 정확도는 `75.50%`, 교차 검증된 정확도는 `77.25%` 테스트파일의 실제 장르는 blues로 데이터의 장르 예측에는 실패했다.





###  xgboost2



1. 필요한 라이브러리를 추가 임포트:
   - `RandomizedSearchCV`: 하이퍼파라미터 튜닝에 사용된다.
   - `randint`, `uniform`: 하이퍼파라미터 튜닝에서 무작위 값을 생성하는 데 사용된다.
2. `extract_features` 함수를수정:
   - `n_features` 매개변수를 추가하여 함수 호출시 원하는 특성 개수를 지정할 수 있도록 했다.
   - `feature_vector` 변수를 생성하여 여러 특성을 하나의 배열로 결합하고, 원하는 개수의 특성으로 자른다.
3. 데이터 분할 과정에서 `random_state`를 제거.
4. XGBoost 분류기 생성 시 `random_state`를 제거.
5. GridSearchCV 대신 RandomizedSearchCV를 사용하여 하이퍼파라미터 튜닝을 수행했다:
   - 무작위 값이 있는 `param_dist` 딕셔너리를 정의.
   - `random_search`를 사용하여 하이퍼파라미터 탐색을 수행하고 최적의 하이퍼파라미터를 출력.
6. 수정된 `extract_features` 함수를 사용하여 테스트 파일의 특성을 추출.





**코드 실행 결과**

```
최적의 하이퍼파라미터: {'learning_rate': 0.17940931103542268, 'max_depth': 10, 'min_child_weight': 1, 'n_estimators': 295}
예측한 음악 장르: classical
정확도: 76.50%
교차 검증된 정확도: 76.88%
```

으로 정확도는 `76.50%`, 교차 검증된 정확도는 `76.88%` 테스트파일의 실제 장르는 blues로 데이터의 장르 예측에는 실패했다.





**features_3_sec.csv 데이터로 변경 후 코드 실행 결과**

```
최적의 하이퍼파라미터: {'learning_rate': 0.09796599427179664, 'max_depth': None, 'min_child_weight': 3, 'n_estimators': 243}
예측한 음악 장르: classical
정확도: 90.14%
교차 검증된 정확도: 88.39%
```

으로 정확도는 `90.14%`, 교차 검증된 정확도는 `88.39%` 테스트파일의 실제 장르는 blues로 데이터의 장르 예측에는 실패했다.











**데이터 셋을 test_dataset.csv로 설정한 코드 실행 결과**

```
최적의 하이퍼파라미터: {'learning_rate': 0.11712624707999042, 'max_depth': 18, 'min_child_weight': 1, 'n_estimators': 299} 'n_estimators': 299}
예측한 음악 장르: classical
정확도: 94.67%
교차 검증된 정확도: 91.17%
```

![](/confusion_matrix_test_dataset.png)

