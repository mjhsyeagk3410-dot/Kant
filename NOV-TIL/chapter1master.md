# 챕터 1 완전정복하기

## Part 1. Python 핵심 문법

### Python 프로젝트와 실행 환경 
- uv init
     터미널에서 **uv init --no-package**를 입력해서 uv초기화를 한다 
- uv sync 또는 uv run
    - uv초기화가 되면 **uv sync**나 **uv run**으로 .venv라는 가상환경을 만든다
- 가상환경
    - **source .venv/Scripts/activate** 라는 명령어로 가상환경으로 들어간다
- Jupyter 커널
    - 사용을 위해 먼저 **uv add ipykernel** 이라는 명령어를 사용해 다운로드를 받아준다 
    - .ipynb라는 파일을 만들어주고, 여기서 커널을 선택할 수 있는데 위에서 만든 가상환경의 커널을 선택해주면 된다. 

### 변수와 자료형, 자료구조
# 값에 이름 붙이기 
price = 4500

# 값 보기 
print("합계:", total)

# 타입 확인
type(price)

# 타입 바꾸기 
int("3") str(3)

# 계산: + - * / // % **
# 먼저할 계산: (2 + 3) * 4
# 값 쌓기: score += 10
# 비교하기: == != > < >= <=

# 리스트
prices = [4500, 5000, 6500]
print(prices)
print(len(prices))
print(type(prices))
# 리스트는 값 여러 개를 [] 하나에 담는다 

# 리스트 꺼내고 자르기 
menus = ["coffee", "latte", "cake"]
print(menus[0])
print(menus[-1])
print(menus[0:2])

# 리스트 값 바꾸기, 더하기
prices[0] = 4800
prices.append(3000)
print(prices)
print(sum(prices))
print(max(prices))
print(min(prices))

# 넣고 빼는 메서드: append, insert, remove, pop
cart = ["coffee", "latte"]
cart.append("cake")
cart.insert(0, "tea")
cart.remove("latte")
last = cart.pop()
first = cart.pop()
print(cart, last, first)

# 찾고 세고 정렬하는 메서드: count, index, sort
scores = [70, 95, 80, 95]
print(scores.count(95))
print(scores.index(80))
print(95 in scores)
scores.sort()
print(scores)
scores.sort(reverse=True)
print(scores) 

# 리스트 안의 리스트 
table = [[1, 2, 3], [4, 5, 6], [7, 8, 9]]
print(table[1]) # 4, 5, 6
print(table[1][2]) #6
print(table[-1][-1]) # 9
print(menus[0][0]) # c, menus[0][0] coffee의 0번 글자
mixed = ["coffee", 4500, True]
print(mixed) # 'coffee', 4500, True

# 튜플은 ()에 묶고, 만들면 못바꾼다 
order = ("coffee", 4500, 2)
print(order[0]) # coffee
print(order[1] * order[2]) # 9000
print(order[1:]) # (4500, 2)
print(type(order)) # <class 'tuple'>

# 딕셔너리는 번호 대신 키로 찾는다 
student = ["kim", 90, 85, 77]
print(student[2]) # 85

student = {"name": "kim", "kor": 90, 
           "eng": 85, "math": 77}
print(student["eng"]) # 85 

### 조건문과 반복문
# if는 코드의 갈림길을 만든다 
money = 5000
price = 4500
if money >= price: # True일때만 실행
    print("주문할 수 있어요")
print("다음 손님")

# 조건 자리에는 True나 False가 나오는 식을 적는다
# if는 조건이 True인지 False인지 보고 길을 고른다 
print(money >= price) 
print(money == price)
print("tea" in menu)
print("tea" not in menu)
print(type(money >= price)) 

# else는 조건이 False일 때 갈 길 
money = 3000
if money >= price:
    print("주문할 수 있어요")
else:
    print(f"{price - money}원 더 필요해요")

# elif로 갈림길을 셋 이상 만든다 
total = 12000
if total >= 20000:
    print("10% 할인")
elif total >= 10000:
    print("5% 할인")
else: 
    print("할인 없음")

# for는 정해진 조건만큼 돈다 
money = 10000
for cup in [1, 2, 3]:
    money -= 4500
    print(f"{cup}잔째, 남은 돈 {money}원")

# for와 range로 정한 횟수만큼 돈다 
for i in range(3):
    print("주문", i)
