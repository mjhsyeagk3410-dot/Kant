# 11월 5주차 정리 TIL

## 11월 23일 MON 
### part1 개념
#### 01 AI Literacy 
> 인공지능(AI)의 원리와 한계를 이해하고, 결과물을 비판적으로 평가하며, 윤리적이고 주체적으로 활용하는 종합 역량 

#### 02 AI 기술 포함 관계 (포개진 원)
##### (A) 인공지능
> 컴퓨터나 기계가 학습, 추론, 지각, 언어 이해, 문제 해결, 의사 결정 등 인간의 지적 능력을 수행하도록 구현한 기술과 그 연구 분야를 뜻함
##### (B) 머신러닝
> 전통 프로그래밍은 사람이 만든대로만 하다보니 예상치 못한 상황에서 막히고 머신러닝은 예상치 못한 상황에서도 해결해나간다 <br>
> 추론: 학습이 끝난 모델에 새 입력을 넣어 예측값이나 응답을 생성하는 실행 단계 <br>
> 온도: 다음 토큰을 고를 때 확률 분포를 얼마나 날카롭게(결정적) 또는 평탄하게 조정할지 정하는 샘플링 하이퍼파라미터. 낮으면 일관된 답, 높으면 다양한 표현이 나옴
> 컨텍스트 위도우: 모델이 한 번에 처리하고 기억할 수 있는 최대 토큰 길이. 이 범위를 넘어가면 앞부분 맥락이 잘리거나 주의력이 희석됨. 
> 지도학습: 입력(X)과 정답(y) 쌍을 주고 둘 사이의 관계를 학습하는 방식
> 비지도학습: 정답 레이블 없이 데이터 자체의 구조, 군집, 패턴을 찾아내는 방식
> 강화학습: 에이전트가 환경과 상호작용하며 보상을 최대화하는 행동 전략(정책)을 시행착오 끝에 학습하는 방식 
##### (C) 딥러닝
> 트랜스포머: 순차적으로 처리하던 기존 구조와 달리, 문장이나 토큰 전체를 병렬로 다루며 맥락을 파악하는 신경망 아키텍처. 
> 셀프 어텐션: 시퀀스 내 각 토큰이 다른 토큰들과 얼마나 강하게 연관되는지 가중치를 계산해 문맥을 반영하는 트랜스포머의 핵심 연산 메커니즘. 
> 파운데이션 모델: 방대한 데이터로 폭넓게 사전학습한 뒤 요약, 번역, 코드 생성, 분류 등 다양한 다운스트림 작업에 범용적으로 활용할 수 있는 기반 모델. 
##### (D) 생성형 AI & LLM
> 생성형 AI는 새로운 결과물을 만드는 기술 전체<br>
> LLM은 생성형 AI중 글(언어)을 다루는 모델<br>
> LLM의 작동원리는 확률계산-단어선택-반복

#### 03 AI 리터러시 3가지 원칙
> 확률적 제안임을 인지: 정답 생성기가 아니라 확률 기반 다음 토큰/결과 예측기<br>
> 환각 현상 경계: 학습 데이터, 문맥 밖에서도 단정적으로 꾸며낼 수 있음<br>
> 안전한 활용과 보안: 입력과 출력 모두 데이터 유출, 권한, 정책 이슈와 연결

