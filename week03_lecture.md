# 3주차: 변수와 자료형 심화 및 연산자 활용 규칙
**총 강의시간: 3시간 20분 (200분)**
- 강의: 120분 (3부로 구성)
- 휴식: 20분 (10분씩 2회)
- 실습: 60분

---

## 🎯 1부: 변수가 왜 필요할까? - 복잡한 세상을 다루는 방법 (40분)

### 📌 핵심 개념 1: 지난 주 복습 - 우리가 도달한 지점 (5분)

#### 🔄 **지금까지의 여정**

**1주차**: 프로그래밍의 3대 마법 구조 발견
- 순차: "차례대로 하나씩"
- 선택: "상황에 따라 다르게"  
- 반복: "조건 만족할 때까지 계속"

**2주차**: 어디서든 코딩할 수 있는 환경 구축
- ☁️ Google Colab: 브라우저만으로 즉시 코딩
- 🐳 Docker: 전문적인 개발환경 구성

**오늘 해결할 문제**: 
더 복잡하고 실용적인 프로그램을 만들고 싶은데, 지금까지 배운 것만으로는 부족하다!

### 📌 핵심 개념 2: 왜 변수가 필요한가? - 복잡한 계산의 문제 (15분)

#### 🤔 **간단한 계산은 쉽다**

**일상 속 간단한 계산:**
```python
# 편의점에서 물건 하나 사기
price = 1200
print(f"지불할 금액: {price}원")
```

**하지만 현실은 더 복잡하다:**

#### 🏗️ **복잡한 도형의 면적 계산 문제**

**상황**: 놀이터 설계 - 여러 도형이 겹쳐진 복잡한 영역의 면적 구하기

```
🏞️ 놀이터 부지 계획:
┌─────────────────┐
│     직사각형     │
│  ┌─────┐        │
│  │원형  │  삼각형 │
│  │분수대│   /\    │
│  └─────┘  /  \   │
│           /____\  │
└─────────────────┘

최종 면적 = 직사각형 - 원형분수대 + 삼각형놀이터
```

**변수 없이 한 번에 계산하려면:**
```python
# 😱 끔찍한 한 줄 계산 (변수 없이)
area = (20 * 15) - (3.14159 * 5 * 5) + (0.5 * 8 * 6)
print(f"놀이터 면적: {area}")

# 문제점들:
# 1. 숫자들이 뭘 의미하는지 모르겠음 🤷‍♂️
# 2. 실수하기 너무 쉬움 😰
# 3. 나중에 수정하기 어려움 😡
# 4. 다른 사람이 이해하기 어려움 🤯
```

**변수를 사용한 명확한 계산:**
```python
# ✅ 변수로 단계별 계산 (명확하고 안전함)
print("🏞️ 놀이터 부지 면적 계산")
print("=" * 30)

# 1단계: 전체 직사각형 부지
site_width = 20    # 부지 가로 (미터)
site_height = 15   # 부지 세로 (미터)
total_site_area = site_width * site_height
print(f"전체 부지: {site_width}m × {site_height}m = {total_site_area}㎡")

# 2단계: 원형 분수대 (제외할 영역)
fountain_radius = 5  # 분수대 반지름 (미터)
pi = 3.14159
fountain_area = pi * fountain_radius * fountain_radius
print(f"분수대: 반지름 {fountain_radius}m = {fountain_area:.1f}㎡")

# 3단계: 삼각형 놀이터 (추가할 영역)
triangle_base = 8    # 삼각형 밑변 (미터)
triangle_height = 6  # 삼각형 높이 (미터)
triangle_area = 0.5 * triangle_base * triangle_height
print(f"삼각형 놀이터: 밑변 {triangle_base}m, 높이 {triangle_height}m = {triangle_area}㎡")

# 4단계: 최종 계산
usable_area = total_site_area - fountain_area + triangle_area
print("-" * 30)
print(f"사용 가능한 놀이터 면적: {usable_area:.1f}㎡")

# 5단계: 추가 분석
area_per_child = 10  # 어린이 1명당 필요한 면적 (㎡)
max_children = int(usable_area / area_per_child)
print(f"동시에 놀 수 있는 어린이 수: 약 {max_children}명")
```

#### 💡 **변수의 첫 번째 필요성: 중간 결과 보관소**

**변수 = 계산 과정의 메모장**
1. **복잡한 계산을 단계별로 나누기**
2. **각 단계의 결과를 임시 저장**
3. **저장된 결과를 다음 계산에 활용**
4. **실수 줄이고 가독성 향상**

**더 복잡한 예시: 건물 설계**
```python
# 🏢 아파트 건설비 계산
print("🏢 아파트 건설비 계산")
print("=" * 25)

# 기본 정보
floors = 15           # 층 수
units_per_floor = 4   # 층당 세대 수
total_units = floors * units_per_floor
print(f"총 세대 수: {floors}층 × {units_per_floor}세대 = {total_units}세대")

# 공사비 계산
structure_cost_per_unit = 80000000    # 세대당 구조 공사비
interior_cost_per_unit = 45000000     # 세대당 내부 공사비
total_construction_cost = (structure_cost_per_unit + interior_cost_per_unit) * total_units

# 부대비용
land_cost = 12000000000        # 토지비
design_cost = 800000000        # 설계비
management_cost = 600000000    # 공사 관리비
other_costs = land_cost + design_cost + management_cost

# 최종 총비용
total_project_cost = total_construction_cost + other_costs

print(f"건설비: {total_construction_cost:,}원")
print(f"부대비용: {other_costs:,}원")
print(f"총 프로젝트 비용: {total_project_cost:,}원")

# 분석
cost_per_unit = total_project_cost / total_units
print(f"세대당 평균 비용: {cost_per_unit:,.0f}원")
```

### 📌 핵심 개념 3: 결정되지 않은 상황 다루기 - 동적 프로그래밍의 시작 (20분)

#### 🎲 **미리 정해지지 않은 상황들**

**일상 속 불확실한 상황들:**
- 사용자가 어떤 숫자를 입력할지 모름
- 오늘 날씨가 어떨지 모름  
- 게임에서 상대방이 어떤 선택을 할지 모름
- 온라인 쇼핑에서 어떤 상품을 선택할지 모름

**이런 상황에서 변수가 필수인 이유:**
```python
# ❌ 미리 정해진 값으로만 프로그램을 만들면
print("5 + 3 = 8")  # 항상 같은 결과만 나옴

# ✅ 변수를 사용하면 다양한 상황에 대응 가능
num1 = ???  # 사용자가 입력할 첫 번째 숫자
num2 = ???  # 사용자가 입력할 두 번째 숫자
result = num1 + num2  # 입력에 따라 결과가 달라짐
```

#### 🎯 **실용적 예제: 숫자야구 게임 설계**

**게임 규칙:**
1. 컴퓨터가 3자리 숫자를 생각함 (예: 742)
2. 플레이어가 3자리 숫자를 추측 (예: 123)
3. 컴퓨터가 힌트를 줌:
   - 스트라이크: 숫자와 위치가 모두 맞음
   - 볼: 숫자는 맞지만 위치가 틀림
4. 3스트라이크가 될 때까지 반복

**왜 변수가 필요한가?**
```python
# 🎮 숫자야구 게임에서 변수의 역할
print("🎮 숫자야구 게임")
print("=" * 20)

# 변수들이 필요한 이유들:
secret_number = "742"    # 컴퓨터의 비밀 숫자 (매 게임마다 다름)
player_guess = "???"     # 플레이어의 추측 (매번 다름)
attempt_count = 0        # 시도 횟수 (계속 증가)
game_over = False        # 게임 종료 여부 (상황에 따라 변함)

# 각 자리수 비교를 위한 변수들
secret_1 = secret_number[0]    # 비밀번호 첫째 자리
secret_2 = secret_number[1]    # 비밀번호 둘째 자리  
secret_3 = secret_number[2]    # 비밀번호 셋째 자리

print(f"비밀 숫자가 정해졌습니다! (힌트: {len(secret_number)}자리)")
print("추측해보세요!")
```