for i in range(1, 4):
    print(f"{i}번 손님")

# while은 조건이 True인 동안 쓴다 
money = 10000
cups = 0 
while money >= 4500:
    money -= 4500
    cups += 1
print(f"{cups}잔, 남은 돈 {money}원")

# continue와 break
orders = ["coffee", "cake", "latte", "tea", "cake"]
soldout = ["latte"]
for o in orders:
    if o in soldout: # 품절일때만 멈추게 if안에 
        print(f"{o} 품절, 주문을 멈춰요")
        break
    print(f"{o} 주문 받았어요")
print("끝")

for o in orders:
    if o in soldout: 
        print(f"{o} 품절, 주문을 멈춰요")
        continue #break를 할지 선택. 
    print(f"{o} 주문 받았어요")
print("끝")

### 함수와 모듈
# def, 매개변수, return, 지역/전역변수, lambda, import

# def 로 만드는 함수 정의와 호출 
def hello():
    print("어서 오세요") # 여기까지는 정의만 하는 코드

hello() # 이렇게 호출을 해야 위 문자열이 출력이 된다 

# 매개변수는 함수이름 괄호안에 들어간다. 
def greet(name):
    print(f"{name}님, 어서 오세요")

greet("kim") #"kim"이라고 쓴 이것은 인자라고 한다. 
greet("lee") # 인자는 적은 순서대로 칸에 들어간다 
             # greet(1, "lee")면, 1 lee님 어서 어서오세요
             # 라떼 두잔이면 (2, "latte")가 아닌 ("latte", 2) 이렇게.

# 매개변수는 쉼표로 여러 개 만든다
def order(menu_name, qty) 

# return은 값을 반환하고 혀냊 실행 중인 함수를 즉시 종료
def check_age(age):
    if age < 0:
        return "잘못된 나이입니다."
    if age >= 18:
        return "성인"
    return "미성년자" 

# 지역변수와 전역변수 
# 함수안에서 만든 변수는 밖에서 안보인다 
# 함수밖에서 만든 변수는 안에서 읽을 수 있다 
def calculate_area(radius):
    area = 3.14 * radius * radius # # 지역변수
    return area

result = calculate_area(5)
print(result) # 78.5 출력
# print(area) # 오류: 함수밖에서는 지역변수에 접근못함

tax_rate = 0.1 # 전역변수

def get_total_price(price):
    return price + (price * tax_rate) # 함수안에서 전역변수 읽기 가능

print(get_total_price(10000)) # 11000.0 출력 

# lambda는 한 줄로 만드는 이름 없는 함수 
price_of = lambda price, qty: price * qty
print(price_of(2500, 2))
label = lambda p: "비쌈" if p >= 5000 else "보통" 
print(label(6500), label(4500))

# lambda에서 map은 for와 append로 새 리스트를 만드는 일을 한 줄로 줄인다 
prices = [4500, 5000, 6500] 

def add500(p):
    return p + 500

print(list(map(add500, prices)))
print(list(map(lambda p: p + 500, prices)))
print(prices)

# lambda에서 filter는 for와 if로 골라 담던 일을 한 줄로 줄여준다
prices = [4500, 5000, 6500, 3000]
big = []
for p in prices:
    if p >= 5000:
        big.append(p)
print(big)
print(list(filter(lambda p: p >= 5000, prices)))

# import 하는법
# import 모듈을 하거나 from 모듈 import 이름을 하면 됨
# 첫번째는 모듈 전체를 가져오는것, 두번째는 모듈 내 필요한것만 가져올때 쓴다 
---

## Part 2. Docker 핵심 개념과 명령어

### Docker의 기본 개념
- 이미지 
> 컨테이너를 생성하고 실행하는 데 필요한 코드, 
> 실행 환경, 라이브러리, 설정 파일 등을 담을 
> 읽기 전용 템플릿, 요약하면 게임 칩

- 컨테이너
> 애플리케이션과 그 실행에 필요한 코드, 라이브러리, 설정 등을 하나로 묶어 독립적이고 일관된 환경에서 실행하는 격리된 프로세스 단위 

- Docker Engine
> 애플리케이션을 컨테이너로 빌드하고 실행, 관리하는 오픈 소스 컨테이너화 핵심 소프트웨어

