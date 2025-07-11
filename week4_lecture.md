# 4주차: 제어문 I - 조건문과 선택 구조
**총 강의시간: 3시간 20분 (200분)**
- 강의: 120분 (3부로 구성)
- 휴식: 20분 (10분씩 2회)
- 실습: 60분

---

## 🎯 1부: 왜 함수가 필요할까? - 복잡한 로직을 다루는 방법 (40분)

### 📌 핵심 개념 1: 지금까지의 여정과 새로운 문제 (8분)

#### 🔄 **지금까지 우리가 도달한 지점**

**1주차**: 프로그래밍의 3대 마법 구조
- 순차: "차례대로 하나씩"
- 선택: "상황에 따라 다르게"  
- 반복: "조건 만족할 때까지 계속"

**2주차**: 개발환경 마스터
- Google Colab & Docker 활용

**3주차**: 변수와 자료형 완전 정복
- 복잡한 계산을 변수로 단계별 처리
- 문자열 포맷팅과 PEP 8 스타일

**오늘 해결할 문제**: 
코드가 점점 길어지고 복잡해지는데, 어떻게 관리하고 재사용할 수 있을까?

#### 🤔 **현실적인 문제 상황: 코드 중복의 악마**

**예시: 성적 계산 프로그램**

```python
# 😰 함수 없이 작성한 성적 계산 (중복 코드가 가득!)

# 첫 번째 학생 성적 계산
student1_korean = 85
student1_english = 92
student1_math = 78
student1_total = student1_korean + student1_english + student1_math
student1_average = student1_total / 3

if student1_average >= 90:
    student1_grade = "A"
elif student1_average >= 80:
    student1_grade = "B"
elif student1_average >= 70:
    student1_grade = "C"
else:
    student1_grade = "F"

print(f"첫 번째 학생: 총점 {student1_total}, 평균 {student1_average:.1f}, 등급 {student1_grade}")

# 두 번째 학생 성적 계산 (똑같은 코드 반복!)
student2_korean = 90
student2_english = 88
student2_math = 95
student2_total = student2_korean + student2_english + student2_math  # 중복!
student2_average = student2_total / 3  # 중복!

if student2_average >= 90:      # 중복!
    student2_grade = "A"        # 중복!
elif student2_average >= 80:    # 중복!
    student2_grade = "B"        # 중복!
elif student2_average >= 70:    # 중복!
    student2_grade = "C"        # 중복!
else:                          # 중복!
    student2_grade = "F"        # 중복!

print(f"두 번째 학생: 총점 {student2_total}, 평균 {student2_average:.1f}, 등급 {student2_grade}")

# 세 번째 학생... (또 똑같은 코드!)
# 네 번째 학생... (또또 똑같은 코드!)
# 😱 학생이 30명이라면? 똑같은 코드를 30번 작성!
```

**이 코드의 심각한 문제점들:**

1. **코드 중복**: 똑같은 계산 로직을 여러 번 작성 🔄
2. **수정의 악몽**: 등급 기준이 바뀌면 모든 곳을 다 수정해야 함 😰
3. **실수 위험**: 복사-붙여넣기 중 실수할 확률 높음 ❌
4. **가독성 악화**: 코드가 길어져서 핵심을 파악하기 어려움 📖
5. **유지보수 지옥**: 나중에 수정하거나 개선하기 매우 어려움 🔧

#### 💡 **함수의 등장 - 중복을 제거하는 마법**

**같은 기능을 함수로 작성하면:**

```python
# ✅ 함수를 사용한 깔끔한 코드

def calculate_grade(korean, english, math):
    """
    세 과목 점수를 받아서 총점, 평균, 등급을 계산하는 함수
    
    Args:
        korean (int): 국어 점수
        english (int): 영어 점수
        math (int): 수학 점수
    
    Returns:
        dict: 총점, 평균, 등급 정보
    """
    total = korean + english + math
    average = total / 3
    
    if average >= 90:
        grade = "A"
    elif average >= 80:
        grade = "B"
    elif average >= 70:
        grade = "C"
    else:
        grade = "F"
    
    return {
        "total": total,
        "average": average,
        "grade": grade
    }

# 함수 사용 - 단 한 줄로!
student1_result = calculate_grade(85, 92, 78)
student2_result = calculate_grade(90, 88, 95)
student3_result = calculate_grade(75, 82, 88)

print(f"첫 번째 학생: 총점 {student1_result['total']}, 평균 {student1_result['average']:.1f}, 등급 {student1_result['grade']}")
print(f"두 번째 학생: 총점 {student2_result['total']}, 평균 {student2_result['average']:.1f}, 등급 {student2_result['grade']}")
print(f"세 번째 학생: 총점 {student3_result['total']}, 평균 {student3_result['average']:.1f}, 등급 {student3_result['grade']}")

# 🎉 30명의 학생이라도 30줄이면 끝!
```

#### 🌟 **함수의 4대 핵심 이점**

**1. 재사용성 (Reusability)**
```python
# 같은 함수를 몇 번이든 사용 가능
result1 = calculate_grade(85, 90, 88)
result2 = calculate_grade(92, 87, 94)
result3 = calculate_grade(78, 85, 90)
# 필요한 만큼 계속...
```

**2. 유지보수성 (Maintainability)**  
```python
# 등급 기준이 바뀌어도 함수 하나만 수정하면 끝!
def calculate_grade(korean, english, math):
    total = korean + english + math
    average = total / 3
    
    # 등급 기준 변경 - 여기 한 곳만 수정!
    if average >= 95:    # A+ 등급 추가
        grade = "A+"
    elif average >= 90:
        grade = "A"
    # ... 나머지 동일
```

**3. 가독성 (Readability)**
```python
# 함수명만 봐도 무엇을 하는지 명확!
student_result = calculate_grade(85, 90, 88)  # 명확!
payment_result = process_payment(card_info, amount)  # 명확!
shipping_cost = calculate_shipping(address, weight)  # 명확!
```

**4. 테스트 용이성 (Testability)**
```python
# 각 함수를 개별적으로 테스트 가능
def test_calculate_grade():
    result = calculate_grade(90, 90, 90)
    assert result["grade"] == "A"
    assert result["average"] == 90
    print("✅ 테스트 통과!")

test_calculate_grade()
```

#### 🏗️ **일상생활의 함수 개념**

**요리에서의 함수:**
```
🍳 계란 후라이 만들기 = make_fried_egg()
🍜 라면 끓이기 = cook_ramen()
🥗 샐러드 만들기 = make_salad()

전체 요리 = make_fried_egg() + cook_ramen() + make_salad()
```

**조직에서의 함수:**
```
📊 회계팀 = calculate_finances()
📈 마케팅팀 = create_marketing_campaign()  
🔧 개발팀 = develop_software()

회사 운영 = calculate_finances() + create_marketing_campaign() + develop_software()
```

함수는 이미 우리 일상 곳곳에 있는 자연스러운 개념입니다!

### 📌 핵심 개념 2: 함수의 필요성 - 코드의 중복과 복잡성 문제 (12분)

### 📌 핵심 개념 3: 함수 만들기 - 구성 절차와 포맷 (20분)

#### 📝 **함수의 기본 구조와 문법**

**파이썬 함수의 기본 포맷:**
```python
def 함수명(매개변수1, 매개변수2, ...):
    """
    함수 설명 (Docstring)
    """
    # 함수 본문 (실행할 코드)
    return 반환값  # 선택사항
```

**각 부분별 상세 설명:**

**1. def 키워드**
- "define"의 줄임말
- "이제부터 함수를 정의하겠다"는 선언

**2. 함수명 (Function Name)**
- 함수를 식별하는 이름
- snake_case 규칙 사용 (예: calculate_total, get_user_info)
- 동사로 시작하는 것이 좋음 (무엇을 하는지 표현)

**3. 매개변수 (Parameters)**
- 함수가 받을 입력값들
- 괄호 안에 쉼표로 구분
- 없어도 괄호는 필수: `def say_hello():`

**4. 콜론 (:)**
- 함수 정의 시작을 알리는 문법
- 이후 들여쓰기 필수

**5. Docstring (문서화 문자열)**
- 삼중 따옴표로 둘러싼 함수 설명
- 선택사항이지만 강력 권장
- 함수의 목적, 매개변수, 반환값 설명

**6. 함수 본문 (Function Body)**
- 실제 실행될 코드
- 4칸 들여쓰기 필수

**7. return 문**
- 함수의 결과값을 돌려줌
- 선택사항 (없으면 None 반환)

#### 🔨 **함수 작성 5단계 절차**

**단계 1: 문제 분석과 함수 설계**
```python
# 예시 문제: "원의 넓이를 계산하고 싶다"

# 1단계 분석:
# - 입력: 반지름
# - 처리: 넓이 계산 (π × r²)
# - 출력: 넓이 값
# - 함수명: calculate_circle_area
```

**단계 2: 함수 틀 만들기**
```python
def calculate_circle_area(radius):
    """
    원의 넓이를 계산하는 함수
    """
    pass  # 일단 비워두기
```

**단계 3: Docstring 작성하기**
```python
def calculate_circle_area(radius):
    """
    원의 넓이를 계산하는 함수
    
    Args:
        radius (float): 원의 반지름
    
    Returns:
        float: 원의 넓이
        
    Examples:
        >>> calculate_circle_area(5)
        78.54
    """
    pass
```