**간단한 버전으로 동작 원리 설명:**
```python
# 🎯 숫자야구 게임 (간단 버전)
print("🎮 숫자야구 게임 시뮬레이션")
print("=" * 35)

# 게임 설정 (변수로 관리)
secret_answer = "742"    # 정답 (실제로는 랜덤 생성)
max_attempts = 5         # 최대 시도 횟수

# 게임 진행 상황을 저장하는 변수들
current_attempt = 1
game_finished = False

print(f"🎯 목표: 3자리 숫자 맞추기")
print(f"📝 최대 {max_attempts}번 시도 가능")
print("=" * 35)

# 플레이어의 시도들 (시뮬레이션)
player_guesses = ["123", "456", "741", "742"]  # 실제로는 사용자 입력

for guess in player_guesses:
    print(f"\n{current_attempt}번째 시도: {guess}")
    
    # 각 자리 비교를 위한 변수들
    strike_count = 0    # 스트라이크 개수
    ball_count = 0      # 볼 개수
    
    # 첫 번째 자리 검사
    if guess[0] == secret_answer[0]:
        strike_count = strike_count + 1
        print(f"  첫째 자리 '{guess[0]}': 스트라이크! ⚾")
    elif guess[0] in secret_answer:
        ball_count = ball_count + 1
        print(f"  첫째 자리 '{guess[0]}': 볼! 🥎")
    else:
        print(f"  첫째 자리 '{guess[0]}': 아웃! ❌")
    
    # 두 번째 자리 검사
    if guess[1] == secret_answer[1]:
        strike_count = strike_count + 1
        print(f"  둘째 자리 '{guess[1]}': 스트라이크! ⚾")
    elif guess[1] in secret_answer:
        ball_count = ball_count + 1
        print(f"  둘째 자리 '{guess[1]}': 볼! 🥎")
    else:
        print(f"  둘째 자리 '{guess[1]}': 아웃! ❌")
    
    # 세 번째 자리 검사
    if guess[2] == secret_answer[2]:
        strike_count = strike_count + 1
        print(f"  셋째 자리 '{guess[2]}': 스트라이크! ⚾")
    elif guess[2] in secret_answer:
        ball_count = ball_count + 1
        print(f"  셋째 자리 '{guess[2]}': 볼! 🥎")
    else:
        print(f"  셋째 자리 '{guess[2]}': 아웃! ❌")
    
    # 결과 판정
    print(f"  결과: {strike_count}스트라이크 {ball_count}볼")
    
    # 게임 종료 조건 확인
    if strike_count == 3:
        print(f"\n🎉 정답입니다! {current_attempt}번 만에 맞추셨네요!")
        game_finished = True
        break
    elif current_attempt >= max_attempts:
        print(f"\n😭 게임 오버! 정답은 {secret_answer}였습니다.")
        game_finished = True
        break
    
    current_attempt = current_attempt + 1

if not game_finished:
    print(f"\n게임 계속 진행 중...")
```

#### 💡 **변수의 두 번째 필요성: 상황 대응 능력**

**변수 = 프로그램의 기억력과 적응력**
1. **사용자 입력 저장**: 무엇을 입력할지 미리 모름
2. **게임 상태 추적**: 현재 점수, 레벨, 생명 등
3. **계산 결과 활용**: 이전 결과를 바탕으로 다음 동작 결정
4. **조건부 실행**: 상황에 따라 다른 처리

**변수가 없다면:**
```python
# ❌ 변수 없이는 불가능한 것들
print("항상 742만 정답인 게임")  # 재미없음
print("항상 김철수만 1등")        # 의미없음
print("항상 1200원만 계산")       # 쓸모없음
```

**변수가 있다면:**
```python
# ✅ 변수로 가능한 것들
user_name = input("이름을 입력하세요: ")        # 매번 다른 이름
difficulty = input("난이도를 선택하세요: ")     # 매번 다른 설정
score = 0                                      # 게임하면서 계속 변함
level = 1                                      # 실력에 따라 증가

print(f"{user_name}님, {difficulty} 모드에서 게임을 시작합니다!")
print(f"현재 레벨: {level}, 점수: {score}")
```

---

## ☕ 휴식 시간 (10분)

---

## 🎯 2부: 자료형 심화와 문자열의 마법 (40분)

### 📌 핵심 개념 1: 자료형별 특징과 활용법 - 상세 분석 (15분)

#### 📊 **자료형 = 데이터의 종류와 처리 방법**

**일상에서의 "종류" 개념:**
```
📚 도서관에서 책 분류:
- 소설책: 재미있게 읽기 위해
- 참고서: 문제 풀기 위해  
- 요리책: 따라하기 위해
- 사전: 찾아보기 위해

각각 사용 방법이 다름!
```

**프로그래밍에서의 자료형도 마찬가지:**

#### 📝 **문자열(String) - 텍스트 데이터의 모든 것**

**기본 활용:**
```python
# 🔤 문자열의 다양한 활용
print("📝 문자열 자료형 마스터하기")
print("=" * 30)

# 기본 문자열
name = "김파이썬"
greeting = "안녕하세요!"
sentence = "오늘은 파이썬을 배우는 날입니다."

print(f"이름: {name}")
print(f"인사: {greeting}")
print(f"문장: {sentence}")

# 문자열 길이 확인
print(f"\n📏 길이 측정:")
print(f"이름 길이: {len(name)}글자")
print(f"인사 길이: {len(greeting)}글자")  
print(f"문장 길이: {len(sentence)}글자")

# 문자열 합치기 (연결)
full_greeting = greeting + " " + name + "님!"
print(f"\n🔗 문자열 연결: {full_greeting}")

# 문자열 반복
excited = "와! " * 5
print(f"🎉 반복: {excited}")

# 문자열 일부 가져오기 (슬라이싱)
print(f"\n✂️ 문자열 자르기:")
print(f"이름의 첫 글자: {name[0]}")
print(f"이름의 마지막 글자: {name[-1]}")
print(f"문장의 앞 5글자: {sentence[:5]}")
print(f"문장의 뒤 5글자: {sentence[-5:]}")
```

**문자열 메서드 활용:**
```python
# 🔧 문자열 메서드로 다양한 작업하기
text = "Python Programming"

print("🔧 문자열 메서드 실습")
print("=" * 25)
print(f"원본: {text}")

# 대소문자 변환
print(f"대문자: {text.upper()}")
print(f"소문자: {text.lower()}")
print(f"첫글자만 대문자: {text.capitalize()}")

# 문자열 찾기와 바꾸기
print(f"\n🔍 'Python' 찾기: {text.find('Python')}번째 위치")
print(f"'Python'을 '파이썬'으로 바꾸기: {text.replace('Python', '파이썬')}")

# 문자열 분리와 결합
words = text.split()  # 공백으로 분리
print(f"단어 분리: {words}")
joined = "-".join(words)  # '-'로 결합
print(f"하이픈으로 결합: {joined}")

# 문자열 검사
print(f"\n✅ 문자열 검사:")
print(f"'Python'이 포함되어 있나? {'Python' in text}")
print(f"'Java'가 포함되어 있나? {'Java' in text}")
print(f"문자열이 'P'로 시작하나? {text.startswith('P')}")
print(f"문자열이 'ing'로 끝나나? {text.endswith('ing')}")
```

#### 🔢 **숫자형 - 정수와 실수의 차이점**