### part2 코드
#### 타이타닉 데이터셋 다루기
```sh
# 사용한 라이브러리 부르고 버전확인하기
import pandas as pd
import numpy as np
import seaborn as sns
print("pandas:", pd.__version__, "numpy:", np.__version__, "seaborn:", sns.__version__)

# 타이타닉 데이터셋 불러오고 상단 5행 출력하기
df = sns.load_dataset('titanic')
df.head(5)

# 데이터 shape 조회
df.shape

# 자료형 조회 
df.info()

# 기초 통계수학 조회 
df.describe()

# 각 셀의 널(Nan)여부
df.isnull().sum()

# 나이가 비어있는 승객 수, 성별, 클래스 조회 
empty_age = df["age"].isnull()
print("나이 빈칸:", empty_age.sum(), "명")
df.loc[empty_age, ["sex", "age", "class"] ].head()

# 평균값, 중앙값 산출하기
print("평균:", round(df["age"].mean().2))
print("중앙값:", round(df["age"].median().2))

mean_age = df["age"].mean()
df.loc[:, "age"] = df["age"].fillna(mean_age)

# 탑승한 항구 중 최빈값
df["embark_town"].value_counts(dropna=False)

# 최빈값 추출 후 빈칸에 채우는 로직
mean_town = df["embark_town"].mode()[0]
print("최빈값:", mode_town)
df.loc[:, "embark_town"] = df["embark_town"].fillna(mode_town)
df["embark_town:].value_counts(dropna=False)

# embarked town 값으로 설정
df.loc[:, "embarked"] = df["embark_town"].str[0]
df[["embarked", "embark_town"]].isnull().sum()

# deck의 null값에 unknown으로 추가해줌
df["deck"] = df["deck"].cat.add_categories("Unknown").fillna("Unknows")

print(df["deck"].cat.categories.to_list())
print(df["deck"].value_count())

# 튀는 값 확인하기 
print(df["fare"].quantile([0.25, 0.5, 0.75]))
df["fare"].describe()[["25%", "50%", "75%"]]

# IQR 계산(Q3~Q1), 이상수치 Q3+1.5*IQR
q1 = df["fare"].quantile(0.25)
q3 = df["fare"].quantile(0.75)
iqr = q3 - q1
upper = q3 + 1.5*iqr

# 사분위수(Q1, Q2, Q3) 및 IQR 기준 이상치 상한선 (UPPER) 출력과 초과 인원 수 확인하기
print(f"Q1={q1:.2f}, Q3={q3:.2f} IQR={iqr:.2f} UPPER={upper:.2f}")
print("이상 승선요금:", (df["fare"] > upper).sum(), "명")

# 승선요금(fare)이 512 이상인 고객 데이터 필터링 조회
df[df["fare"] >= 512]

# 승선요금 512 이상 이상치를 제거하고 제거 전후 데이터 행 수(len) 비교)
before = len(df)
df = df [df["fare"] < 512].copy()
print(before, "=>", len(df))

# 중복되는 행 확인
print("중복 행:", df.duplicated().sum(), "개")
df[df.duplicated(keep:False)].sort_values(["fare", "age"]).head(5)

# 그래프로 시각화해보기 (+한글폰트로 보기)
import platform
import matplotlib.pyplot as plt
import seaborn as sns

plt.rcParams["font.family"] = "Malgun Gothic"

## 나이 분포 차트
fig, ax = plt.subplots(figsize=(6,4))
ax.hist(df["age"].dropna(), bins=20, color="blue", edgecolor="black")
ax.set_title("나이분포")
ax.set_xlabel("나이(세)")
ax.set_ylabel("인원 수")
plt.tight_layout()
plt.show()

# 산점도
fig, ax = plt.subplots(figsize=(6,4))
ax.scatter(df["age"], df["fare"], s=12, alpha=0.6)
ax.set_title("산점도")
ax.set(xlabel="나이", ylabel="요금")
plt.tight_layout()
plt.show()

# 박스플롯
fig, ax = plt.subplots(figsize=(10,3))
sns.boxplot(x="class", y="fare", data=df, ax=ax, hue="class", palette="Set2", legend=False)
ax.set_title("등급별 승선요금 분포")
ax.set(xlabel="좌석 등급", ylabel="요금")
plt.tight_layout()
plt.show()

```

## 11월 24일 TUE