**단계 4: 함수 본문 구현하기**
```python
import math

def calculate_circle_area(radius):
    """
    원의 넓이를 계산하는 함수
    
    Args:
        radius (float): 원의 반지름
    
    Returns:
        float: 원의 넓이
        
    Examples:
        >>> calculate_circle_area(5)
        78.54
    """
    # 입력값 검증
    if radius < 0:
        return 0
    
    # 넓이 계산
    area = math.pi * radius ** 2
    
    return area
```

**단계 5: 테스트와 개선**
```python
# 테스트 실행
test_radius = 5
result = calculate_circle_area(test_radius)
print(f"반지름 {test_radius}인 원의 넓이: {result:.2f}")

# 다양한 경우 테스트
test_cases = [0, 1, 5, 10, -3]
for r in test_cases:
    area = calculate_circle_area(r)
    print(f"반지름 {r}: 넓이 {area:.2f}")
```

#### 🎯 **매개변수와 반환값 심화**

**매개변수의 다양한 형태:**

**1. 기본 매개변수**
```python
def greet_user(name):
    return f"안녕하세요, {name}님!"

# 사용
message = greet_user("김파이썬")
print(message)  # 안녕하세요, 김파이썬님!
```

**2. 기본값이 있는 매개변수**
```python
def calculate_power(base, exponent=2):
    """거듭제곱 계산 (기본값: 제곱)"""
    return base ** exponent

# 사용
print(calculate_power(5))      # 25 (5²)
print(calculate_power(5, 3))   # 125 (5³)
```

**3. 여러 매개변수**
```python
def calculate_bmi(height, weight, unit="kg/m"):
    """BMI 계산"""
    if unit == "kg/m":
        bmi = weight / (height ** 2)
    else:  # 다른 단위 처리
        bmi = weight / (height ** 2)
    
    return round(bmi, 1)

# 사용
bmi_result = calculate_bmi(1.75, 70)
print(f"BMI: {bmi_result}")  # BMI: 22.9
```

**반환값의 다양한 형태:**

**1. 단일 값 반환**
```python
def get_absolute_value(number):
    """절댓값 반환"""
    if number < 0:
        return -number
    else:
        return number
```

**2. 여러 값 반환 (튜플)**
```python
def divide_with_remainder(dividend, divisor):
    """나눗셈의 몫과 나머지 반환"""
    quotient = dividend // divisor
    remainder = dividend % divisor
    return quotient, remainder

# 사용
q, r = divide_with_remainder(17, 3)
print(f"17 ÷ 3 = {q} 나머지 {r}")  # 17 ÷ 3 = 5 나머지 2
```

**3. 딕셔너리 반환**
```python
def analyze_text(text):
    """텍스트 분석 결과 반환"""
    return {
        "length": len(text),
        "word_count": len(text.split()),
        "uppercase_count": sum(1 for c in text if c.isupper()),
        "lowercase_count": sum(1 for c in text if c.islower())
    }

# 사용
result = analyze_text("Hello Python World!")
print(f"분석 결과: {result}")
```

#### 📋 **함수 명명 규칙과 모범 사례**

**좋은 함수명의 특징:**

**1. 동사로 시작 (무엇을 하는지 표현)**
```python
# ✅ 좋은 예시
def calculate_total(prices):
    return sum(prices)

def validate_email(email):
    return "@" in email

def convert_temperature(celsius):
    return celsius * 9/5 + 32

# ❌ 나쁜 예시
def total(prices):        # 동사가 없음
def email_check(email):   # 애매함
def temp(celsius):        # 축약형
```

**2. 구체적이고 명확한 이름**
```python
# ✅ 좋은 예시
def calculate_monthly_payment(principal, rate, years):
    pass

def get_user_by_email(email_address):
    pass

def format_phone_number(phone):
    pass

# ❌ 나쁜 예시
def calc(a, b, c):       # 너무 축약됨
def get_user(x):         # 애매함
def format_data(data):   # 구체적이지 않음
```

**3. 일관된 명명 패턴**
```python
# ✅ 일관된 패턴
def get_user_name(user_id):
    pass

def get_user_email(user_id):
    pass

def get_user_phone(user_id):
    pass

# ❌ 일관성 없음
def get_user_name(user_id):
    pass

def fetch_email(user_id):    # 다른 동사
    pass

def user_phone(user_id):     # 동사 없음
    pass
```

#### 🎨 **실용적인 함수 예시들**

**예시 1: 사용자 입력 검증 함수**
```python
def validate_age(age_input):
    """
    나이 입력값을 검증하는 함수
    
    Args:
        age_input (str): 사용자가 입력한 나이
    
    Returns:
        tuple: (유효성 여부, 나이 또는 오류 메시지)
    """
    try:
        age = int(age_input)
        if age < 0:
            return False, "나이는 0 이상이어야 합니다."
        elif age > 150:
            return False, "나이는 150 이하여야 합니다."
        else:
            return True, age
    except ValueError:
        return False, "올바른 숫자를 입력해주세요."

# 사용 예시
user_input = input("나이를 입력하세요: ")
is_valid, result = validate_age(user_input)

if is_valid:
    print(f"입력된 나이: {result}세")
else:
    print(f"오류: {result}")
```

**예시 2: 복합 계산 함수**
```python
def calculate_loan_payment(principal, annual_rate, years):
    """
    대출 월 상환금을 계산하는 함수
    
    Args:
        principal (float): 대출 원금
        annual_rate (float): 연 이율 (예: 0.05 = 5%)
        years (int): 대출 기간 (년)
    
    Returns:
        dict: 상환 관련 모든 정보
    """
    # 월 이율과 상환 횟수 계산
    monthly_rate = annual_rate / 12
    num_payments = years * 12
    
    if monthly_rate == 0:  # 무이자 대출
        monthly_payment = principal / num_payments
    else:
        # 복리 계산 공식
        monthly_payment = principal * (
            monthly_rate * (1 + monthly_rate) ** num_payments
        ) / (
            (1 + monthly_rate) ** num_payments - 1
        )
    
    total_payment = monthly_payment * num_payments
    total_interest = total_payment - principal
    
    return {
        "monthly_payment": round(monthly_payment, 0),
        "total_payment": round(total_payment, 0),
        "total_interest": round(total_interest, 0),
        "interest_ratio": round((total_interest / principal) * 100, 1)
    }

# 사용 예시
loan_info = calculate_loan_payment(100000000, 0.035, 20)  # 1억원, 3.5%, 20년
print(f"월 상환금: {loan_info['monthly_payment']:,}원")
print(f"총 상환금: {loan_info['total_payment']:,}원")
print(f"총 이자: {loan_info['total_interest']:,}원")
print(f"이자 비율: {loan_info['interest_ratio']}%")
```

**예시 3: 사용자 인터페이스 함수**
```python
def display_menu():
    """메뉴를 출력하는 함수"""
    print("\n" + "="*30)
    print("   🍕 피자 주문 시스템")
    print("="*30)
    print("1. 피자 주문하기")
    print("2. 주문 내역 확인")
    print("3. 주문 취소하기")
    print("4. 종료")
    print("="*30)

def get_menu_choice():
    """사용자의 메뉴 선택을 받는 함수"""
    while True:
        choice = input("메뉴를 선택하세요 (1-4): ")
        if choice in ['1', '2', '3', '4']:
            return int(choice)
        else:
            print("❌ 1부터 4까지의 숫자를 입력해주세요.")

def confirm_action(message):
    """사용자 확인을 받는 함수"""
    while True:
        response = input(f"{message} (y/n): ").lower()
        if response in ['y', 'yes', '예', 'ㅇ']:
            return True
        elif response in ['n', 'no', '아니오', 'ㄴ']:
            return False
        else:
            print("❌ y 또는 n으로 답해주세요.")

# 사용 예시
display_menu()
user_choice = get_menu_choice()
print(f"선택하신 메뉴: {user_choice}")

if user_choice == 4:
    if confirm_action("정말로 종료하시겠습니까?"):
        print("프로그램을 종료합니다.")
    else:
        print("계속 진행합니다.")
```

#### 💡 **함수 작성 시 주의사항**

**1. 하나의 함수는 하나의 일만 (Single Responsibility)**
```python
# ❌ 나쁜 예: 여러 일을 하는 함수
def process_user_data_and_send_email(user_data):
    # 사용자 데이터 검증
    if not user_data["email"]:
        return False
    
    # 데이터베이스에 저장
    save_to_database(user_data)
    
    # 이메일 발송
    send_welcome_email(user_data["email"])
    
    # 로그 기록
    log_user_registration(user_data)

# ✅ 좋은 예: 각각 분리된 함수들
def validate_user_data(user_data):
    return bool(user_data.get("email"))

def save_user_to_database(user_data):
    # 데이터베이스 저장 로직
    pass

def send_welcome_email(email):
    # 이메일 발송 로직
    pass

def log_user_registration(user_data):
    # 로그 기록 로직
    pass
```

**2. 함수는 10-20줄 이내로 (가독성)**
```python
# ❌ 너무 긴 함수 (50줄 이상)
def giant_function():
    # 수십 줄의 복잡한 로직...
    pass

# ✅ 작은 함수들로 분할
def step1_prepare_data():
    pass

def step2_process_data():
    pass

def step3_save_results():
    pass

def main_process():
    step1_prepare_data()
    step2_process_data()
    step3_save_results()
```