**정수(int)와 실수(float)의 차이:**
```python
# 🔢 숫자형 자료형 완전 분석
print("🔢 숫자형 자료형 분석")
print("=" * 25)

# 정수 (Integer)
student_count = 30        # 학생 수 (자연수)
temperature = -5          # 온도 (음수 가능)
floor_number = 0          # 층수 (0 포함)

print("🔢 정수형 (int):")
print(f"학생 수: {student_count} (타입: {type(student_count)})")
print(f"온도: {temperature}°C (타입: {type(temperature)})")
print(f"층수: {floor_number}층 (타입: {type(floor_number)})")

# 실수 (Float)
height = 175.5           # 키 (소수점 있음)
pi = 3.14159            # 원주율
account_balance = 1234.56  # 계좌 잔액

print(f"\n💰 실수형 (float):")
print(f"키: {height}cm (타입: {type(height)})")
print(f"원주율: {pi} (타입: {type(pi)})")
print(f"잔액: {account_balance}원 (타입: {type(account_balance)})")

# 숫자형 연산의 특징
print(f"\n🧮 연산 결과의 타입:")
int_result = 10 + 5      # 정수 + 정수 = 정수
float_result = 10.0 + 5  # 실수 + 정수 = 실수
division_result = 10 / 3  # 나눗셈은 항상 실수

print(f"10 + 5 = {int_result} (타입: {type(int_result)})")
print(f"10.0 + 5 = {float_result} (타입: {type(float_result)})")
print(f"10 / 3 = {division_result} (타입: {type(division_result)})")

# 타입 변환
print(f"\n🔄 타입 변환:")
number_str = "123"
number_int = int(number_str)     # 문자열 → 정수
number_float = float(number_str)  # 문자열 → 실수

print(f"문자열 '{number_str}' → 정수 {number_int}")
print(f"문자열 '{number_str}' → 실수 {number_float}")
```

#### ✅ **불린형 - 참/거짓의 논리**

**불린형의 실용적 활용:**
```python
# ✅ 불린형 (Boolean) - 논리의 세계
print("✅ 불린형 마스터하기")
print("=" * 20)

# 기본 불린값
is_student = True
has_homework = False
is_weekend = True

print(f"학생인가요? {is_student}")
print(f"숙제가 있나요? {has_homework}")
print(f"주말인가요? {is_weekend}")

# 비교 연산의 결과도 불린형
age = 20
print(f"\n🔍 비교 연산 결과:")
print(f"나이가 18 이상인가? {age >= 18}")
print(f"나이가 65 이상인가? {age >= 65}")
print(f"나이가 20과 같은가? {age == 20}")

# 논리 연산
can_drive = age >= 18 and has_homework == False
can_party = is_weekend and age >= 20

print(f"\n🚗 운전 가능? {can_drive}")
print(f"🎉 파티 가능? {can_party}")

# 불린값을 활용한 조건문
if is_student and is_weekend:
    print("\n📚 주말이지만 공부해야겠어요!")
elif is_weekend:
    print("\n🎮 주말이니까 쉬어도 돼요!")
else:
    print("\n💼 평일이니까 열심히 해요!")
```

### 📌 핵심 개념 2: 문자열 포맷팅의 진화 - 3세대 비교 (15분)

#### 📝 **1세대: % 포맷팅 (과거의 방식)**

```python
# 📜 1세대: % 포맷팅 (오래된 방식)
print("📜 1세대: % 포맷팅")
print("=" * 20)

name = "김학생"
age = 20
score = 85.7

# % 포맷팅 방식
old_style = "이름: %s, 나이: %d, 점수: %.1f" % (name, age, score)
print(old_style)

# 장점: 간단함
# 단점: 복잡해지면 읽기 어려움, 순서 꼬이기 쉬움

# 복잡한 예시
product = "노트북"
price = 1200000
discount = 0.15
final_price = price * (1 - discount)

old_complex = "%s 원가 %d원, 할인율 %.0f%%, 최종가격 %d원" % (
    product, price, discount * 100, final_price
)
print(f"복잡한 경우: {old_complex}")
print("→ 순서 맞추기 어렵고, 타입 지정자 외우기 어려움")
```

#### 🔧 **2세대: .format() 메서드 (개선된 방식)**

```python
# 🔧 2세대: .format() 메서드
print("\n🔧 2세대: .format() 메서드")
print("=" * 25)

# 기본 사용법
basic_format = "이름: {}, 나이: {}, 점수: {:.1f}".format(name, age, score)
print(basic_format)

# 순서 지정 가능
ordered_format = "점수: {2:.1f}, 이름: {0}, 나이: {1}".format(name, age, score)
print(ordered_format)

# 이름으로 지정 가능
named_format = "이름: {student_name}, 나이: {student_age}, 점수: {student_score:.1f}".format(
    student_name=name,
    student_age=age,
    student_score=score
)
print(named_format)

# 복잡한 포맷팅
product_info = """
🛍️ 상품 정보:
- 상품명: {product}
- 원가: {price:,}원
- 할인율: {discount:.0%}
- 할인액: {discount_amount:,}원
- 최종가격: {final:,}원
""".format(
    product=product,
    price=price,
    discount=discount,
    discount_amount=int(price * discount),
    final=int(final_price)
)
print(product_info)
```

#### 🚀 **3세대: f-string (현재 최고의 방식)**

```python
# 🚀 3세대: f-string (Python 3.6+, 최신 방식)
print("🚀 3세대: f-string (최신 방식)")
print("=" * 30)

# 가장 간단하고 직관적
modern_style = f"이름: {name}, 나이: {age}, 점수: {score:.1f}"
print(modern_style)

# 변수명이 그대로 보여서 읽기 쉬움
print(f"학생 {name}({age}세)의 점수는 {score:.1f}점입니다.")

# 계산식도 바로 사용 가능
print(f"내년 나이: {age + 1}세")
print(f"평균 점수: {(score + 90 + 88) / 3:.1f}점")

# 조건문도 바로 사용 가능
grade = "A" if score >= 90 else "B" if score >= 80 else "C"
print(f"학점: {grade}등급 {'🎉' if grade == 'A' else '👍' if grade == 'B' else '💪'}")

# 복잡한 f-string
current_time = "2024-03-15 14:30"
summary = f"""
📊 {name} 학생 요약 보고서
{'=' * 30}
📅 작성일: {current_time}
👤 이름: {name}
🎂 나이: {age}세 (생년: {2024 - age}년)
📚 점수: {score:.1f}점 (등급: {grade})
📈 상위 비율: 상위 {100 - score:.0f}%
💭 평가: {'우수' if score >= 85 else '보통' if score >= 70 else '노력 필요'}

다음 목표: {score + 5:.1f}점 (현재보다 +{5}점)
"""
print(summary)
```

#### 🎯 **포맷팅 방식 선택 가이드**

```python
# 🎯 어떤 방식을 선택할까?
print("🎯 포맷팅 방식 선택 가이드")
print("=" * 30)

# 간단한 경우: f-string 추천
simple_message = f"안녕하세요, {name}님!"
print(f"✅ 간단한 경우: {simple_message}")

# 복잡한 조건이 있는 경우: f-string으로도 가능
status = "재학생" if is_student else "일반인"
detailed = f"{name}님은 {age}세 {status}입니다."
print(f"✅ 조건 포함: {detailed}")

# 템플릿이 미리 정해진 경우: .format() 도 괜찮음
template = "학번: {student_id}, 이름: {name}, 학과: {major}"
student_info = template.format(
    student_id="20240001",
    name=name,
    major="컴퓨터공학과"
)
print(f"✅ 템플릿 사용: {student_info}")

print(f"\n💡 결론: 대부분의 경우 f-string이 최고!")
print(f"   - 가장 읽기 쉬움")
print(f"   - 가장 빠름")
print(f"   - 가장 직관적")
```

### 📌 핵심 개념 3: 변수 이름 짓기의 예술 - 네이밍 컨벤션 (10분)

#### 🎨 **좋은 변수명 vs 나쁜 변수명**