- 가상머신과 차이점
> 도커는 호스트 OS 커널을 공유하는 운영체제 수준의 가벼운 가상화이고 가상머신(VM)은 하이퍼바이저를 통해 독립된 게스트OS 전체를 실행하는 하드웨어 수준의 가상화

- 설치법
> wsl --install
> winget install -e --id Docker.DockerDesktop

### 이미지 다운로드와 컨테이너 실행
# 이미지 다운로드(불러오는) 명령어 
docker pull 이미지명
# 또는 
doker run 이미지명 # 을 해도, pull도 알아서 받아오고 실행이 된다 

# 컨테이너 실행 명령어
doker run 이미지명 #exec를 쓸 필요 없는 이미지들만 

### 컨테이너 관리 명령어
# 컨테이너 켜진게 있는지 확인
docker ps 

# 컨테이너 꺼진것도 보고 싶다면 
docker ps -a

# 실행중인 컨테이너로 들어가고싶을때(리눅스, 데이터베이스 등)
docker exec

# 컨테이너가 남긴 기록을 확인하고싶을때
docker logs

# 실행된 컨테이너를 끄고싶을때
docker stop

# 종료된 컨테이너를 실행하고싶을때
docker start

# 종료된 컨테이너를 완전 삭제하고싶을때
docker rm

# 이미지를 지우고싶을때 
docker rmi

### Volume과 데이터 영속성
- 볼륨
> 볼륨은 데이터를 저장하고 보존하는 공간(저장소)

- 볼륨 마운트
> 그 저장소를 특정 경로(디렉터리)에 연결해 접근할 수 있게 만드는 작업 

- 컨테이너 삭제와 데이터 보존의 차이 
> 삭제를 하면 컨테이너 내부의 쓰기 가능 계층에 저장된 데이터는 지워지는데, 볼륨이나 바인드 마운트로 외부에 연결한 데이터는 보존된다. 이게 볼륨을 쓰는 핵심적인 이유.
# 볼륨 생성
docker volume create 볼륨명

# 볼륨 목록 조회 
docker volume ls

# 볼륨 상세 정보 확인
docker volume inspect 볼륨명

# 특정 볼륨 삭제 
docker volume rm 볼륨명

# 미사용 볼륨 일괄 삭제 
docker volume prune

# 볼륨 마운트 실행
docker run -v 볼륨명:컨테이너경로 이미지명

# 읽기 전용 마운트
docker run -v 볼륨명: 컨테이너 경로:ro 이미지명

### Docker Compose
- YAML 구성
> yml파일에 서비스, 네트워크, 볼륨을 정의해 다중 컨테이너 앱을 관리할때 씀 

- docker compose up -d
> 위와 같이 프로젝트 폴더에 yml파일이 있으면, 이 명령어를 써서 컨테이너를 바로 켤 수 있다 

- docker compose down 
> up이 실행이라면, down은 중지하고 삭제하는 명령어

- docker compose down -v
> 이 명령어는 볼륨까지 삭제를 하는 명령어 

- docker compose exec
> DB접속, 컨테이너 내부 셀로 바로 접속하기 위해 쓰는 명령어
------------

## Part 3. 데이터베이스 핵심 개념 

### 관계형 데이터베이스의 기본 구조
- DBMS
> Database Management System.
> 데이터를 저장, 조회, 수정, 삭제하고 체계적으로 관리할 수 있게 해주는 소프트웨어
> DB를 생성하고 운영, 관리하는 소프트웨어 시스템 

- 데이터베이스(DB)
> 여러 사용자나 응용 프로그램이 함께 사용하고 효율적으로 관리할 수 있도록 체계적으로 저장한 데이터의 집합. 
> 데이터베이스 관리 시스템(DBMS)을 통해 저장, 조회, 수정, 삭제와 백업, 보안, 동시성 제어를 수행 

- 테이블
> 데이터를 2차원 표(행과 열) 형태로 조직하여 저장하는 기본 단위 

- 행(Row/레코드/튜플)
> 가로 방향으로 존재하는 실질적인 데이터의 한 단위 (예: 특정 사용자 1명의 정보)

- 열(Column/필드/속성)
> 세로 방향의 데이터 구조로 저장할 데이터의 타입과 이름(예: 이름, 나이, 이메일)을 미리 정의