**3. 의미 있는 변수명과 주석**
```python
def calculate_discount(price, customer_type, purchase_amount):
    """
    고객 유형과 구매 금액에 따른 할인 계산
    """
    # 기본 할인율 설정
    base_discount_rate = 0.0
    
    # VIP 고객 할인
    if customer_type == "VIP":
        base_discount_rate = 0.15
    elif customer_type == "GOLD":
        base_discount_rate = 0.10
    
    # 대량 구매 추가 할인
    bulk_discount_rate = 0.05 if purchase_amount > 100000 else 0.0
    
    # 최종 할인율 계산
    total_discount_rate = base_discount_rate + bulk_discount_rate
    discount_amount = price * total_discount_rate
    
    return discount_amount
```

### 📌 핵심 개념 3: 조건문 - 선택의 기술 (15분)

#### 🔀 **조건문의 기본 구조**

**if문의 기본 형태:**
```python
# 기본 if문
age = int(input("나이를 입력하세요: "))

if age >= 18:
    print("성인입니다. 투표할 수 있어요! 🗳️")
```

**if-else문:**
```python
if age >= 18:
    print("성인입니다. 투표할 수 있어요! 🗳️")
else:
    print("미성년자입니다. 조금만 더 기다려주세요! 👶")
```

**if-elif-else문:**
```python
if age >= 65:
    print("경로우대 대상입니다. 🎖️")
elif age >= 18:
    print("성인입니다. 🧑‍💼")
elif age >= 13:
    print("청소년입니다. 🧑‍🎓")
else:
    print("어린이입니다. 👶")
```

#### 📊 **사용자 입력받기 - 동적 프로그래밍의 시작**

**input() 함수로 사용자와 소통하기:**
```python
# 기본 입력받기
name = input("이름을 입력하세요: ")
print(f"안녕하세요, {name}님!")

# 숫자 입력받기
age_str = input("나이를 입력하세요: ")
age = int(age_str)  # 문자열을 정수로 변환

# 한 번에 변환하기
score = float(input("점수를 입력하세요: "))
```

**실용적인 입력 처리:**
```python
def get_user_info():
    """사용자 정보를 입력받는 함수"""
    print("=== 사용자 정보 입력 ===")
    
    name = input("이름: ")
    age = int(input("나이: "))
    
    print("\n회원등급을 선택하세요:")
    print("1. VIP")
    print("2. 일반회원") 
    print("3. 비회원")
    
    membership_choice = input("선택 (1-3): ")
    
    if membership_choice == "1":
        membership = "VIP"
    elif membership_choice == "2":
        membership = "일반"
    else:
        membership = "비회원"
    
    return {
        "name": name,
        "age": age,
        "membership": membership
    }

# 사용자 정보 받기
user = get_user_info()
print(f"\n입력된 정보:")
print(f"이름: {user['name']}")
print(f"나이: {user['age']}")
print(f"회원등급: {user['membership']}")
```

**입력 검증과 오류 처리:**
```python
def get_valid_age():
    """유효한 나이를 입력받을 때까지 반복"""
    while True:
        try:
            age_input = input("나이를 입력하세요 (0-120): ")
            age = int(age_input)
            
            if 0 <= age <= 120:
                return age
            else:
                print("❌ 0부터 120 사이의 나이를 입력해주세요.")
        except ValueError:
            print("❌ 숫자만 입력해주세요.")

# 안전한 나이 입력
user_age = get_valid_age()
print(f"입력된 나이: {user_age}세")
```

#### 🎮 **실용적인 조건문 예시들**

**예시 1: 성적 등급 판정 시스템**
```python
def calculate_grade(score):
    """점수에 따른 등급 계산"""
    if score >= 95:
        return "A+", "최우수"
    elif score >= 90:
        return "A", "우수"
    elif score >= 85:
        return "B+", "양호"
    elif score >= 80:
        return "B", "보통"
    elif score >= 70:
        return "C", "미흡"
    else:
        return "F", "재수강"

# 사용자로부터 점수 입력받기
student_score = float(input("시험 점수를 입력하세요: "))
grade, comment = calculate_grade(student_score)

print(f"점수: {student_score}점")
print(f"등급: {grade}")
print(f"평가: {comment}")
```

**예시 2: 온도별 옷차림 추천**
```python
def recommend_clothing(temperature):
    """온도에 따른 옷차림 추천"""
    if temperature >= 28:
        return "🩱 반팔 + 반바지", "매우 더워요!"
    elif temperature >= 23:
        return "👕 반팔 + 긴바지", "따뜻해요"
    elif temperature >= 17:
        return "👔 긴팔 + 긴바지", "적당해요"
    elif temperature >= 10:
        return "🧥 자켓 + 긴바지", "쌀쌀해요"
    elif temperature >= 0:
        return "🧥 코트 + 목도리", "추워요!"
    else:
        return "🧥❄️ 패딩 + 장갑", "매우 추워요!"

# 현재 온도 입력받기
current_temp = float(input("현재 온도를 입력하세요 (°C): "))
clothing, description = recommend_clothing(current_temp)

print(f"현재 온도: {current_temp}°C")
print(f"추천 옷차림: {clothing}")
print(f"날씨: {description}")
```

---

## ☕ 휴식 시간 (10분)

---

## 🎯 2부: 조건문 심화 - 복잡한 논리 처리 (40분)

### 📌 핵심 개념 1: 논리 연산자 완전 정복 (15분)

#### 🧠 **논리 연산자: and, or, not**

**기본 논리 연산자들:**
```python
# and: 모든 조건이 True여야 True
print("=== AND 연산자 ===")
age = 25
income = 3000000

can_get_loan = age >= 20 and income >= 2000000
print(f"나이 {age}세, 소득 {income:,}원")
print(f"대출 가능: {can_get_loan}")

# or: 하나라도 True면 True
print("\n=== OR 연산자 ===")
is_student = True
has_job = False

can_get_discount = is_student or has_job
print(f"학생: {is_student}, 직장인: {has_job}")
print(f"할인 가능: {can_get_discount}")

# not: True를 False로, False를 True로
print("\n=== NOT 연산자 ===")
is_weekend = False
must_work = not is_weekend
print(f"주말: {is_weekend}")
print(f"일해야 함: {must_work}")
```

**복합 논리 조건 예시:**
```python
def check_movie_rating(age, movie_rating):
    """영화 관람 가능 여부 확인"""
    print(f"나이: {age}세, 영화 등급: {movie_rating}")
    
    if movie_rating == "전체관람가":
        return True, "모든 연령 관람 가능"
    elif movie_rating == "12세" and age >= 12:
        return True, "12세 이상 관람 가능"
    elif movie_rating == "15세" and age >= 15:
        return True, "15세 이상 관람 가능"
    elif movie_rating == "청소년불가" and age >= 18:
        return True, "18세 이상 관람 가능"
    else:
        return False, "연령 제한으로 관람 불가"

# 테스트
viewer_age = int(input("나이를 입력하세요: "))
movie_grade = input("영화 등급을 입력하세요 (전체관람가/12세/15세/청소년불가): ")

can_watch, message = check_movie_rating(viewer_age, movie_grade)
print(f"결과: {message}")
```

#### ⚖️ **논리 연산자 우선순위와 괄호 활용**

```python
# 논리 연산자 우선순위: not > and > or
age = 20
income = 1500000
is_student = True

# ❌ 괄호 없이 쓰면 의도와 다를 수 있음
condition1 = age >= 18 and income > 2000000 or is_student
print(f"조건1 결과: {condition1}")  # True (학생이므로)

# ✅ 괄호로 의도를 명확히 표현
condition2 = age >= 18 and (income > 2000000 or is_student)
print(f"조건2 결과: {condition2}")  # True (성인이면서 학생이므로)

condition3 = (age >= 18 and income > 2000000) or is_student  
print(f"조건3 결과: {condition3}")  # True (학생이므로)

# 복잡한 조건문에서 괄호의 중요성
def check_scholarship_eligibility(gpa, family_income, is_first_generation):
    """장학금 대상자 판정"""
    
    # 성적 우수 장학금: GPA 3.8 이상
    academic_scholarship = gpa >= 3.8
    
    # 저소득층 장학금: 가구소득 3000만원 이하이면서 GPA 3.0 이상
    need_based_scholarship = (family_income <= 30000000) and (gpa >= 3.0)
    
    # 첫 대학생 장학금: 가족 중 첫 대학생이면서 GPA 2.8 이상
    first_gen_scholarship = is_first_generation and (gpa >= 2.8)
    
    # 하나라도 해당되면 장학금 대상
    eligible = academic_scholarship or need_based_scholarship or first_gen_scholarship
    
    return {
        "eligible": eligible,
        "academic": academic_scholarship,
        "need_based": need_based_scholarship,
        "first_gen": first_gen_scholarship
    }

# 사용자 입력받기
print("=== 장학금 대상자 판정 ===")
student_gpa = float(input("GPA를 입력하세요: "))
family_income = int(input("가구소득을 입력하세요 (원): "))
is_first_gen = input("가족 중 첫 대학생인가요? (y/n): ").lower() == 'y'

result = check_scholarship_eligibility(student_gpa, family_income, is_first_gen)

print(f"\n=== 장학금 판정 결과 ===")
print(f"성적 우수 장학금: {'✅' if result['academic'] else '❌'}")
print(f"저소득층 장학금: {'✅' if result['need_based'] else '❌'}")  
print(f"첫 대학생 장학금: {'✅' if result['first_gen'] else '❌'}")
print(f"최종 결과: {'🎉 장학금 대상!' if result['eligible'] else '😔 대상 아님'}")
```