```python
# 🎨 변수 이름 짓기의 예술
print("🎨 변수 이름 짓기 마스터하기")
print("=" * 30)

# ❌ 나쁜 변수명들
a = 20            # 뭘 의미하는지 모름
b = 175.5         # 단위도 모름  
x = "김학생"      # 무엇을 나타내는지 불분명
temp = 85.5       # 온도? 임시 변수?
data = True       # 어떤 데이터?

print("❌ 나쁜 변수명 예시:")
print(f"a = {a} (이게 뭔가요?)")
print(f"b = {b} (뭘 측정한 건가요?)")
print(f"x = {x} (왜 x인가요?)")

# ✅ 좋은 변수명들
student_age = 20                    # 학생의 나이
student_height_cm = 175.5          # 학생의 키 (센티미터)
student_name = "김학생"             # 학생의 이름
exam_score = 85.5                  # 시험 점수
is_homework_submitted = True        # 숙제 제출 여부

print(f"\n✅ 좋은 변수명 예시:")
print(f"student_age = {student_age} (학생의 나이)")
print(f"student_height_cm = {student_height_cm} (키, 단위까지 명확)")
print(f"student_name = {student_name} (학생 이름)")
print(f"exam_score = {exam_score} (시험 점수)")
print(f"is_homework_submitted = {is_homework_submitted} (불린값은 is_로 시작)")
```

#### 📏 **파이썬 네이밍 컨벤션 규칙**

```python
# 📏 파이썬 네이밍 컨벤션 (PEP 8 기준)
print("\n📏 파이썬 네이밍 컨벤션")
print("=" * 25)

# 1. 변수와 함수: snake_case (스네이크 케이스)
user_name = "홍길동"                    # ✅ 단어 사이에 언더스코어
total_student_count = 150               # ✅ 여러 단어도 언더스코어
is_exam_finished = False                # ✅ 불린값은 is_, has_ 등으로 시작
max_retry_count = 3                     # ✅ 최대/최소값은 max_, min_

print("✅ snake_case 변수명:")
print(f"user_name = {user_name}")
print(f"total_student_count = {total_student_count}")
print(f"is_exam_finished = {is_exam_finished}")

# 2. 상수: UPPER_CASE (대문자)
MAX_STUDENTS_PER_CLASS = 30             # ✅ 상수는 모두 대문자
PI = 3.14159                           # ✅ 수학 상수
DEFAULT_TIMEOUT_SECONDS = 60            # ✅ 기본값도 상수로

print(f"\n✅ UPPER_CASE 상수:")
print(f"MAX_STUDENTS_PER_CLASS = {MAX_STUDENTS_PER_CLASS}")
print(f"PI = {PI}")

# 3. 클래스: PascalCase (나중에 배울 내용)
class StudentInfo:                      # ✅ 클래스는 각 단어 첫글자 대문자
    pass

print(f"\n✅ PascalCase 클래스명: StudentInfo")

# ❌ 피해야 할 네이밍
print(f"\n❌ 피해야 할 네이밍:")
print(f"l = 1  # 소문자 L은 숫자 1과 헷갈림")
print(f"O = 0  # 대문자 O는 숫자 0과 헷갈림")
print(f"userName = '홍길동'  # camelCase는 자바스크립트 스타일")
print(f"user-name = '홍길동'  # 하이픈은 파이썬에서 금지")
```

#### 🎯 **실용적 네이밍 예시들**

```python
# 🎯 실용적인 변수명 예시
print("\n🎯 실용적인 변수명 예시")
print("=" * 25)

# 쇼핑몰 프로그램 변수들
product_name = "무선 이어폰"              # 상품명
product_price_krw = 89000                # 상품 가격 (원화)
customer_age = 25                        # 고객 나이
is_member = True                         # 회원 여부
has_discount_coupon = False              # 할인 쿠폰 보유 여부
order_count = 1                          # 주문 수량
shipping_fee_krw = 3000                  # 배송비 (원화)

# 할인 계산
member_discount_rate = 0.1 if is_member else 0.0
coupon_discount_amount = 5000 if has_discount_coupon else 0
subtotal = product_price_krw * order_count
discount_amount = subtotal * member_discount_rate + coupon_discount_amount
final_total = subtotal - discount_amount + shipping_fee_krw

print(f"🛍️ 쇼핑몰 주문 정보:")
print(f"상품: {product_name}")
print(f"가격: {product_price_krw:,}원 × {order_count}개")
print(f"회원 할인: {member_discount_rate:.0%}")
print(f"쿠폰 할인: {coupon_discount_amount:,}원")
print(f"배송비: {shipping_fee_krw:,}원")
print(f"최종 결제: {final_total:,}원")

# 게임 프로그램 변수들
print(f"\n🎮 게임 상태 변수:")
player_name = "드래곤슬레이어"            # 플레이어 이름
current_level = 15                       # 현재 레벨
current_health_points = 85               # 현재 체력
max_health_points = 100                  # 최대 체력  
experience_points = 2450                 # 경험치
gold_amount = 15600                      # 소지금
is_in_battle = False                     # 전투 중 여부
respawn_time_seconds = 30                # 부활 시간 (초)

health_percentage = (current_health_points / max_health_points) * 100

print(f"플레이어: {player_name}")
print(f"레벨: {current_level}")
print(f"체력: {current_health_points}/{max_health_points} ({health_percentage:.1f}%)")
print(f"경험치: {experience_points:,}")
print(f"골드: {gold_amount:,}")
print(f"전투 상태: {'전투 중' if is_in_battle else '평화'}")
```

---

## ☕ 휴식 시간 (10분)

---

## 🎯 3부: 연산자 마스터하기와 코딩 스타일 (40분)

### 📌 핵심 개념 1: 연산자 우선순위와 괄호의 힘 (15분)

#### 🧮 **수학과 똑같은 연산자 우선순위**

```python
# 🧮 연산자 우선순위 완전 분석
print("🧮 연산자 우선순위 마스터하기")
print("=" * 35)

# 기본 수학 규칙과 동일
expression1 = 2 + 3 * 4
expression2 = (2 + 3) * 4

print(f"2 + 3 * 4 = {expression1}")         # 곱셈 먼저: 2 + 12 = 14
print(f"(2 + 3) * 4 = {expression2}")       # 괄호 먼저: 5 * 4 = 20

# 복잡한 예시로 우선순위 확인
complex_expr = 10 + 5 * 2 - 8 / 4 + 3 ** 2
print(f"\n복잡한 식: 10 + 5 * 2 - 8 / 4 + 3 ** 2")
print(f"단계별 계산:")
print(f"  1. 3 ** 2 = 9        (지수 연산 먼저)")
print(f"  2. 5 * 2 = 10        (곱셈)")
print(f"  3. 8 / 4 = 2.0       (나눗셈)")
print(f"  4. 10 + 10 - 2.0 + 9 = 27.0  (덧셈/뺄셈)")
print(f"결과: {complex_expr}")
```

#### 🎯 **실용적인 계산에서 괄호 활용**

```python
# 🎯 실용적인 계산에서 괄호의 중요성
print("\n🎯 실용적 계산에서 괄호 활용")
print("=" * 30)

# 예시 1: 할인된 상품 가격 계산
original_price = 50000
discount_rate = 0.2
tax_rate = 0.1

# ❌ 잘못된 계산 (괄호 없이)
wrong_calculation = original_price - original_price * discount_rate + original_price * tax_rate
print(f"❌ 잘못된 계산: {wrong_calculation}")

# ✅ 올바른 계산 (괄호 사용)
correct_calculation = original_price * (1 - discount_rate) * (1 + tax_rate)
print(f"✅ 올바른 계산: {correct_calculation}")

print(f"\n단계별 계산:")
discounted_price = original_price * (1 - discount_rate)  # 할인 적용
final_price = discounted_price * (1 + tax_rate)          # 세금 적용
print(f"1. 원가: {original_price:,}원")
print(f"2. 할인 후: {discounted_price:,}원")
print(f"3. 세금 포함 최종: {final_price:,}원")

# 예시 2: 복리 이자 계산
principal = 1000000      # 원금
annual_rate = 0.05       # 연 이율 5%
years = 3                # 3년

# 복리 공식: 원금 * (1 + 이율) ** 기간
compound_interest = principal * (1 + annual_rate) ** years
simple_interest = principal * (1 + annual_rate * years)

print(f"\n💰 이자 계산 비교:")
print(f"원금: {principal:,}원")
print(f"연 이율: {annual_rate:.1%}")
print(f"기간: {years}년")
print(f"복리: {compound_interest:,.0f}원")
print(f"단리: {simple_interest:,.0f}원")
print(f"차이: {compound_interest - simple_interest:,.0f}원")
```