- 셀(Cell)
> 행과 열이 교차하는 지점으로 구체적인 데이터 값이 들어가는 최소 단위 

- 스키마(Schema)
> 데이터베이스에 데이터가 저장되는 구조와 규칙, 제약 조건을 정의한 설계도(메타데이터). 
> 건물 짓기 전 건축 도면 같음 
> 외부스키마/개념스키마/내부스키마가 있음 

### SQL의 종류와 역할
- SQL (Structured Query Language, 구조화 질의어)
> 관계형 데이터베이스 관리 시스템(RDBMS)에서 데이터를 저장, 조회, 수정, 삭제하고 구조를 관리하기 위해 사용하는 언어 
> SELECT(조회)/INSERT(추가)/UPDATE(수정)/DELETE(삭제) 역할이 있고
> 구조 정의 및 제어(DDL, DCL, TCL)를 한다

- DDL(Data Definition Language, 데이터 정의어)의 역할
> 데이터베이스의 테이블, 인덱스, 스키마, 뷰 등 구조를 생성, 수정, 삭제하는 SQL명령어 집합

- DML(Data Manipulation Language, 데이터 조작어)의 역할
> 데이터베이스 테이블에 저장된 데이터를 조회, 삽입, 수정, 삭제하는 SQL 명령어 집합

- DQL(Data Query Language, 데이터질의어)의 역할
> 데이터베이스의 테이블이나 뷰에서 데이터를 검색(조회)하는데 사용하는 SQL 명령어 분류

- CREATE의 역할
> 데이터베이스나 테이블 같은 데이터베이스 객체를 정의하고 생성하는 DDL 명령어

- INSERT INTO의 역할
> 테이블에 새 행(레코드)을 추가

- SELECT의 역할
> 데이터베이스에 저장된 데이터를 조회(Read)하기 위해 가장 기본적이고 빈번하게 사용되는 DML명령어


### 데이터 타입과 제약조건
- INTEGER
> 소수점이 없는 정수를 저장하는 기본 데이터 타입

- VARCHAR
> 가변 길이 문자열을 저장하는 데이터 타입

- DATE
> 날짜 정보를 저장하는 자료형. (mysql, sql server, postgresql, 표준sql은)연월일만 저장하고 시간정보는 포함하지 않음. 

- NUMERIC
> 오차가 없는 고정 소수점 숫자를 저장하는 데이터 타입

- NOT NULL
> 데이터타입 뒤에 붙는 제약 조건(Constraint)으로 해당 컬럼에 NULL(값이 정해지지 않은 상태)이 들어가는 것을 금지 

- CHECK
> 입력 값이 지정한 조건이나 범위를 만족하는지 검사

### 기본 키와 외래 키
- PRIMARY KEY(기본키)
> 각 행을 고유하게 식별. 

- FOREIGN KEY(외래키)
> 다른 테이블의 PRIMARY KEY또는 UNIQUE 컬럼을 참조해 참조 무결성을 유지 

- REFERENCES
> 한 테이블의 컬럼이 다른 테이블의 특정 컬럼을 참조하도록 설정하여 외래키(Foreign Key, FK) 관계를 만드는데 사용. 이를 통해 참조무결성 유지.

- UNIQUE
> 특정 열(또는 열 조합)에 중복된 값이 들어가지 않도록 막는 규칙 

### 테이블 간 관계와 ERD
- ERD(Entity Relationship Diagram)
> DB에서 존재하는 것들의 관계를 도표로 나타낸 것

- 1:1 (one to one, 1대1)
> 한 엔터티(테이블)의 레코드 1개가 다른 엔터티의 레코드 1개와의 연결
> 컬럼을 분리하거나 민감 정보, 대용량 데이터를 나눌때 씀. 외래키를 한쪽 테이블에 두고 unique 제약을 검 

- 1:M/1:N (one to many, 1대다)
> 한 엔터티의 레코드 1개가 다른 엔터티의 여러 레코드(0개 이상)와 연결
> 관계형 데이터베이스에서 가장 흔한 형태 
> 학교(1)와 학생(M), 부서(1)와 직원(M), 주문(1)과 주문항목(M)
> 다(M)쪽 테이블에 일(1)쪽의 기본 키를 외래 키로 추가 