### 📌 핵심 개념 2: 중첩 조건문과 구조화 (15분)

#### 🏗️ **중첩 조건문 - 복잡한 상황 처리**

**기본 중첩 구조:**
```python
def determine_tax_bracket(income, filing_status):
    """소득과 납세자 유형에 따른 세율 계산"""
    
    if filing_status == "single":  # 단독세대
        if income <= 10000000:
            tax_rate = 0.10  # 10%
            bracket = "1구간"
        elif income <= 30000000:
            tax_rate = 0.15  # 15%
            bracket = "2구간"
        elif income <= 50000000:
            tax_rate = 0.25  # 25%
            bracket = "3구간"
        else:
            tax_rate = 0.35  # 35%
            bracket = "4구간"
            
    elif filing_status == "married":  # 부부합산
        if income <= 20000000:
            tax_rate = 0.10  # 10%
            bracket = "1구간"
        elif income <= 50000000:
            tax_rate = 0.15  # 15%  
            bracket = "2구간"
        elif income <= 80000000:
            tax_rate = 0.25  # 25%
            bracket = "3구간"
        else:
            tax_rate = 0.35  # 35%
            bracket = "4구간"
    else:
        tax_rate = 0.10  # 기본세율
        bracket = "기본구간"
    
    tax_amount = income * tax_rate
    
    return {
        "bracket": bracket,
        "rate": tax_rate,
        "amount": tax_amount
    }

# 사용자 입력받기
print("=== 소득세 계산기 ===")
annual_income = int(input("연소득을 입력하세요 (원): "))
print("납세 유형을 선택하세요:")
print("1. 단독세대 (single)")
print("2. 부부합산 (married)")
choice = input("선택 (1 또는 2): ")

filing_type = "single" if choice == "1" else "married"
tax_info = determine_tax_bracket(annual_income, filing_type)

print(f"\n=== 세금 계산 결과 ===")
print(f"연소득: {annual_income:,}원")
print(f"납세유형: {filing_type}")
print(f"세율구간: {tax_info['bracket']}")
print(f"적용세율: {tax_info['rate']:.0%}")
print(f"예상세액: {tax_info['amount']:,.0f}원")
```

**중첩 조건문 최적화 기법:**
```python
# ❌ 과도한 중첩 (읽기 어려움)
def calculate_shipping_complex_bad(weight, distance, is_express, is_fragile):
    if weight > 0:
        if distance > 0:
            if is_express:
                if is_fragile:
                    if weight <= 1:
                        return 15000
                    else:
                        return 20000
                else:
                    if weight <= 1:
                        return 10000
                    else:
                        return 12000
            else:
                if is_fragile:
                    if weight <= 1:
                        return 8000
                    else:
                        return 10000
                else:
                    if weight <= 1:
                        return 5000
                    else:
                        return 7000
    return 0

# ✅ 구조화된 중첩 (읽기 쉬움)
def calculate_shipping_complex_good(weight, distance, is_express, is_fragile):
    """배송비 계산 (구조화된 버전)"""
    
    # 기본 검증
    if weight <= 0 or distance <= 0:
        return 0
    
    # 기본 배송비 결정
    if is_express:
        base_fee = 10000 if weight <= 1 else 12000
    else:
        base_fee = 5000 if weight <= 1 else 7000
    
    # 추가 옵션 적용
    if is_fragile:
        base_fee += 3000  # 안전포장비
    
    if distance > 50:
        base_fee += 2000  # 장거리 추가비
    
    return base_fee

# 사용 비교
print("=== 배송비 계산 비교 ===")
test_weight = 0.8
test_distance = 30
test_express = True
test_fragile = True

result1 = calculate_shipping_complex_bad(test_weight, test_distance, test_express, test_fragile)
result2 = calculate_shipping_complex_good(test_weight, test_distance, test_express, test_fragile)

print(f"복잡한 중첩 버전: {result1:,}원")
print(f"구조화된 버전: {result2:,}원")
print(f"두 결과가 같은가? {result1 == result2}")
```

### 📌 핵심 개념 3: 조건문 활용 패턴 (10분)

#### 🎯 **실용적인 조건문 패턴들**

**패턴 1: 범위 체크**
```python
def categorize_temperature(temp):
    """온도 범위별 분류"""
    if temp < -10:
        return "극한추위", "🥶"
    elif temp < 0:
        return "추위", "🧊"
    elif temp < 10:
        return "쌀쌀함", "😰"
    elif temp < 20:
        return "선선함", "😊"
    elif temp < 30:
        return "따뜻함", "☀️"
    else:
        return "더위", "🔥"

temp = float(input("현재 온도를 입력하세요: "))
category, emoji = categorize_temperature(temp)
print(f"{temp}°C는 {category} {emoji}")
```

**패턴 2: 다중 조건 검사**
```python
def check_password_strength(password):
    """비밀번호 강도 검사"""
    score = 0
    feedback = []
    
    # 길이 검사
    if len(password) >= 8:
        score += 1
    else:
        feedback.append("8자 이상 사용하세요")
    
    # 대문자 포함 검사
    if any(c.isupper() for c in password):
        score += 1
    else:
        feedback.append("대문자를 포함하세요")
    
    # 소문자 포함 검사
    if any(c.islower() for c in password):
        score += 1
    else:
        feedback.append("소문자를 포함하세요")
    
    # 숫자 포함 검사
    if any(c.isdigit() for c in password):
        score += 1
    else:
        feedback.append("숫자를 포함하세요")
    
    # 특수문자 포함 검사
    special_chars = "!@#$%^&*()_+-=[]{}|;:,.<>?"
    if any(c in special_chars for c in password):
        score += 1
    else:
        feedback.append("특수문자를 포함하세요")
    
    # 강도 판정
    if score == 5:
        strength = "매우 강함"
        color = "🟢"
    elif score >= 3:
        strength = "보통"
        color = "🟡"
    else:
        strength = "약함"
        color = "🔴"
    
    return {
        "score": score,
        "strength": strength,
        "color": color,
        "feedback": feedback
    }

# 비밀번호 강도 테스트
user_password = input("비밀번호를 입력하세요: ")
result = check_password_strength(user_password)

print(f"\n=== 비밀번호 강도 분석 ===")
print(f"강도: {result['color']} {result['strength']} ({result['score']}/5)")
if result['feedback']:
    print("개선사항:")
    for suggestion in result['feedback']:
        print(f"  - {suggestion}")
```

**패턴 3: 상태 기반 처리**
```python
def process_order_status(current_status, action):
    """주문 상태에 따른 처리"""
    
    if current_status == "주문접수":
        if action == "결제완료":
            new_status = "결제완료"
            message = "결제가 완료되었습니다."
        elif action == "주문취소":
            new_status = "취소완료"
            message = "주문이 취소되었습니다."
        else:
            new_status = current_status
            message = "잘못된 액션입니다."
            
    elif current_status == "결제완료":
        if action == "배송시작":
            new_status = "배송중"
            message = "배송이 시작되었습니다."
        elif action == "주문취소":
            new_status = "취소처리중"
            message = "취소 처리 중입니다."
        else:
            new_status = current_status
            message = "현재 상태에서는 불가능한 액션입니다."
            
    elif current_status == "배송중":
        if action == "배송완료":
            new_status = "배송완료"
            message = "배송이 완료되었습니다."
        else:
            new_status = current_status
            message = "배송 중에는 취소할 수 없습니다."
            
    elif current_status == "배송완료":
        if action == "구매확정":
            new_status = "구매확정"
            message = "구매가 확정되었습니다."
        elif action == "반품신청":
            new_status = "반품처리중"
            message = "반품 신청이 접수되었습니다."
        else:
            new_status = current_status
            message = "잘못된 액션입니다."
    else:
        new_status = current_status
        message = "알 수 없는 상태입니다."
    
    return new_status, message

# 주문 상태 관리 시뮬레이션
print("=== 주문 상태 관리 시스템 ===")
order_status = "주문접수"

while True:
    print(f"\n현재 주문 상태: {order_status}")
    print("가능한 액션:")
    
    if order_status == "주문접수":
        print("1. 결제완료")
        print("2. 주문취소")
    elif order_status == "결제완료":
        print("1. 배송시작")
        print("2. 주문취소")
    elif order_status == "배송중":
        print("1. 배송완료")
    elif order_status == "배송완료":
        print("1. 구매확정")
        print("2. 반품신청")
    
    print("0. 종료")
    
    choice = input("선택하세요: ")
    
    if choice == "0":
        break
    
    action_map = {
        "1": {"주문접수": "결제완료", "결제완료": "배송시작", "배송중": "배송완료", "배송완료": "구매확정"},
        "2": {"주문접수": "주문취소", "결제완료": "주문취소", "배송완료": "반품신청"}
    }
    
    if choice in action_map and order_status in action_map[choice]:
        action = action_map[choice][order_status]
        order_status, message = process_order_status(order_status, action)
        print(f"✅ {message}")
    else:
        print("❌ 잘못된 선택입니다.")

print("주문 관리를 종료합니다.")
```