#### ⚖️ **비교 연산자와 논리 연산자 우선순위**

```python
# ⚖️ 비교와 논리 연산자 우선순위
print("\n⚖️ 비교와 논리 연산자")
print("=" * 25)

age = 20
income = 3000000
is_student = True

# 복잡한 조건문에서 우선순위
condition1 = age >= 18 and income > 2000000 or is_student
condition2 = age >= 18 and (income > 2000000 or is_student)

print(f"나이: {age}세")
print(f"소득: {income:,}원")
print(f"학생 여부: {is_student}")

print(f"\n조건1 (괄호 없음): {condition1}")
print(f"조건2 (괄호 있음): {condition2}")

# 명확하게 괄호로 의도 표현
can_get_loan = (age >= 18) and ((income > 2000000) or is_student)
print(f"대출 가능 여부: {can_get_loan}")

# 단계별 분석
print(f"\n단계별 분석:")
print(f"  성인인가? {age >= 18}")
print(f"  소득 충분? {income > 2000000}")
print(f"  학생인가? {is_student}")
print(f"  소득 충분 또는 학생? {(income > 2000000) or is_student}")
print(f"  최종 결과: {can_get_loan}")
```

### 📌 핵심 개념 2: 복합 할당 연산자 - 코드를 간결하게 (10분)

#### 🔄 **복합 할당 연산자의 편리함**

```python
# 🔄 복합 할당 연산자 완전 활용
print("🔄 복합 할당 연산자 마스터하기")
print("=" * 35)

# 기본 복합 할당 연산자들
score = 100
lives = 3
name = "Player"
items = []

print(f"초기값들:")
print(f"점수: {score}, 목숨: {lives}, 이름: {name}")

# += (더하기 후 할당)
score += 50        # score = score + 50 과 동일
print(f"\n점수 +50: {score}")

# -= (빼기 후 할당)  
lives -= 1         # lives = lives - 1 과 동일
print(f"목숨 -1: {lives}")

# *= (곱하기 후 할당)
score *= 2         # score = score * 2 와 동일
print(f"점수 ×2: {score}")

# /= (나누기 후 할당)
score /= 3         # score = score / 3 과 동일
print(f"점수 ÷3: {score:.1f}")

# //= (몫 구하기 후 할당)
score //= 2        # score = score // 2 와 동일
print(f"점수 //2: {score}")

# **= (거듭제곱 후 할당)
base_damage = 10
base_damage **= 2  # base_damage = base_damage ** 2 와 동일
print(f"기본 데미지 제곱: {base_damage}")

# %= (나머지 후 할당)
turn_count = 7
turn_count %= 3    # turn_count = turn_count % 3 과 동일
print(f"턴 수를 3으로 나눈 나머지: {turn_count}")
```

#### 📊 **실용적인 복합 할당 연산자 활용**

```python
# 📊 실용적인 복합 할당 연산자 활용
print("\n📊 실용적 활용 사례")
print("=" * 20)

# 게임 스코어 시스템
print("🎮 게임 스코어 시스템:")
player_score = 0
combo_multiplier = 1

print(f"초기 점수: {player_score}")

# 적 처치로 점수 획득
enemy_points = 100
player_score += enemy_points
print(f"적 처치 (+{enemy_points}): {player_score}")

# 콤보 달성으로 배수 증가
combo_multiplier += 0.5
player_score *= combo_multiplier
print(f"콤보 달성 (×{combo_multiplier}): {player_score}")

# 실수로 감점
penalty = 50
player_score -= penalty
print(f"실수 감점 (-{penalty}): {player_score}")

# 쇼핑몰 장바구니 시스템
print(f"\n🛒 쇼핑몰 장바구니:")
total_price = 0
item_count = 0

# 상품 추가
item_price = 25000
item_quantity = 2
total_price += item_price * item_quantity
item_count += item_quantity
print(f"상품 추가: {item_price:,}원 × {item_quantity}개")
print(f"현재 총액: {total_price:,}원, 상품 수: {item_count}개")

# 할인 적용
discount_rate = 0.1
total_price *= (1 - discount_rate)
print(f"할인 적용 (-{discount_rate:.0%}): {total_price:,}원")

# 배송비 추가
shipping_fee = 3000
total_price += shipping_fee
print(f"배송비 추가 (+{shipping_fee:,}원): {total_price:,}원")
```

#### 📝 **문자열과 리스트에서의 복합 할당**

```python
# 📝 문자열과 리스트에서의 복합 할당
print("\n📝 문자열과 리스트 복합 할당")
print("=" * 30)

# 문자열 합치기
message = "안녕하세요"
message += ", "        # message = message + ", "
message += "파이썬"
message += " 세계!"
print(f"메시지 완성: {message}")

# 메시지 반복
excited_message = "와! "
excited_message *= 3   # excited_message = excited_message * 3
print(f"흥분된 메시지: {excited_message}")

# 리스트에 항목 추가 (나중에 자세히 배울 내용)
shopping_list = ["우유"]
shopping_list += ["빵"]           # 리스트 연결
shopping_list += ["계란", "사과"]  # 여러 항목 한번에 추가
print(f"쇼핑 목록: {shopping_list}")

# 실용적 예시: 로그 메시지 작성
log_message = "[2024-03-15 14:30:00] "
log_message += "시스템 시작"
log_message += " - 사용자: " + "김개발자"
log_message += " - 상태: 정상"
print(f"로그: {log_message}")

# 진행률 표시 (프로그레스 바)
progress_bar = ""
progress_percentage = 65
filled_blocks = progress_percentage // 10
progress_bar += "█" * filled_blocks           # 채워진 부분
progress_bar += "░" * (10 - filled_blocks)    # 빈 부분
print(f"진행률: [{progress_bar}] {progress_percentage}%")
```

### 📌 핵심 개념 3: PEP 8 스타일 가이드 - 아름다운 코드 작성법 (15분)

#### 🎨 **코드 가독성의 중요성**

```python
# 🎨 PEP 8 스타일 가이드 - 아름다운 코드
print("🎨 PEP 8 스타일 가이드")
print("=" * 25)

# ❌ 나쁜 스타일의 코드 (동작은 하지만 읽기 어려움)
a=10
b=20
c=30
if a>b and b<c:d=a+b*c
else:d=a-b
print("결과:",d)

print("❌ 위 코드는 동작하지만 읽기 어려워요!")

# ✅ 좋은 스타일의 코드 (같은 기능, 읽기 쉬움)
first_number = 10
second_number = 20
third_number = 30

if first_number > second_number and second_number < third_number:
    result = first_number + second_number * third_number
else:
    result = first_number - second_number

print(f"✅ 계산 결과: {result}")
```

#### 📏 **들여쓰기와 띄어쓰기 규칙**

```python
# 📏 들여쓰기와 띄어쓰기 규칙
print("\n📏 들여쓰기와 띄어쓰기")
print("=" * 25)

# 1. 들여쓰기: 스페이스 4개 (탭 X)
def calculate_grade(score):
    if score >= 90:        # 4칸 들여쓰기
        grade = "A"
        comment = "우수"
    elif score >= 80:      # 4칸 들여쓰기
        grade = "B"        # 8칸 들여쓰기 (중첩)
        comment = "양호"
    else:
        grade = "C"
        comment = "노력 필요"
    
    return grade, comment

# 2. 연산자 앞뒤 띄어쓰기
total = 100 + 200 + 300              # ✅ 연산자 앞뒤 공백
average = total / 3                  # ✅ 
result = (first_number + second_number) * 2  # ✅

# 3. 함수 호출 시 띄어쓰기
print(f"평균: {average:.1f}")         # ✅ 콤마 뒤 공백
student_grade, student_comment = calculate_grade(85)  # ✅

# 4. 리스트와 딕셔너리 띄어쓰기
numbers = [1, 2, 3, 4, 5]            # ✅ 콤마 뒤 공백
student_info = {                     # ✅ 여러 줄로 정리
    "name": "김학생",
    "age": 20,
    "grade": student_grade
}

print(f"학생 정보: {student_info}")
```