- M:N/N:M (many to many, 다대다)
> 양쪽 엔터티의 레코드 여러 개가 서로 여러 개와 연결
> 학생(M)과 수강 과목(N), 상품(M)과 태그(N), 직원(M)과 프로젝트(N)
> 관계형 DB 테이블로는 직접 구현하기 어려워 두 테이블을 1:M관계로 풀어내는 중간 연결 테이블(매핑/교차 테이블)을 만들어 설계함 

- 중간 테이블
> 다대다(N:M/M:N)관계를 관계형 데이터베이스(RDB)에 구현하기 위해 두 테이블 사이에 두는 연결 테이블(조인 테이블, 매핑 테이블)

- 참조 무결성
> ERD와 관계형 데이터베이스에서 외래키(FK)값이 참조하는 부모 테이블의 기본키(PK)값과 일치하거나 NULL이어야 한다는 규칙. 존재하지 않는 데이터를 잘못 참조하는 '고아 데이터'를 막음 

- ON DELTE CASCADE
> 부모 테이블의 행이 삭제 될 떄 해당 외래 키(FK)를 참조하는 자식 테이블의 관련 행도 자동으로 함께 삭제되도록 지정하는 외래 키 제약 조건 옵션 
------------

## Part 4. PostgreSQL과 SQL 핵심 쿼리

### 데이터 조회와 조건 검색
- SELECT
> SQL과 PostgreSQL에서 테이블의 데이터를 조회(SELECT-FROM)하고, WHERE절로 원하는 조건의 행만 골라내는 핵심 구문

- WHERE
> SELECT로 데이터를 조회할 때 불린(참/거짓) 조건을 지정해 원하는 행만 필터링하는 핵심 구문. 논리적 실행 순서에서는 FROM 다음, SELECT와 GROUP BY 이전에 동작 

- LIKE
> WHERE 절에서 문자열 패턴을 기준으로 데이터를 필터링하는 연산자

- IN
> SELECT와 WHERE절에서 특정 열의 값이 지정된 목록(값의 나열 또는 서브쿼리 결과)중 하나와 일치하는지 검사하는 조건 연산자. 여러개의 OR조건을 간결하게 줄여줌 

- BETWEEN
> 컬럼 >= 시작값 AND 컬럼 <= 끝값처럼 양쪽 경계값을 모두 포함하는 범위를 조회할때 사용

- IS NULL
> 컬럼의 값이 비어 있거나 알 수 없는 상태(NULL)인 행을 조회할때 사용하는 조건 연산자. NULL은 숫자 0이나 문자열('')과 다르며, =연산자로는 비교할 수 없으므로 반드시 IS NULL또는 IS NOT NULL을 사용해야함 

- ORDER BY
> SELECT 쿼리로 조회한 결과를 지정한 열이나 표현식 기준으로 오름차순(ASC, 기본값)또는 내림차순(DESC)정렬하는 절. 쿼리 작성 시 보통 가장 마지막에 위치. 생략하면 정렬 순서가 보장되지 않음 

### 집계 함수와 그룹화
- COUNT
> 데이터를 묶은 뒤 각 그룹에 속한 행 또는 값의 개수를 세는 집계 함수

- SUM
> 데이터를 특정 기준(GROUP BY)으로 나눈뒤 각 그룹에 속한 숫자 값들의 합계를계산하는 함수

- AVG
> 숫자 데이터의 평균을 계산하는 집계 함수. GROUP BY와 함께 쓰면 지정한 기준(그룹)별로 평균을 구할 수 있음 

- GROUP BY
> 특정 열의 값이 같은 행끼리 그룹으로 묶고, 각 그룹마다 집계 함수(Aggregate Function)를 적용해 요약 결과를 만드는 절

- HAVING
> GROUP BY로 묶인 그룹별 집계 결과에 조건을 걸어 원하는 그룹만 필터링 하는 구문

- WHERE 와 HAVING의 차이
> WHERE는 GROUP BY 로 묶기전에 개별 행을 걸러내고, HAVING은 GROUP BY로 집계한 후에 그룹 결과를 걸러낸다 

### 테이블 결합 JOIN
- INNER JOIN
> 두 개 이상의 테이블에서 ON 조건이 일치하는 행만 결합해 반환하는 SQL조인 방식. 집합론으로 보면 두 테이블의 교집합에 해당. 한쪽에만 있는 데이터나 조건에 맞지 않는 행은 결과에서 제외