---

## ☕ 휴식 시간 (10분)

---

## 🎯 3부: 삼항 연산자와 고급 조건문 활용 (40분)

### 📌 핵심 개념 1: 삼항 연산자 - 간결한 조건 처리 (15분)

#### ⚡ **삼항 연산자 = 한 줄 조건문**

**기본 문법:**
```python
# 일반적인 if-else문
age = 20
if age >= 18:
    status = "성인"
else:
    status = "미성년자"

# 삼항 연산자로 한 줄에!
status = "성인" if age >= 18 else "미성년자"
```

**삼항 연산자의 구조:**
```
값1 if 조건 else 값2
👆      👆        👆
True일때  조건      False일때
```

#### 🎯 **삼항 연산자 활용 예시들**

**예시 1: 최대값/최소값 구하기**
```python
# 두 수 중 큰 값 구하기
a = int(input("첫 번째 숫자: "))
b = int(input("두 번째 숫자: "))

# 일반적인 방법
if a > b:
    max_value = a
else:
    max_value = b

# 삼항 연산자 사용
max_value = a if a > b else b
min_value = a if a < b else b

print(f"더 큰 값: {max_value}")
print(f"더 작은 값: {min_value}")
```

**예시 2: 상태 표시**
```python
def get_battery_status(battery_percentage):
    """배터리 상태 표시"""
    
    # 여러 삼항 연산자 조합
    status = (
        "🔴 위험" if battery_percentage < 10 else
        "🟡 부족" if battery_percentage < 30 else
        "🟢 양호"
    )
    
    # 아이콘만 따로
    icon = "🪫" if battery_percentage < 20 else "🔋"
    
    return f"{icon} {battery_percentage}% ({status})"

# 테스트
for battery in [5, 15, 25, 50, 85]:
    print(get_battery_status(battery))
```

**예시 3: 할인 적용**
```python
def calculate_price_with_discount(original_price, is_member, quantity):
    """회원 여부와 수량에 따른 가격 계산"""
    
    # 회원 할인
    member_discount = 0.1 if is_member else 0.0
    
    # 수량 할인 (10개 이상 구매시)
    quantity_discount = 0.05 if quantity >= 10 else 0.0
    
    # 총 할인율
    total_discount = member_discount + quantity_discount
    
    # 최종 가격
    final_price = original_price * quantity * (1 - total_discount)
    
    return {
        "original": original_price * quantity,
        "discount_rate": total_discount,
        "discount_amount": (original_price * quantity) * total_discount,
        "final": final_price
    }

# 사용자 입력받기
print("=== 할인 가격 계산기 ===")
price = int(input("상품 가격: "))
qty = int(input("구매 수량: "))
membership = input("회원이신가요? (y/n): ").lower() == 'y'

result = calculate_price_with_discount(price, membership, qty)

print(f"\n=== 계산 결과 ===")
print(f"정가: {result['original']:,}원")
print(f"할인율: {result['discount_rate']:.1%}")
print(f"할인액: {result['discount_amount']:,.0f}원")
print(f"최종가: {result['final']:,.0f}원")

# 삼항 연산자로 메시지 표시
savings_message = (
    f"🎉 {result['discount_amount']:,.0f}원 절약!" 
    if result['discount_amount'] > 0 
    else "할인 혜택이 없습니다."
)
print(savings_message)
```

### 📌 핵심 개념 2: 조건문 성능 최적화와 패턴 (15분)

#### ⚡ **Early Return 패턴**

```python
# ❌ 깊은 중첩 (읽기 어려움)
def validate_user_input_bad(username, password, email):
    if username:
        if len(username) >= 3:
            if password:
                if len(password) >= 8:
                    if email:
                        if "@" in email:
                            return True, "유효한 입력입니다."
                        else:
                            return False, "이메일 형식이 잘못되었습니다."
                    else:
                        return False, "이메일을 입력해주세요."
                else:
                    return False, "비밀번호는 8자 이상이어야 합니다."
            else:
                return False, "비밀번호를 입력해주세요."
        else:
            return False, "사용자명은 3자 이상이어야 합니다."
    else:
        return False, "사용자명을 입력해주세요."

# ✅ Early Return 패턴 (읽기 쉬움)
def validate_user_input_good(username, password, email):
    # 빠른 검증으로 조기 반환
    if not username:
        return False, "사용자명을 입력해주세요."
    
    if len(username) < 3:
        return False, "사용자명은 3자 이상이어야 합니다."
    
    if not password:
        return False, "비밀번호를 입력해주세요."
    
    if len(password) < 8:
        return False, "비밀번호는 8자 이상이어야 합니다."
    
    if not email:
        return False, "이메일을 입력해주세요."
    
    if "@" not in email:
        return False, "이메일 형식이 잘못되었습니다."
    
    return True, "유효한 입력입니다."

# 테스트
test_cases = [
    ("", "password123", "test@email.com"),
    ("user", "123", "test@email.com"),
    ("user123", "password123", "invalid-email"),
    ("user123", "password123", "test@email.com")
]

for username, password, email in test_cases:
    is_valid, message = validate_user_input_good(username, password, email)
    print(f"입력: {username}, {password}, {email}")
    print(f"결과: {'✅' if is_valid else '❌'} {message}\n")
```

#### 🎯 **조건문 최적화 기법들**

**기법 1: 조건 순서 최적화**
```python
def check_user_access_optimized(user_role, is_logged_in, has_permission):
    """사용자 접근 권한 확인 (최적화된 버전)"""
    
    # 가장 빨리 실패할 수 있는 조건부터 확인
    if not is_logged_in:  # 가장 흔한 실패 케이스
        return False, "로그인이 필요합니다."
    
    if user_role == "banned":  # 두 번째로 흔한 실패 케이스
        return False, "차단된 사용자입니다."
    
    if not has_permission:  # 세 번째 체크
        return False, "권한이 없습니다."
    
    if user_role in ["admin", "moderator", "user"]:  # 마지막 체크
        return True, "접근 허용"
    
    return False, "알 수 없는 사용자 역할입니다."

# 성능 측정을 위한 시뮬레이션
import time

def performance_test():
    test_users = [
        ("user", False, True),    # 로그인 안됨 (즉시 실패)
        ("banned", True, True),   # 차단된 사용자 (빠른 실패)
        ("user", True, False),    # 권한 없음 (중간 실패)
        ("admin", True, True),    # 성공 케이스
    ]
    
    for user_role, logged_in, permission in test_users:
        start_time = time.time()
        result, message = check_user_access_optimized(user_role, logged_in, permission)
        end_time = time.time()
        
        print(f"역할: {user_role}, 로그인: {logged_in}, 권한: {permission}")
        print(f"결과: {'✅' if result else '❌'} {message}")
        print(f"처리시간: {(end_time - start_time) * 1000:.3f}ms\n")

performance_test()
```

**기법 2: Dictionary를 활용한 조건 분기**
```python
# ❌ 긴 if-elif 체인
def get_day_name_old(day_number):
    if day_number == 1:
        return "월요일"
    elif day_number == 2:
        return "화요일"
    elif day_number == 3:
        return "수요일"
    elif day_number == 4:
        return "목요일"
    elif day_number == 5:
        return "금요일"
    elif day_number == 6:
        return "토요일"
    elif day_number == 7:
        return "일요일"
    else:
        return "잘못된 요일"

# ✅ Dictionary 활용
def get_day_name_new(day_number):
    day_names = {
        1: "월요일",
        2: "화요일", 
        3: "수요일",
        4: "목요일",
        5: "금요일",
        6: "토요일",
        7: "일요일"
    }
    return day_names.get(day_number, "잘못된 요일")

# 더 복잡한 예시: 등급별 혜택
def get_membership_benefits(membership_level):
    benefits = {
        "브론즈": {
            "discount": 0.05,
            "free_shipping": False,
            "priority_support": False,
            "monthly_coupon": 1
        },
        "실버": {
            "discount": 0.10,
            "free_shipping": True,
            "priority_support": False,
            "monthly_coupon": 2
        },
        "골드": {
            "discount": 0.15,
            "free_shipping": True,
            "priority_support": True,
            "monthly_coupon": 3
        },
        "플래티넘": {
            "discount": 0.20,
            "free_shipping": True,
            "priority_support": True,
            "monthly_coupon": 5
        }
    }
    
    return benefits.get(membership_level, {
        "discount": 0.0,
        "free_shipping": False,
        "priority_support": False,
        "monthly_coupon": 0
    })

# 사용자 멤버십 혜택 확인
user_membership = input("멤버십 등급을 입력하세요 (브론즈/실버/골드/플래티넘): ")
benefits = get_membership_benefits(user_membership)

print(f"\n=== {user_membership} 멤버십 혜택 ===")
print(f"할인율: {benefits['discount']:.0%}")
print(f"무료배송: {'✅' if benefits['free_shipping'] else '❌'}")
print(f"우선지원: {'✅' if benefits['priority_support'] else '❌'}")
print(f"월 쿠폰: {benefits['monthly_coupon']}장")
```