#### 📝 **주석과 문서화 스타일**

```python
# 📝 주석과 문서화 스타일
print("\n📝 주석과 문서화")
print("=" * 20)

# ✅ 좋은 주석 스타일
def calculate_monthly_payment(loan_amount, annual_rate, years):
    """
    월 대출 상환금을 계산하는 함수
    
    Args:
        loan_amount (float): 대출 원금
        annual_rate (float): 연 이율 (예: 0.05 = 5%)
        years (int): 대출 기간 (년)
    
    Returns:
        float: 월 상환금
    """
    # 월 이율 계산
    monthly_rate = annual_rate / 12
    
    # 총 상환 횟수 (개월)
    total_payments = years * 12
    
    # 월 상환금 공식 적용
    if monthly_rate == 0:  # 무이자인 경우
        monthly_payment = loan_amount / total_payments
    else:
        # 복리 계산 공식
        monthly_payment = loan_amount * (
            monthly_rate * (1 + monthly_rate) ** total_payments
        ) / (
            (1 + monthly_rate) ** total_payments - 1
        )
    
    return monthly_payment

# 함수 사용 예시
principal = 100000000  # 1억원 대출
rate = 0.035          # 연 3.5%
period = 30           # 30년

monthly_payment = calculate_monthly_payment(principal, rate, period)
total_payment = monthly_payment * period * 12
total_interest = total_payment - principal

print(f"💰 대출 계산 결과:")
print(f"대출원금: {principal:,}원")
print(f"월 상환금: {monthly_payment:,.0f}원")
print(f"총 상환금: {total_payment:,.0f}원")
print(f"총 이자: {total_interest:,.0f}원")
```

#### 🔧 **코딩 스타일 검사 도구**

```python
# 🔧 코딩 스타일 자가 진단
print("\n🔧 코딩 스타일 자가 진단")
print("=" * 25)

# 체크리스트
style_checklist = {
    "변수명이 명확한가?": True,        # snake_case 사용
    "들여쓰기가 일정한가?": True,       # 스페이스 4개
    "연산자에 공백이 있는가?": True,    # x = 1 + 2
    "함수에 문서화가 있는가?": True,    # docstring
    "주석이 도움되는가?": True,         # 의미 있는 주석
    "한 줄이 너무 길지 않은가?": True   # 79자 이하 권장
}

print("✅ 스타일 체크리스트:")
for check, passed in style_checklist.items():
    status = "✅" if passed else "❌"
    print(f"  {status} {check}")

print(f"\n💡 스타일 점수: {sum(style_checklist.values())}/{len(style_checklist)}")

# 실제 적용 예시
def format_currency(amount, currency="원"):
    """
    금액을 통화 형식으로 포맷팅
    
    Args:
        amount (float): 금액
        currency (str): 통화 단위
    
    Returns:
        str: 포맷된 금액 문자열
    """
    return f"{amount:,.0f}{currency}"

# 깔끔한 코드 예시
sales_data = [1200000, 1500000, 980000, 2100000]
total_sales = sum(sales_data)
average_sales = total_sales / len(sales_data)
best_month = max(sales_data)
worst_month = min(sales_data)

print(f"\n📊 매출 분석 결과:")
print(f"총 매출: {format_currency(total_sales)}")
print(f"평균 매출: {format_currency(average_sales)}")
print(f"최고 매출: {format_currency(best_month)}")
print(f"최저 매출: {format_currency(worst_month)}")
```

---

## 🎯 실습 시간 (60분)

### 🎯 실습 과제 1: 숫자야구 게임 완성하기 (25분)

**목표**: 오늘 배운 변수, 문자열 처리, 조건문을 활용하여 완전한 숫자야구 게임 만들기

```python
#!/usr/bin/env python3
"""
🎮 숫자야구 게임 (완전판)
- 변수 활용: 게임 상태 관리
- 문자열 처리: 입력값 검증 및 비교
- 조건문: 스트라이크/볼 판정
- 반복문: 게임 진행
"""

print("🎮 숫자야구 게임에 오신 것을 환영합니다!")
print("=" * 40)
print("📋 게임 규칙:")
print("1. 컴퓨터가 3자리 숫자를 생각합니다")
print("2. 각 자리는 1~9의 서로 다른 숫자입니다")
print("3. 숫자와 위치가 모두 맞으면 '스트라이크'")
print("4. 숫자는 맞지만 위치가 틀리면 '볼'")
print("5. 3스트라이크가 되면 승리!")
print("=" * 40)

# 게임 설정 변수들
SECRET_ANSWER = "742"        # 실제로는 랜덤 생성해야 함
MAX_ATTEMPTS = 10            # 최대 시도 횟수
current_attempt = 0          # 현재 시도 횟수
game_over = False           # 게임 종료 여부
game_won = False            # 게임 승리 여부

print(f"🎯 목표: 3자리 숫자 맞추기 (최대 {MAX_ATTEMPTS}번 시도)")
print(f"💡 힌트: 각 자리는 1~9의 서로 다른 숫자입니다")

# 게임 시뮬레이션 (실제로는 input() 사용)
player_guesses = ["123", "456", "781", "724", "742"]

for guess in player_guesses:
    if game_over:
        break
        
    current_attempt += 1
    print(f"\n{'='*20} {current_attempt}번째 시도 {'='*20}")
    print(f"입력: {guess}")
    
    # 입력값 검증
    if len(guess) != 3:
        print("❌ 3자리 숫자를 입력해주세요!")
        continue
    
    if not guess.isdigit():
        print("❌ 숫자만 입력해주세요!")
        continue
    
    # 중복 숫자 검사
    if len(set(guess)) != 3:
        print("❌ 서로 다른 숫자를 입력해주세요!")
        continue
    
    # 스트라이크와 볼 계산
    strike_count = 0
    ball_count = 0
    
    # 각 자리수별 상세 분석
    print(f"\n🔍 자리별 분석:")
    
    for position in range(3):
        guess_digit = guess[position]
        secret_digit = SECRET_ANSWER[position]
        
        if guess_digit == secret_digit:
            strike_count += 1
            print(f"  {position+1}번째 자리 '{guess_digit}': ⚾ 스트라이크!")
        elif guess_digit in SECRET_ANSWER:
            ball_count += 1
            print(f"  {position+1}번째 자리 '{guess_digit}': 🥎 볼!")
        else:
            print(f"  {position+1}번째 자리 '{guess_digit}': ❌ 아웃!")
    
    # 결과 출력
    print(f"\n📊 결과: {strike_count}스트라이크 {ball_count}볼")
    
    # 게임 종료 조건 확인
    if strike_count == 3:
        print(f"\n🎉🎉🎉 축하합니다! 🎉🎉🎉")
        print(f"정답 '{SECRET_ANSWER}'을 {current_attempt}번 만에 맞추셨습니다!")
        game_won = True
        game_over = True
    elif current_attempt >= MAX_ATTEMPTS:
        print(f"\n😭 아쉽네요! 기회를 모두 사용하셨습니다.")
        print(f"정답은 '{SECRET_ANSWER}'였습니다.")
        game_over = True
    else:
        remaining_attempts = MAX_ATTEMPTS - current_attempt
        print(f"💪 남은 기회: {remaining_attempts}번")
        
        # 힌트 제공
        if strike_count > 0:
            print(f"🎯 {strike_count}개 자리의 위치가 정확합니다!")
        if ball_count > 0:
            print(f"🔄 {ball_count}개 숫자가 포함되어 있지만 위치가 틀렸습니다!")

# 게임 통계
print(f"\n📈 게임 통계:")
print(f"총 시도 횟수: {current_attempt}번")
print(f"성공률: {100 if game_won else 0}%")
if game_won:
    efficiency = (current_attempt / MAX_ATTEMPTS) * 100
    print(f"효율성: {efficiency:.1f}% (빠를수록 좋음)")

print(f"\n🎮 게임이 종료되었습니다. 감사합니다!")
```