- LEFT JOIN
> 왼쪽 테이블의 모든 행을 유지하면서 오른쪽 테이블에서 조인 조건이 일치하는 행을 결합하고 일치하지 않는 부분은 NULL로 채우는 SQL 결합 방식. 

- ON
> 두 테이블을 결합할 때 어떤 열을 기준으로 어떻게 연결할지 지정하는 조인 조건 

- 테이블 별칭과 테이블 조회 
> 테이블 별칭(Alias)은 긴 테이블 이름을 줄여 가독성을 높이고 여러 테이블에 같은 이름의 컬럼이 있을때 모호함을 피하기 위해 사용 


### 서브쿼리
- WHERE절 서브쿼리
> 메인 쿼리의 데이터를 필터링하기 위해 조건절 안에 작성하는 하위 쿼리

- IN
> 서브쿼리가 반환하는 여러 행(다중 행)의 결과 중 하나라도 일치하는 데이터를 조회할 때 사용

- EXISTS
> 서브쿼리 결과가 1건 이상 존재하면 TRUE, 없으면 FALSE를 반환하는 논리 연산자. 실제 값을 꺼내기보다 조건을 만족하는 행이 있는지 여부만 확인 

- FROM절 인라인 뷰
> 쿼리 실행 시 임시 테이블(동적뷰)처럼 동작. 데이터베이스 객체로 저장되지 않고 해당 SLQ이 실행될 때만 만들어지며 바깥 쿼리에서 하나의 테이블처럼 컬럼과 행을 참조할 수 있다.

### 데이터 변경과 Python 연동
- INSERT
> 파이썬에서 데이터베이스에 새 데이터를 추가할 때는 SQL의 INSERT INTO문을 실행한 뒤 반드시 commit()을 호출해 변경 사항을 확정해야 한다 

- UPDATE
> 파이썬에서 데이터베이스 연동을 통해 데이터를 변경할 때는 SQL UPDATE쿼리 실행과 변경사항 commit()이 핵심. 

- DELETE
> 파이썬에서 데이터베이스와 연동해 데이터를 삭제할때는 SQL DELETE문을 실행한뒤 commit()으로 변경사항을 반영해야한다. WHERE절을 생략하면 테이블의 모든 데이터가 삭제 되므로 주의 

- RETURNING
> 데이터변경(INSERT, UPDATE, DELETE, MERGE)쿼리 뒤에 RETURNING절을 붙이면 별도의 SELECT쿼리 없이 변경되거나 생성, 삭제된 행의 데이터를 파이썬 드라이버로 바로 돌려받을 수 있다. 

- psycopg의 매개변수 바인딩
> 파이썬과 PostgreSQL연동시 psycopg에서 SQL 인젝션(Injection)을 방지하고 데이터 타입을 안전하게 처리하기 위해 사용하는 매개변수 바인딩(Parameter Binding) 방법 
------------

## Part 5. NumPy 핵심 연산
=====================================
### NumPy 배열의 개념
- Python 리스트와 ndarray의 차이
> ndarray는 모든 요소가 동일한 자료형(dtype)을 갖는 다차원 수치 배열이며, 파이썬 list는 서로 다른 자료형과 가변 길이를 지원하는 범용 시퀀스 컨테이너

- 배열 생성
> 모든 원소가 같은 자료형(dtype)을 가지며 메모리에 연속적으로 저장되는 다차원 배열 객체로, np.array()나 전용 생성 함수로 만들 수 있다 
### 배열의 구조와 속성
- shape
> 배열의 각 차원(축)에 몇 개의 원소가 들어있는지를 나타내는 튜플형태의 속성. 

- dtype
> 각 원소가 저장하는 데이터 타입과 메모리 해석 방식을 나타내는 속성
### 인덱싱과 슬라이싱
- 1차원, 2차원 배열의 요소 접근과 부분 배열 선택
> 특정 위치의 단일 요소나 행, 열에 접근해 차원을 줄이고 슬라이싱은 시작:끝:간격 범위로 부분 배열을 선택해 차원을 유지. 2차원 배열에서는 쉼표로 [행, 열] (0번 축, 1번 축)을 함께 지정할 수 있다 
### 벡터 연산과 브로드캐스팅
- 벡터 연산(Vectorization)
> 파이썬 반복문(for)없이 배열 전체에 대해 요소별 연산을 빠르게 처리하는 기능