### 📌 핵심 개념 3: 실전 조건문 응용 (10분)

#### 🎮 **게임 로직에서의 조건문**

```python
def rock_paper_scissors_game():
    """가위바위보 게임"""
    
    choices = {
        "1": "가위", "가위": "가위",
        "2": "바위", "바위": "바위", 
        "3": "보", "보": "보"
    }
    
    # 컴퓨터 선택 (시뮬레이션)
    import random
    computer_choice = random.choice(["가위", "바위", "보"])
    
    print("=== 가위바위보 게임 ===")
    print("1. 가위")
    print("2. 바위")
    print("3. 보")
    
    user_input = input("선택하세요 (1-3 또는 가위/바위/보): ")
    
    if user_input not in choices:
        return "잘못된 입력입니다."
    
    user_choice = choices[user_input]
    
    print(f"\n당신의 선택: {user_choice}")
    print(f"컴퓨터 선택: {computer_choice}")
    
    # 게임 결과 판정
    if user_choice == computer_choice:
        result = "무승부"
        emoji = "🤝"
    elif (
        (user_choice == "가위" and computer_choice == "보") or
        (user_choice == "바위" and computer_choice == "가위") or
        (user_choice == "보" and computer_choice == "바위")
    ):
        result = "승리"
        emoji = "🎉"
    else:
        result = "패배"
        emoji = "😭"
    
    return f"결과: {emoji} {result}!"

# 게임 실행
game_result = rock_paper_scissors_game()
print(game_result)
```

#### 💰 **금융 계산에서의 조건문**

```python
def calculate_loan_eligibility(age, income, credit_score, existing_debt):
    """대출 자격 심사"""
    
    # 기본 자격 요건 확인
    if age < 19:
        return {
            "approved": False,
            "reason": "만 19세 이상만 대출 가능합니다.",
            "max_amount": 0
        }
    
    if income < 2000000:
        return {
            "approved": False,
            "reason": "최소 소득 요건을 충족하지 않습니다.",
            "max_amount": 0
        }
    
    # 신용점수별 기본 한도
    if credit_score >= 900:
        base_limit = income * 10  # 연소득의 10배
        interest_rate = 0.025     # 2.5%
    elif credit_score >= 800:
        base_limit = income * 8   # 연소득의 8배
        interest_rate = 0.035     # 3.5%
    elif credit_score >= 700:
        base_limit = income * 6   # 연소득의 6배
        interest_rate = 0.045     # 4.5%
    elif credit_score >= 600:
        base_limit = income * 4   # 연소득의 4배
        interest_rate = 0.065     # 6.5%
    else:
        return {
            "approved": False,
            "reason": "신용점수가 너무 낮습니다.",
            "max_amount": 0
        }
    
    # 기존 부채 고려
    debt_ratio = existing_debt / income
    if debt_ratio > 0.8:
        return {
            "approved": False,
            "reason": "부채 비율이 너무 높습니다.",
            "max_amount": 0
        }
    
    # 부채비율에 따른 한도 조정
    if debt_ratio > 0.5:
        adjusted_limit = base_limit * 0.6
    elif debt_ratio > 0.3:
        adjusted_limit = base_limit * 0.8
    else:
        adjusted_limit = base_limit
    
    # 최종 한도는 기존 부채를 제외한 금액
    final_limit = max(0, adjusted_limit - existing_debt)
    
    return {
        "approved": True,
        "max_amount": final_limit,
        "interest_rate": interest_rate,
        "debt_ratio": debt_ratio,
        "recommendation": (
            "우수한 신용등급입니다!" if credit_score >= 800 else
            "양호한 신용등급입니다." if credit_score >= 700 else
            "신용등급 개선을 권장합니다."
        )
    }

# 대출 자격 심사 실행
print("=== 대출 자격 심사 ===")
user_age = int(input("나이: "))
user_income = int(input("연소득 (원): "))
user_credit = int(input("신용점수 (300-950): "))
user_debt = int(input("기존 부채 (원): "))

result = calculate_loan_eligibility(user_age, user_income, user_credit, user_debt)

print(f"\n=== 심사 결과 ===")
if result["approved"]:
    print("✅ 대출 승인")
    print(f"최대 한도: {result['max_amount']:,}원")
    print(f"금리: {result['interest_rate']:.1%}")
    print(f"부채비율: {result['debt_ratio']:.1%}")
    print(f"평가: {result['recommendation']}")
else:
    print("❌ 대출 거절")
    print(f"사유: {result['reason']}")
```

---

## 🎯 실습 시간 (60분)

### 🎯 실습 과제 1: 사각형 내접원 면적 계산기 (20분)

#### 📋 **과제 요구사항**

**알고리즘 말투로 표현:**
1. "사용자로부터 정사각형의 한 변의 길이 a를 입력받는다"
2. "만약 a가 0보다 작거나 같으면 오류 메시지를 출력한다"
3. "그렇지 않으면 다음을 계산한다:"
   - "정사각형의 넓이를 계산한다 (a × a)"
   - "내접하는 원의 반지름을 계산한다 (a ÷ 2)"  
   - "내접원의 넓이를 계산한다 (π × 반지름²)"
   - "좌측 상단 모서리 부분의 넓이를 계산한다 (정사각형 넓이 - 내접원 넓이)"
4. "결과를 사용자가 이해하기 쉽게 출력한다"

**구체적 요구사항:**
- 사용자로부터 정사각형의 한 변 길이 입력받기
- 입력값 검증 (양수인지 확인)
- 정사각형 넓이 계산
- 내접원 넓이 계산 
- 내접원 밖의 모서리 부분 넓이 계산
- 결과를 소수점 둘째 자리까지 출력
- 시각적인 설명 포함

---

### 🎯 실습 과제 2: 소수 찾기 프로그램 (20분)

#### 📋 **과제 요구사항**

**알고리즘 말투로 표현:**
1. "사용자로부터 시작 숫자 a와 끝 숫자 b를 입력받는다"
2. "만약 a가 b보다 크면 오류 메시지를 출력한다"
3. "만약 a가 2보다 작으면 a를 2로 설정한다 (2가 가장 작은 소수)"
4. "a부터 b까지 각 숫자에 대해 반복한다:"
   - "현재 숫자가 소수인지 확인한다"
   - "소수라면 리스트에 추가한다"
5. "소수 확인 방법:"
   - "2부터 현재 숫자의 제곱근까지 반복한다"
   - "만약 나누어떨어지는 수가 있으면 소수가 아니다"
   - "모든 수로 나누어떨어지지 않으면 소수다"
6. "찾은 모든 소수를 출력하고 개수도 함께 출력한다"

**구체적 요구사항:**
- 사용자로부터 범위 입력받기 (시작, 끝)
- 입력값 검증 (시작 ≤ 끝)
- 효율적인 소수 판별 알고리즘 구현
- 찾은 소수들을 리스트로 저장
- 결과를 보기 좋게 출력 (한 줄에 10개씩)
- 총 소수 개수와 통계 정보 제공

---

### 🎯 실습 과제 3: 369 게임 프로그램 (20분)

#### 📋 **과제 요구사항**

**알고리즘 말투로 표현:**
1. "사용자로부터 시작 숫자 a와 끝 숫자 b를 입력받는다"
2. "만약 a가 b보다 크거나 같으면 오류 메시지를 출력한다"
3. "a부터 b까지 각 숫자에 대해 반복한다:"
   - "현재 숫자를 문자열로 변환한다"
   - "3, 6, 9가 포함된 개수를 센다"
   - "만약 3, 6, 9가 포함되어 있으면:"
     - "포함된 개수만큼 '짝'을 출력한다"
   - "그렇지 않으면 숫자 그대로 출력한다"
4. "결과를 한 줄에 10개씩 정렬해서 출력한다"
5. "총 몇 번 박수를 쳤는지 통계를 출력한다"

**구체적 요구사항:**
- 사용자로부터 범위 입력받기
- 입력값 검증
- 각 숫자에서 3, 6, 9 개수 확인
- 3, 6, 9 개수만큼 "짝" 출력
- 일반 숫자는 그대로 출력
- 결과를 표 형태로 정렬해서 출력
- 통계 정보 제공 (총 박수 횟수, 가장 많이 박수 친 숫자 등)

---

## 📚 실습 과제 모범답안

### 🎯 과제 1 모범답안: 사각형 내접원 면적 계산기