### 🎯 실습 과제 2: 고급 계산기 프로그램 (20분)

**목표**: PEP 8 스타일을 적용한 다기능 계산기 만들기

```python
#!/usr/bin/env python3
"""
🧮 고급 계산기 프로그램
- 변수 네이밍: snake_case 적용
- 문자열 포맷팅: f-string 활용
- 연산자 우선순위: 괄호 적절히 사용
- 복합 할당 연산자: 코드 간결화
- PEP 8 스타일: 가독성 향상
"""

def format_number(number):
    """
    숫자를 읽기 쉬운 형태로 포맷팅
    
    Args:
        number (float): 포맷팅할 숫자
    
    Returns:
        str: 포맷된 숫자 문자열
    """
    if number == int(number):
        return f"{int(number):,}"
    else:
        return f"{number:,.2f}"


def calculate_circle_info(radius):
    """
    원의 둘레와 넓이를 계산
    
    Args:
        radius (float): 원의 반지름
    
    Returns:
        tuple: (둘레, 넓이)
    """
    PI = 3.14159265359
    circumference = 2 * PI * radius
    area = PI * (radius ** 2)
    return circumference, area


def calculate_loan_payment(principal, annual_rate, years):
    """
    대출 월 상환금 계산
    
    Args:
        principal (float): 대출 원금
        annual_rate (float): 연 이율
        years (int): 대출 기간
    
    Returns:
        dict: 대출 관련 계산 결과
    """
    monthly_rate = annual_rate / 12
    total_months = years * 12
    
    if monthly_rate == 0:
        monthly_payment = principal / total_months
    else:
        monthly_payment = principal * (
            monthly_rate * ((1 + monthly_rate) ** total_months)
        ) / (
            ((1 + monthly_rate) ** total_months) - 1
        )
    
    total_payment = monthly_payment * total_months
    total_interest = total_payment - principal
    
    return {
        "monthly_payment": monthly_payment,
        "total_payment": total_payment,
        "total_interest": total_interest
    }


# 메인 계산기 프로그램
print("🧮 고급 계산기 프로그램")
print("=" * 30)

# 기본 계산 실습
print("📊 1. 기본 사칙연산")
print("-" * 20)

first_number = 1250
second_number = 347

addition_result = first_number + second_number
subtraction_result = first_number - second_number
multiplication_result = first_number * second_number
division_result = first_number / second_number

print(f"첫 번째 수: {format_number(first_number)}")
print(f"두 번째 수: {format_number(second_number)}")
print(f"덧셈: {format_number(addition_result)}")
print(f"뺄셈: {format_number(subtraction_result)}")
print(f"곱셈: {format_number(multiplication_result)}")
print(f"나눗셈: {format_number(division_result)}")

# 복합 할당 연산자 활용
print(f"\n🔄 2. 누적 계산")
print("-" * 15)

running_total = 0
print(f"초기값: {format_number(running_total)}")

running_total += 1000    # 첫 번째 추가
print(f"1,000 추가: {format_number(running_total)}")

running_total *= 1.05    # 5% 증가
print(f"5% 증가: {format_number(running_total)}")

running_total -= 200     # 200 차감
print(f"200 차감: {format_number(running_total)}")

running_total //= 10     # 10으로 나눈 몫
print(f"10으로 나눈 몫: {format_number(running_total)}")

# 기하학 계산
print(f"\n🔵 3. 원의 계산")
print("-" * 15)

circle_radius = 7.5
circle_circumference, circle_area = calculate_circle_info(circle_radius)

print(f"반지름: {format_number(circle_radius)}cm")
print(f"둘레: {format_number(circle_circumference)}cm")
print(f"넓이: {format_number(circle_area)}cm²")

# 금융 계산
print(f"\n💰 4. 대출 계산")
print("-" * 15)

loan_amount = 300000000      # 3억원
interest_rate = 0.025        # 연 2.5%
loan_period = 20             # 20년

loan_info = calculate_loan_payment(loan_amount, interest_rate, loan_period)

print(f"대출 원금: {format_number(loan_amount)}원")
print(f"연 이율: {interest_rate:.1%}")
print(f"대출 기간: {loan_period}년")
print(f"월 상환금: {format_number(loan_info['monthly_payment'])}원")
print(f"총 상환금: {format_number(loan_info['total_payment'])}원")
print(f"총 이자: {format_number(loan_info['total_interest'])}원")

# 복잡한 수식 계산
print(f"\n🔬 5. 복잡한 수식")
print("-" * 15)

x = 5
y = 3
z = 2

# 괄호를 활용한 명확한 수식
complex_result_1 = (x + y) * z - (x - y) ** 2
complex_result_2 = ((x * y) + (z ** 2)) / (x + z)
complex_result_3 = (x ** 2 + y ** 2) ** 0.5  # 피타고라스 정리

print(f"x = {x}, y = {y}, z = {z}")
print(f"(x + y) × z - (x - y)² = {format_number(complex_result_1)}")
print(f"(xy + z²) ÷ (x + z) = {format_number(complex_result_2)}")
print(f"√(x² + y²) = {format_number(complex_result_3)}")

# 단위 변환
print(f"\n📏 6. 단위 변환")
print("-" * 15)

meters = 1500
kilometers = meters / 1000
centimeters = meters * 100
inches = meters * 39.3701
feet = inches / 12

print(f"{format_number(meters)}m =")
print(f"  {format_number(kilometers)}km")
print(f"  {format_number(centimeters)}cm")  
print(f"  {format_number(inches)}inch")
print(f"  {format_number(feet)}feet")

print(f"\n🎉 계산기 프로그램 완료!")
```

### 🎯 실습 과제 3: 변수와 문자열 종합 활용 (15분)

**목표**: 학생 성적 관리 시스템으로 모든 개념 통합하기