- 브로드캐스팅(Broadcasting)
> 형태(shape)가 다른 배열 간에도 연산이 가능하도록 작은 배열의 차원을 자동으로 늘려 맞추는 기능

- 요소별 연산
> 브로드캐스팅은 크기가 다른 배열의 차원을 맞춰 요소별 연산이 가능하게 확장하는 기능이 있다

- 배열 간 연산
> 벡터화 연산은 반복문 없이 배열 전체에 요소별 확산을 수행하는 기능

- 반복문 없는 계산
> 벡터화 연산과 브로드캐스팅은 파이썬의 명시적인 for 반복문 없이 배열 전체나 서로 다른 크기의 배열 간 연산을 한 번에 처리하는 기법 
### 통계 연산과 조건 필터링
- sum()
> 조건식을 쓰면 결과로 True(1)와 False(0)가 반환되는데 여기에 sum()을 적용해 조건을 만족하는 데이터의 개수를 쉽게 구할 수 있다 

- mean()
> 데이터의 평균값(산술 평균)을 계산할때 사용하며 조건 필터링과 결합하면 특정 조건을 만족하는 그룹만의 평균을 쉽게 구할 수 있다. 

- max()
> 그룹별 최댓값을 구하는 통계 연산과 특정 최댓값 조건에 맞는 데이터를 추출하는 조건 필터링에 핵심적으로 사용 

- min()
> 데이터 분석 및 프로그래밍에서 가장 작은 값(최솟값)을 찾는데 사용되며 통계연산과 조건 필터링에서 핵심적인 역할을 함 
------------

## Part 6. Panda 데이터 분석
=====================================
### Series와 DataFrame
- Pandas의 핵심 자료구조
> Series(시리즈)와 DataFrame(데이터프레임) 두가지. 

- Series(1차원 배열)
> 인덱스(행 라벨)와 데이터 값이 1:1로 대응하는 1차원 구조 
> 리스트, 딕셔너리, NumPy 배열 등으로 pd.Series()를 호출해 만듦

- DataFrame (2차원 표)
> 행(index)과 열(columns)로 이루어진 2차원 테이블이며 각 열은 하나의 Series로 볼 수 있다. 
> 열 이름을 키로 하는 딕셔너리, 2차원 배열, Series모음 등으로 pd.DataFrame()을 호출해 만듦

- 열과 행의 개념
> 열(Column)은 같은 성질의 값이나 속성을 세로로 모은 단위이고 행(Row)은 각 데이터 개체나 관측치 하나를 가로로 묶은 단위 
### 데이터 선택과 불리언 인덱싱
- 데이터 선택
> 열/행 위치, 라벨 기준 선택과 조건 기반 필터링(불리언 인덱싱)으로 나뉨

- df["컬럼"]
> pandas DataFrame에서 특정 컬럼 하나를 1차원 Series형태로 선택하거나 해당 컬럼의 값을 수정, 추가할 때 사용하는 기본 문법 

- loc
> 행(row)과 열(column)의 레이블(이름)을 기준으로 데이터를 조회, 필터링, 수정하는 인덱싱 기능 

- 조건을 이용한 행 필터링 
> DataFrame에서 특정 조건식을 만족(True)하는 행(row)만 골라내어 추출하는 작업. 주로 각 행의 참/거짓 여부를 판별한 불리언 (Boolean) Series를 인덱스에 전달하는 불리언 인덱싱 방식으로 동작 

### 데이터 정렬과 집계
- 데이터 정렬
> 데이터 정렬은 sort_values()와 sort_index()로 수항해며 데이터 집계는 groupby()와 집계 함수(mean(), sum(), count(), agg() 등)로 요약 통계를 계산 

- sort_values()
> 값 기준 정렬. 특정 열이나 여러 열의 값을 기준으로 행을 정렬. ascending=True가 기본값(오름차순)이며 ascending=False로 내림차순 정렬 

- groupby()
> 그룹화 및 기본 집계. 하나 이상의 열을 기준으로 그룹을 나눈 뒤 합계, 평균, 개수, 최댓값, 최솟값등을 구함 

- value_counts()
> 데이터 내 고유한 값(범주)별 출현 빈도를 계산, 기본적으로 내림차순(많은 순서)으로 정렬해주는 집계 메서드 
------------