```python
#!/usr/bin/env python3
"""
사각형 내접원 면적 계산기
- 정사각형의 한 변 길이를 입력받아
- 내접원과 모서리 부분의 넓이를 계산하는 프로그램
"""

import math

def calculate_square_and_circle_areas(side_length):
    """
    정사각형과 내접원의 넓이를 계산
    
    Args:
        side_length (float): 정사각형의 한 변 길이
    
    Returns:
        dict: 계산 결과들
    """
    # 정사각형 넓이
    square_area = side_length ** 2
    
    # 내접원 반지름 (정사각형 한 변의 절반)
    circle_radius = side_length / 2
    
    # 내접원 넓이
    circle_area = math.pi * (circle_radius ** 2)
    
    # 내접원 밖의 모서리 부분 넓이
    corner_area = square_area - circle_area
    
    return {
        "side_length": side_length,
        "square_area": square_area,
        "circle_radius": circle_radius,
        "circle_area": circle_area,
        "corner_area": corner_area
    }

def display_results(results):
    """계산 결과를 시각적으로 출력"""
    print("\n" + "="*50)
    print("🔲 정사각형 내접원 면적 계산 결과")
    print("="*50)
    
    print(f"정사각형 한 변 길이: {results['side_length']:.2f}")
    print(f"정사각형 넓이: {results['square_area']:.2f}")
    print(f"내접원 반지름: {results['circle_radius']:.2f}")
    print(f"내접원 넓이: {results['circle_area']:.2f}")
    print(f"모서리 부분 넓이: {results['corner_area']:.2f}")
    
    # 비율 계산
    circle_ratio = (results['circle_area'] / results['square_area']) * 100
    corner_ratio = (results['corner_area'] / results['square_area']) * 100
    
    print(f"\n📊 비율 분석:")
    print(f"내접원 비율: {circle_ratio:.1f}%")
    print(f"모서리 비율: {corner_ratio:.1f}%")
    
    # 시각적 표현
    print(f"\n🎨 시각적 표현:")
    print("┌────────────┐")
    print("│  ╭──────╮  │")
    print("│ ╱        ╲ │")
    print("│╱    원    ╲│")
    print("│╲          ╱│")
    print("│ ╲        ╱ │")
    print("│  ╰──────╯  │")
    print("└────────────┘")
    print("회색 부분이 모서리 영역입니다.")

def get_valid_side_length():
    """유효한 한 변 길이를 입력받기"""
    while True:
        try:
            side = float(input("정사각형의 한 변 길이를 입력하세요: "))
            
            if side <= 0:
                print("❌ 한 변의 길이는 0보다 커야 합니다.")
                continue
            
            return side
            
        except ValueError:
            print("❌ 올바른 숫자를 입력해주세요.")

# 메인 프로그램
print("🔲 정사각형 내접원 면적 계산기")
print("="*40)

# 사용자 입력받기
side_length = get_valid_side_length()

# 계산 수행
results = calculate_square_and_circle_areas(side_length)

# 결과 출력
display_results(results)

# 추가 분석
print(f"\n💡 재미있는 사실:")
print(f"원의 넓이는 항상 정사각형 넓이의 π/4 ≈ 78.54% 입니다!")
print(f"따라서 모서리 부분은 항상 전체의 21.46% 정도를 차지합니다.")

actual_ratio = (results['circle_area'] / results['square_area']) * 100
theoretical_ratio = (math.pi / 4) * 100
print(f"이론값: {theoretical_ratio:.2f}%, 실제값: {actual_ratio:.2f}%")
```

### 🎯 과제 2 모범답안: 소수 찾기 프로그램

```python
#!/usr/bin/env python3
"""
소수 찾기 프로그램
- 주어진 범위에서 모든 소수를 찾아 출력하는 프로그램
- 에라토스테네스의 체 알고리즘 사용
"""

import math
import time

def is_prime_simple(n):
    """
    간단한 소수 판별법
    
    Args:
        n (int): 판별할 숫자
    
    Returns:
        bool: 소수 여부
    """
    if n < 2:
        return False
    if n == 2:
        return True
    if n % 2 == 0:
        return False
    
    # 3부터 sqrt(n)까지 홀수만으로 나누어보기
    for i in range(3, int(math.sqrt(n)) + 1, 2):
        if n % i == 0:
            return False
    
    return True

def find_primes_in_range(start, end):
    """
    범위 내의 모든 소수 찾기
    
    Args:
        start (int): 시작 숫자
        end (int): 끝 숫자
    
    Returns:
        list: 찾은 소수들의 리스트
    """
    primes = []
    
    # 범위 조정
    start = max(2, start)  # 2보다 작으면 2로 설정
    
    for num in range(start, end + 1):
        if is_prime_simple(num):
            primes.append(num)
    
    return primes

def display_primes(primes, start, end):
    """소수들을 보기 좋게 출력"""
    print(f"\n🔢 {start}부터 {end}까지의 소수")
    print("="*60)
    
    if not primes:
        print("❌ 해당 범위에는 소수가 없습니다.")
        return
    
    # 10개씩 한 줄에 출력
    for i in range(0, len(primes), 10):
        line_primes = primes[i:i+10]
        formatted_line = " ".join(f"{p:4d}" for p in line_primes)
        print(formatted_line)
    
    print("="*60)
    print(f"📊 통계 정보:")
    print(f"총 소수 개수: {len(primes)}개")
    print(f"가장 작은 소수: {min(primes)}")
    print(f"가장 큰 소수: {max(primes)}")
    
    # 범위 내 소수 밀도
    total_numbers = end - start + 1
    prime_density = (len(primes) / total_numbers) * 100
    print(f"소수 밀도: {prime_density:.2f}%")
    
    # 쌍둥이 소수 찾기 (차이가 2인 소수 쌍)
    twin_primes = []
    for i in range(len(primes) - 1):
        if primes[i+1] - primes[i] == 2:
            twin_primes.append((primes[i], primes[i+1]))
    
    if twin_primes:
        print(f"쌍둥이 소수: {len(twin_primes)}쌍")
        for twin in twin_primes[:5]:  # 처음 5개만 출력
            print(f"  ({twin[0]}, {twin[1]})")
        if len(twin_primes) > 5:
            print(f"  ... 외 {len(twin_primes) - 5}쌍 더")

def get_valid_range():
    """유효한 범위를 입력받기"""
    while True:
        try:
            print("소수를 찾을 범위를 입력하세요:")
            start = int(input("시작 숫자: "))
            end = int(input("끝 숫자: "))
            
            if start > end:
                print("❌ 시작 숫자가 끝 숫자보다 클 수 없습니다.")
                continue
            
            if end - start > 100000:
                confirm = input(f"범위가 매우 큽니다 ({end-start+1}개). 계속하시겠습니까? (y/n): ")
                if confirm.lower() != 'y':
                    continue
            
            return start, end
            
        except ValueError:
            print("❌ 올바른 정수를 입력해주세요.")

# 메인 프로그램
print("🔢 소수 찾기 프로그램")
print("="*30)

# 사용자 입력받기
start_num, end_num = get_valid_range()

print(f"\n🔍 {start_num}부터 {end_num}까지 소수를 찾는 중...")

# 시간 측정 시작
start_time = time.time()

# 소수 찾기
found_primes = find_primes_in_range(start_num, end_num)

# 시간 측정 종료
end_time = time.time()
elapsed_time = end_time - start_time

# 결과 출력
display_primes(found_primes, start_num, end_num)

print(f"\n⏱️  계산 시간: {elapsed_time:.3f}초")

# 유명한 소수 정리와 비교
if end_num >= 100:
    # 소수 정리: n 근처의 소수 밀도는 대략 1/ln(n)
    expected_density = 100 / math.log(end_num)
    actual_density = (len(found_primes) / (end_num - start_num + 1)) * 100
    print(f"📈 이론적 소수 밀도: {expected_density:.2f}%")
    print(f"📊 실제 소수 밀도: {actual_density:.2f}%")
```

### 🎯 과제 3 모범답안: 369 게임 프로그램