```python
#!/usr/bin/env python3
"""
📚 학생 성적 관리 시스템
- 변수 활용: 학생 정보 저장
- 문자열 포맷팅: 보고서 생성
- 조건문: 등급 판정
- 수학 계산: 통계 처리
"""

# 학생 기본 정보 (변수 네이밍 컨벤션 적용)
student_name = "김파이썬"
student_id = "2024001"
student_grade = 2
student_major = "컴퓨터공학과"

# 과목별 점수
korean_score = 88.5
english_score = 92.0
mathematics_score = 85.5
science_score = 90.0
social_studies_score = 87.5

print("📚 학생 성적 관리 시스템")
print("=" * 40)

# 기본 정보 출력
print(f"👤 학생 정보")
print(f"{'':>4}이름: {student_name}")
print(f"{'':>4}학번: {student_id}")
print(f"{'':>4}학년: {student_grade}학년")
print(f"{'':>4}전공: {student_major}")

# 점수 통계 계산
subject_scores = [
    korean_score, english_score, mathematics_score,
    science_score, social_studies_score
]
subject_names = ["국어", "영어", "수학", "과학", "사회"]

total_score = sum(subject_scores)
average_score = total_score / len(subject_scores)
highest_score = max(subject_scores)
lowest_score = min(subject_scores)

# 과목별 점수 출력
print(f"\n📊 과목별 점수")
print("-" * 25)
for i, (subject, score) in enumerate(zip(subject_names, subject_scores)):
    # 최고점과 최저점 표시
    if score == highest_score:
        status_icon = "🏆"
    elif score == lowest_score:
        status_icon = "📈"
    else:
        status_icon = "📝"
    
    print(f"{status_icon} {subject:>4}: {score:5.1f}점")

# 통계 정보
print(f"\n📈 성적 통계")
print("-" * 20)
print(f"총점: {total_score:6.1f}점")
print(f"평균: {average_score:6.1f}점")
print(f"최고: {highest_score:6.1f}점")
print(f"최저: {lowest_score:6.1f}점")
print(f"편차: {highest_score - lowest_score:6.1f}점")

# 등급 판정 (복잡한 조건문)
if average_score >= 95:
    letter_grade = "A+"
    grade_comment = "최우수"
    scholarship_eligible = True
elif average_score >= 90:
    letter_grade = "A"
    grade_comment = "우수"
    scholarship_eligible = True
elif average_score >= 85:
    letter_grade = "B+"
    grade_comment = "양호"
    scholarship_eligible = False
elif average_score >= 80:
    letter_grade = "B"
    grade_comment = "보통"
    scholarship_eligible = False
elif average_score >= 75:
    letter_grade = "C+"
    grade_comment = "미흡"
    scholarship_eligible = False
else:
    letter_grade = "C"
    grade_comment = "노력 필요"
    scholarship_eligible = False

# 상대적 위치 계산 (가상의 전체 학생 중)
total_students = 150
estimated_rank = int((100 - average_score) * total_students / 40) + 1
if estimated_rank > total_students:
    estimated_rank = total_students

percentile = ((total_students - estimated_rank) / total_students) * 100

# 최종 결과 출력
print(f"\n🎯 최종 평가")
print("-" * 20)
print(f"학점: {letter_grade}")
print(f"평가: {grade_comment}")
print(f"예상 순위: {estimated_rank:3d}/{total_students}등")
print(f"상위 비율: {percentile:5.1f}%")
print(f"장학금 대상: {'✅ 예' if scholarship_eligible else '❌ 아니오'}")

# 과목별 상세 분석
print(f"\n🔍 과목별 분석")
print("-" * 20)

for subject, score in zip(subject_names, subject_scores):
    # 평균 대비 분석
    difference = score - average_score
    
    if difference > 5:
        analysis = "강점 과목"
        icon = "💪"
    elif difference > 0:
        analysis = "평균 이상"
        icon = "👍"
    elif difference > -5:
        analysis = "평균 근처"
        icon = "📝"
    else:
        analysis = "보완 필요"
        icon = "📚"
    
    print(f"{icon} {subject:>4}: {score:5.1f}점 ({difference:+5.1f}) - {analysis}")

# 학습 권장사항
print(f"\n💡 학습 권장사항")
print("-" * 25)

# 가장 낮은 점수 과목 찾기
lowest_subject_index = subject_scores.index(lowest_score)
lowest_subject = subject_names[lowest_subject_index]

# 가장 높은 점수 과목 찾기
highest_subject_index = subject_scores.index(highest_score)
highest_subject = subject_names[highest_subject_index]

improvement_needed = 90 - lowest_score  # 90점까지 올리려면

print(f"🎯 중점 개선 과목: {lowest_subject} (+{improvement_needed:.1f}점 향상 권장)")
print(f"💪 장점 유지 과목: {highest_subject} (현재 수준 유지)")

if average_score < 85:
    print(f"📚 전반적인 학습 시간 증가가 필요합니다.")
else:
    print(f"🎉 전반적으로 우수한 성적입니다!")

# 목표 설정
next_semester_target = average_score + 3
print(f"\n🎯 다음 학기 목표: 평균 {next_semester_target:.1f}점")

required_improvement = next_semester_target - average_score
print(f"   각 과목 평균 +{required_improvement:.1f}점 향상 필요")

print(f"\n📄 성적표 생성 완료!")
print(f"   작성 대상: {student_name} ({student_id})")
print(f"   종합 평점: {letter_grade} ({average_score:.1f}점)")
```

---

## 📚 오늘 배운 내용 정리

### ✅ 핵심 포인트

1. **변수의 필요성**:
   - 복잡한 계산의 중간 결과 보관 (도형 면적 계산 예시)
   - 미리 정해지지 않은 상황 대응 (숫자야구 게임 예시)
   - 프로그램의 상태 추적과 관리

2. **자료형 심화**:
   - 문자열: 길이, 슬라이싱, 메서드 활용
   - 숫자형: 정수와 실수의 차이, 타입 변환
   - 불린형: 논리 연산과 조건문 활용

3. **문자열 포맷팅 진화**:
   - 1세대: % 포맷팅 (레거시)
   - 2세대: .format() 메서드 (템플릿용)
   - 3세대: f-string (현재 최고, 가장 권장)

4. **네이밍 컨벤션**:
   - 변수/함수: snake_case
   - 상수: UPPER_CASE
   - 클래스: PascalCase
   - 의미 있는 이름 사용의 중요성

5. **연산자와 코딩 스타일**:
   - 연산자 우선순위와 괄호 활용
   - 복합 할당 연산자로 코드 간결화
   - PEP 8 스타일 가이드 적용

### 🏠 다음 주까지 해볼 과제

1. **변수 활용 연습**:
   - 복잡한 수학 문제를 단계별로 변수를 사용해서 풀어보기
   - 일상생활의 계산을 프로그램으로 만들어보기

2. **문자열 연습**:
   - f-string으로 다양한 형태의 메시지 만들어보기
   - 문자열 메서드들 직접 실험해보기

3. **코딩 스타일 연습**:
   - 기존에 작성한 코드를 PEP 8 스타일로 개선하기
   - 변수명을 더 명확하게 다시 작성하기

4. **숫자야구 게임 개선**:
   - 실제 사용자 입력 받아서 동작하게 만들기
   - 난이도 조절 기능 추가해보기

### 🔮 다음 주 예고

**4주차: 제어문 I - 조건문과 선택 구조**
- if, elif, else의 다양한 패턴
- 중첩 조건문과 복잡한 논리
- 삼항 연산자와 간결한 조건 처리
- 실제 문제 해결에 조건문 적용하기

### 💡 마지막 정리

**지금까지의 성장 과정:**
```
1주차: "프로그래밍이 뭔지 알았다!"
2주차: "어디서든 코딸할 수 있게 되었다!"
3주차: "변수로 복잡한 문제를 해결할 수 있다!"
```

**오늘 여러분이 할 수 있게 된 것들:**
- 🧮 복잡한 계산을 단계별로 분해하여 처리하기
- 🎮 사용자 입력에 반응하는 동적 프로그램 만들기
- 📝 아름답고 읽기 쉬운 코드 작성하기
- 🔤 문자열을 자유자재로 다루기
- 📏 전문가처럼 변수 이름 짓기

**중요한 깨달음:**
- **변수는 단순한 저장소가 아니라 문제 해결의 핵심 도구**
- **좋은 변수명은 코드를 읽는 사람에 대한 배려**
- **f-string은 현재 최고의 문자열 포맷팅 방법**
- **PEP 8 스타일은 코드의 품격을 높이는 기본 소양**

**실무에서 변수가 중요한 이유:**
```python
# ❌ 변수 없이 작성하면
result = (price * quantity * (1 - discount_rate) * (1 + tax_rate) + shipping_fee) * exchange_rate

# ✅ 변수로 단계별 처리하면
subtotal = price * quantity
discounted_amount = subtotal * (1 - discount_rate)
taxed_amount = discounted_amount * (1 + tax_rate)
total_with_shipping = taxed_amount + shipping_fee
final_amount_krw = total_with_shipping * exchange_rate
```

첫 번째는 실수하기 쉽고 이해하기 어렵지만, 두 번째는 각 단계가 명확하고 검증 가능합니다.

**다음 주 학습을 위한 준비:**
- 오늘 배운 변수와 문자열 처리가 조건문의 기초가 됩니다
- 숫자야구 게임에서 사용한 if-elif-else 패턴을 더 깊이 배웁니다
- 복잡한 조건 처리와 중첩 구조를 마스터하게 됩니다

**마지막 격려:**
프로그래밍에서 변수를 제대로 다룰 수 있다는 것은 마치 요리에서 재료를 다룰 수 있는 것과 같습니다. 기본기가 탄탄해야 멋진 요리(프로그램)를 만들 수 있어요!

변수 하나하나에 의미를 담고, 단계별로 차근차근 문제를 해결하는 여러분의 모습이 벌써 진짜 개발자 같습니다! 🚀

다음 주에는 조건문으로 더욱 똑똑한 프로그램을 만들어봅시다! 💪

---

**🎯 3주차 학습 완료! 수고하셨습니다! 🎉** 