### part1 개념
#### 01 numpy
> 다차원 배열과 벡터 연산을 빠르게 처리하는 수치 계산 기반 라이브러리
#### 02 Pandas
> 행과 열로 구성된 DataFrame으로 데이터를 불러오고 정제하며 집계하는데 쓰임
#### 03 Seaborn
> Matplotlib을 기반으로 분포도, 박스플롯, 히트맵 등 통계 차트를 간결한 코드와 세련된 스타일로 그리는 고수준 시각화 라이브러리
#### 04 Matplotlib
> 선, 막대, 산점도 등 기본 그래프를 그리고 축, 제목, 레이아웃을 세밀하게 제어하는 저수준 시각화 엔진
#### 05 .pyplot
> Matplotlib의 서브패키지로서 2D그래프를 생성하고 제어함 
#### 06. Figure
> Matplotlib에서 사용. <br>
> 여러 개의 그래프를 담을 수 있는 전체 창이나 도화지. 전체크기, 배경색, 전체제목등을 다룸
#### 07. Axes
> Matplotlib에서 사용. <br>
> 실제 선, 막대, 산점도 등이 그려지는 플롯 영역. 하나의 Figure안에 여러 개의 Axes를 배치할 수 있음. 각 Axes는 자체 X축, y축(axis), 제목, 범례, 축 범위 등을 가짐
#### 08. Box Plot
> 전체 데이터로부터 얻어진 최솟값, 제1사분위 수(Q1), 제2사분위 수 또는 중위수(Q2), 제3사분위 수(Q3), 최댓값 요약 수치를 사용해서 그린다 
#### 09. 사분위 수
> Box Plot에서 <br>
> 데이터를 4등분한 지점을 의미. 예를 들어 제1사분위수는 전체 데이터 중 하위 25%에 해당하는 값, 제3사분위 수는 전체 데이터 중 상위 25%에 해당하는 값
#### 10. Whisker(수염)
> Box Plot에서 <br>
> 상자(Q1~Q3, 사분위수 범위 IQR) 바깥으로 뻗어 나온 선. 이상치를 제외한 데이터의 퍼짐 범위 
#### 11. sklearn
> Scikit-learn은 파이썬에서 사용하는 머신러닝 라이브러리. 다양한 머신러닝 알고리즘, 데이터 전처리 기능을 제공, 간단하고 일관된 API를 사용하여 사용자가 모델링 작업을 쉽게 수행할 수 있도록 지원. <br>
> 분류(Classification), 회귀(Regression), 군집화(Clustering), 차원 축소(Dimensionality Reduction), 모델 선택(Model Selection), 전처리(Preprocessing)
#### 12. metrics
> 모델의 성능을 쉽게 측정할 수 있도록 함. torch등의 딥러닝에서 얻은 데이터도 numpy나 list로 변환하여 사이킷런의 metrics를 이용하면 매우 쉽게 성능을 구현. 
#### 13. MAE, mean absolute error
> 평균절대오차, 실제값과 예측값의 차이에 절댓값을 씌운 뒤 평균을 구한 회귀 모델 평가 지표. 값이 0에 가까울수록 예측 정확도가 높음 
#### 14. MSE, mean squared error
> 평균제곱오차, 통계,머신러닝, 딥러닝에서 예측값과 실제값의 차이를 제곱해 평균낸 지표. 값이 작을수록 예측 정확도가 높고 큰 오차에 더 큰 가중치를 둠
#### 15. RMSE, root mean squared error
> 평균 제곱근 오차, 회귀 모델이나 예측 모델의 예측값과 실제값 사이의 오차 크기를 측정하는 대표 지표
#### 16. R2 score, r-squared
> 결정계수. 결정계수는 상관계수를 제곱한 값. 하지만 결정계수는 상관계수와 달리 변수간 영향을 주는 정도 또는 인과관계의 정도를 정량화해서 나타낸 수치. 따라서 결정계수는 상관 분석이 아닌 회귀분석에서 사용하는 수치<br>
> 회귀 모델의 성능에 대한 평가지표이며 회귀모델에서 독립 변수가 종속 변수를 얼마나 잘 설명해주는지 보여주는 지표. 하지만 독립변수의 개수가 증가하면 결정계수 또한 함께 증가하여 결정계수에만 의존하여 회귀모델을 평가하기 어려움. 그래서 조정된 결정계수가 제시. 
#### 17. Boolean Mask(불리언 마스크)
> 데이터 길이와 같은 크기의 True/False 배열을 만들어 원하는 조건의 행만 골라내는 필터링 방식 
### part2 코드
#### 엑셀 데이터셋 다루기
```sh
import numpy as np
import pandas as pd
import seaborn as sns
import matplotlib.pyplot as plt 

plt.rcParams["font.family] = "Malgun Gothic"

# 엑셀데이터셋 불러오기
house = pd.read_csv("./datasets/usa_housing.csv")
print(house.shape)

# 특정 조건을 만족하는 주택 데이터 골라내, 몇행 몇열로 되어있는지 확인
small = house[(house["YearBuilt"]>2015) & (house["CrimeRate"] < 40)]

# 그래프그리기
plt.figure(figsize=(8,4))
plt.scatter(house["SquareFeet"], house["Price"], alpha=0.4, label="전체 300채")
plt.scatter(small["SquareFeet"], small["Price"], color="red", s=50, label="2015이후 건축")
plt.xlabel("면적")
plt.ylabel("가격")
plt.legend()
plt.show()

print("전체 300채의 상관계수:", round(house["SquareFeet"].corr(house["Price"]).2))
print("10채의 상관계수", round(small["SquareFeet"].corr(small["Price"]).2))

# 면적(area)과 가격(price)으로 이루어진 오피스 매물 데이터를 난수로 만듦
# 그중 5개에 일부러 높은 추가 금액을 더한 뒤 기초 통계량을 요약

# 난수 생성기 준비
rng = np.random.default_rng(40)

# 기준값 및 면적 생성, 기본가격 생성
a = 200
area = rng.uniform(20, 85, n)
price = (area * 450 + 5000 + rng.normal(0,2500))

# 일부 매물 가격 상향
special = rng.choice(n, 5,replace=False)
price[special] += rng.uniform(15000, 25000, 5).round(-1)

# 데이터프레임 구성 및 요약
office = pd.DataFrame({"area":area, "price":price})
office.describe().round(1)

# 변경된 엑셀파일 다른 이름으로 저장
office.to_csv("./datasets/office.csv", index=False)

# 산점도 차트 그리기
plt.figure(figsize=(8,5))

plt.scatter(office["area"], office["price"], alpha=0.6)

plt.title("오피스텔 시세 200건")
plt.xlabel("면적")
plt.ylabel("가격")
plt.show()

print("상관계수:", office["area"].corr(office["price"]))

# 선형회귀 모델 만들기
from sklearn.linear_model import LinearRegression

X = office[["area"]]
y = office["price"]

model = LinearRegression()

model.fit(X, y)

print(f"기울기 w = {model.coef_[0]} 정답: 450")
print(f"절편 b = {model.intercept_} 정답: 5000")

# 33, 59 가격 예측 데이터프레임 만들기
new = pd.DataFrame({["area": [33, 59]})
model.predict(new).round(-1)

# 학습한 모델로 예측하기 
y_pred = model.predict(X)
line = X.sort_values("area")
line_pred = model.predict(line)

plt.figure(figsize=(8,5))

plt.scatter(office["area"], office["price", alpha=0.6, label="실제 시세")
plt.plot(line["area"], line_pred, color="red", label="모델의 직선")
plt.title("오피스텔 시세 200건 및 예측")
plt.xlabel("면적")
plt.ylabel("가격")
plt.show()

# MAE, MSE, RMSE, R_SCORE
from sklearn.metrics import mean_absolute_error, mean_squared_error, root_mean_squared_error, r2_score
# ---------------------------------------------------------------------------
# 1. 전체 데이터 기준 모델 성능 평가 (실제값 y vs 예측값 y_pred)
# ---------------------------------------------------------------------------
# MAE: 오차 절댓값의 평균 (단위 직관적 파악용, 소수점 없이 정수로 출력)
print(f"MAE = {mean_absolute_error(y, y_pred):,.0f}")
# MSE: 오차 제곱의 평균 (큰 오차에 더 큰 페널티 부여)
print(f"MSE = {mean_squared_error(y, y_pred):,.0f}")
# RMSE: MSE에 루트를 씌운 값 (원래 타깃과 같은 단위 유지)
print(f"RMSE = {root_mean_squared_error(y, y_pred):,.0f}")
# R2 Score(결정계수): 모델이 데이터 분산을 얼마나 설명하는지 (1에 가까울수록 좋음)
print(f"R_SCORE = {r2_score(y, y_pred):.3f}")

# ---------------------------------------------------------------------------
# 2. 특이매물 / 정상매물 불리언 마스크 생성
# ---------------------------------------------------------------------------
# office 전체 행 길이만큼 True 배열을 만든 뒤, 특이매물 인덱스(special)만 False로 변경
normal = np.ones(len(office), dtype=bool)
normal[special] = False
print("특이매물", special)
print("정상매물", normal.sum()) # True 개수 = 정상매물 건수

# ---------------------------------------------------------------------------
# 3. 비교 대상 구간(전체 vs 특이매물 제외)별 주요 지표 산출
# ---------------------------------------------------------------------------
all_rows = np.ones(len(office), dtype=bool)
# (비교 라벨, 필터링용 불리언 마스크) 튜플 리스트
cases = [("전체 200건", all_rows), ("특이매물 제외 195건", normal)] # 전체 매물 선택용 마스크 (전부 True)

for name, mask in cases:
    # 마스크를 적용해 해당 구간의 실제값과 예측값만 추출
    y_true = y[mask]
    y_hat = y_pred[mask]

    # 구간별 평가지표 계산
    mae = mean_absolute_error(y_true, y_hat)
    rmse = root_mean_squared_error(y_true, y_hat)
    r2 = r2_score(y_true, y_hat)
    print(f"{name} MAE {mae} | RMSA {rmse} | RScore {r2}")
```

## 11월 25일 WED

## 11월 26일 THU
## 11월 27일 FRI