```python
#!/usr/bin/env python3
"""
369 게임 프로그램
- 주어진 범위의 숫자에서 3, 6, 9가 포함된 개수만큼 '짝'을 출력
- 포함되지 않은 숫자는 그대로 출력
"""

def count_369_digits(number):
    """
    숫자에서 3, 6, 9의 개수를 세는 함수
    
    Args:
        number (int): 검사할 숫자
    
    Returns:
        int: 3, 6, 9의 총 개수
    """
    number_str = str(number)
    count = 0
    
    for digit in number_str:
        if digit in ['3', '6', '9']:
            count += 1
    
    return count

def play_369_game(start, end):
    """
    369 게임을 실행하고 결과를 반환
    
    Args:
        start (int): 시작 숫자
        end (int): 끝 숫자
    
    Returns:
        tuple: (게임 결과 리스트, 통계 정보)
    """
    results = []
    total_claps = 0
    clap_numbers = []  # 박수 친 숫자들
    max_claps_number = 0
    max_claps_count = 0
    
    for number in range(start, end + 1):
        clap_count = count_369_digits(number)
        
        if clap_count > 0:
            # 3, 6, 9가 포함된 경우
            clap_result = "짝" * clap_count
            results.append(clap_result)
            total_claps += clap_count
            clap_numbers.append(number)
            
            # 가장 많이 박수 친 숫자 기록
            if clap_count > max_claps_count:
                max_claps_count = clap_count
                max_claps_number = number
        else:
            # 3, 6, 9가 없는 경우
            results.append(str(number))
    
    statistics = {
        "total_numbers": end - start + 1,
        "total_claps": total_claps,
        "clap_numbers": clap_numbers,
        "clap_ratio": (len(clap_numbers) / (end - start + 1)) * 100,
        "max_claps_number": max_claps_number,
        "max_claps_count": max_claps_count
    }
    
    return results, statistics

def display_369_results(results, start, end, stats):
    """369 게임 결과를 보기 좋게 출력"""
    print(f"\n🎯 369 게임 결과 ({start} ~ {end})")
    print("="*80)
    
    # 결과를 10개씩 한 줄에 출력
    for i in range(0, len(results), 10):
        line_results = results[i:i+10]
        # 각 결과를 6자리로 맞춰서 정렬
        formatted_line = " ".join(f"{result:>6}" for result in line_results)
        print(formatted_line)
    
    print("="*80)
    
    # 통계 정보 출력
    print(f"📊 통계 정보:")
    print(f"전체 숫자 개수: {stats['total_numbers']}개")
    print(f"박수 친 숫자 개수: {len(stats['clap_numbers'])}개")
    print(f"박수 비율: {stats['clap_ratio']:.1f}%")
    print(f"총 박수 횟수: {stats['total_claps']}번")
    
    if stats['max_claps_count'] > 0:
        print(f"가장 많이 박수 친 숫자: {stats['max_claps_number']} ({stats['max_claps_count']}번)")
    
    # 박수 친 숫자들을 개수별로 분류
    clap_distribution = {}
    for number in stats['clap_numbers']:
        clap_count = count_369_digits(number)
        if clap_count not in clap_distribution:
            clap_distribution[clap_count] = []
        clap_distribution[clap_count].append(number)
    
    print(f"\n🎵 박수 횟수별 분포:")
    for clap_count in sorted(clap_distribution.keys()):
        numbers = clap_distribution[clap_count]
        print(f"  {clap_count}번 박수: {len(numbers)}개 숫자")
        # 처음 10개만 보여주기
        if len(numbers) <= 10:
            print(f"    {numbers}")
        else:
            print(f"    {numbers[:10]} ... 외 {len(numbers)-10}개 더")

def find_interesting_369_patterns(start, end):
    """흥미로운 369 패턴 찾기"""
    print(f"\n🔍 흥미로운 369 패턴:")
    
    # 연속된 박수 숫자들 찾기
    consecutive_claps = []
    current_streak = []
    
    for number in range(start, end + 1):
        if count_369_digits(number) > 0:
            if not current_streak or number == current_streak[-1] + 1:
                current_streak.append(number)
            else:
                if len(current_streak) >= 3:  # 3개 이상 연속
                    consecutive_claps.append(current_streak.copy())
                current_streak = [number]
        else:
            if len(current_streak) >= 3:
                consecutive_claps.append(current_streak.copy())
            current_streak = []
    
    # 마지막 연속 체크
    if len(current_streak) >= 3:
        consecutive_claps.append(current_streak)
    
    if consecutive_claps:
        print(f"연속 박수 구간 (3개 이상):")
        for streak in consecutive_claps[:5]:  # 처음 5개만
            print(f"  {streak[0]} ~ {streak[-1]} ({len(streak)}개 연속)")
    else:
        print("3개 이상 연속 박수 구간이 없습니다.")
    
    # 특별한 숫자들
    special_numbers = []
    for number in range(start, end + 1):
        clap_count = count_369_digits(number)
        if clap_count >= 3:  # 3번 이상 박수
            special_numbers.append((number, clap_count))
    
    if special_numbers:
        print(f"특별한 숫자들 (3번 이상 박수):")
        for number, count in special_numbers[:10]:  # 처음 10개만
            print(f"  {number}: {'짝' * count}")

def get_valid_369_range():
    """유효한 369 게임 범위 입력받기"""
    while True:
        try:
            print("369 게임을 할 범위를 입력하세요:")
            start = int(input("시작 숫자: "))
            end = int(input("끝 숫자: "))
            
            if start >= end:
                print("❌ 시작 숫자는 끝 숫자보다 작아야 합니다.")
                continue
            
            if end - start > 10000:
                confirm = input(f"범위가 매우 큽니다 ({end-start+1}개). 계속하시겠습니까? (y/n): ")
                if confirm.lower() != 'y':
                    continue
            
            return start, end
            
        except ValueError:
            print("❌ 올바른 정수를 입력해주세요.")

# 메인 프로그램
print("🎵 369 게임 프로그램")
print("="*30)
print("숫자에 3, 6, 9가 포함되면 개수만큼 '짝'을 출력합니다!")

# 사용자 입력받기
start_number, end_number = get_valid_369_range()

print(f"\n🎮 {start_number}부터 {end_number}까지 369 게임 시작!")

# 369 게임 실행
game_results, game_stats = play_369_game(start_number, end_number)

# 결과 출력
display_369_results(game_results, start_number, end_number, game_stats)

# 흥미로운 패턴 찾기
find_interesting_369_patterns(start_number, end_number)

print(f"\n🎉 369 게임 완료!")
print(f"총 {game_stats['total_claps']}번 박수를 쳤습니다! 👏")
```

---

## 📚 오늘 배운 내용 정리

### ✅ 핵심 포인트

1. **함수의 필요성**:
   - 복잡한 로직을 작은 단위로 분해
   - 재사용성, 모듈성, 테스트 용이성 확보
   - `process_order()` 같은 복합 함수로 실무 로직 구현

2. **조건문 완전 정복**:
   - 기본 if-elif-else 구조
   - 논리 연산자 (and, or, not)와 우선순위
   - 중첩 조건문과 구조화 기법

3. **사용자 입력 처리**:
   - `input()` 함수로 동적 프로그래밍 구현
   - 입력값 검증과 오류 처리
   - 실용적인 사용자 인터페이스 설계

4. **삼항 연산자**:
   - `값1 if 조건 else 값2` 패턴
   - 간결한 조건 처리 방법
   - 복잡한 조건문의 대안

5. **조건문 최적화**:
   - Early Return 패턴
   - Dictionary 활용한 조건 분기
   - 성능을 고려한 조건 순서 배치

### 🏠 다음 주까지 해볼 과제

1. **함수 활용 연습**:
   - 오늘 실습한 프로그램들을 더 작은 함수들로 분해해보기
   - 각각의 함수가 하나의 책임만 갖도록 리팩토링

2. **조건문 연습**:
   - 일상생활의 복잡한 의사결정을 조건문으로 표현해보기
   - 중첩된 조건문을 Early Return 패턴으로 개선해보기

3. **사용자 입력 프로그램**:
   - 입력 검증이 포함된 다양한 프로그램 만들어보기
   - 메뉴 기반 프로그램 구현해보기

4. **실습 과제 개선**:
   - 오늘의 실습 과제에 더 많은 기능 추가
   - 에러 처리와 사용자 편의성 개선

### 🔮 다음 주 예고

**5주차: 제어문 II - 반복문 및 코드 구조화**
- for문과 while문의 다양한 활용
- 중첩 반복문과 복잡한 패턴 처리
- break, continue를 활용한 반복 제어
- 반복문과 조건문의 조합으로 실제 문제 해결

### 💡 마지막 정리

**지금까지의 성장 과정:**
```
1주차: "프로그래밍이 뭔지 알았다!"
2주차: "어디서든 코딩할 수 있게 되었다!"
3주차: "변수로 복잡한 문제를 해결할 수 있다!"
4주차: "조건문으로 똑똑한 프로그램을 만들 수 있다!"
```

**오늘 여러분이 할 수 있게 된 것들:**
- 🔧 복잡한 로직을 함수로 분해하여 관리하기
- 🎯 다양한 조건을 처리하는 똑똑한 프로그램 만들기
- 💬 사용자와 상호작용하는 동적 프로그램 구현하기
- ⚡ 삼항 연산자로 간결한 조건 처리하기
- 🚀 성능을 고려한 조건문 최적화하기

**실무에서 조건문이 중요한 이유:**
```python
# 실제 서비스에서는 이런 복잡한 조건들이 존재합니다
def calculate_delivery_fee(user, order, location):
    if user.membership == "PREMIUM":
        return 0  # 프리미엄 회원 무료배송
    elif order.amount >= 50000:
        return 0  # 5만원 이상 무료배송
    elif location.is_same_day_available():
        return 3000 if order.is_urgent else 2000
    else:
        return calculate_distance_based_fee(location)
```

이런 복잡한 비즈니스 로직을 조건문으로 정확하게 구현할 수 있어야 합니다!

**중요한 개발 원칙:**
- **단일 책임 원칙**: 함수 하나는 한 가지 일만
- **가독성 우선**: 동작하는 코드보다 읽기 쉬운 코드
- **사용자 중심**: 입력 검증과 친절한 안내 메시지
- **성능 고려**: 불필요한 계산 줄이기

**다음 주 학습을 위한 준비:**
- 오늘 배운 조건문이 반복문과 결합되면 더욱 강력해집니다
- 반복문 안에서 조건문을 사용하는 다양한 패턴을 배우게 됩니다
- 실제 알고리즘 문제를 해결할 수 있는 실력을 갖추게 됩니다

**마지막 격려:**
조건문을 마스터한다는 것은 컴퓨터에게 "상황에 따라 다르게 행동하라"고 명령할 수 있다는 뜻입니다. 이는 인공지능의 기초이기도 하죠!

여러분은 이제 정말로 "생각하는 프로그램"을 만들 수 있습니다. 사용자의 입력에 따라, 상황에 따라, 조건에 따라 다르게 반응하는 똑똑한 프로그램들을 만들어보세요! 🧠✨

다음 주에는 반복문으로 더욱 강력하고 효율적인 프로그램을 만들어봅시다! 💪

---

**🎯 4주차 학습 완료! 수고하셨습니다