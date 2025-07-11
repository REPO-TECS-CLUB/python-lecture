# 7주차: 함수 정의와 문서화
**총 강의시간: 3시간 20분 (200분)**
- 강의: 120분 (3부로 구성)
- 휴식: 20분 (10분씩 2회)
- 실습: 60분

---

## 🎯 1부: 함수의 필요성과 기본 개념 (40분)

### 📌 핵심 개념 1: 중간시험 이후, 새로운 단계로! (8분)

#### 🔄 **지금까지 우리가 마스터한 것들**

**1-6주차 완주! 프로그래밍의 기초 완성** ✅
- **순차구조**: 차례대로 하나씩 실행하기
- **선택구조**: 조건에 따라 다르게 행동하기  
- **반복구조**: 같은 작업을 효율적으로 여러 번 하기
- **자료구조**: 많은 데이터를 체계적으로 관리하기

**오늘부터 해결할 새로운 문제**: 
코드가 점점 길어지고 복잡해지는데, 같은 기능을 여러 곳에서 사용하려면 매번 복사-붙여넣기를 해야 할까? 더 체계적이고 재사용 가능한 방법은 없을까?

#### 🤔 **현실적인 문제 상황: 코드 중복의 지옥**

**예시: 학생 성적 관리 시스템에서 평균 계산**

```python
# 😰 함수 없이 작성하면... (중복이 너무 많다!)

# 1반 학생들 성적 처리
class1_scores = [85, 92, 78, 96, 88]
class1_total = 0
for score in class1_scores:
    class1_total += score
class1_average = class1_total / len(class1_scores)
print(f"1반 평균: {class1_average:.1f}점")

# 2반 학생들 성적 처리 (똑같은 코드 반복!)
class2_scores = [89, 76, 93, 81, 87]
class2_total = 0
for score in class2_scores:
    class2_total += score
class2_average = class2_total / len(class2_scores)
print(f"2반 평균: {class2_average:.1f}점")

# 3반 학생들 성적 처리 (또 똑같은 코드!)
class3_scores = [82, 95, 77, 90, 84]
class3_total = 0
for score in class3_scores:
    class3_total += score
class3_average = class3_total / len(class3_scores)
print(f"3반 평균: {class3_average:.1f}점")
```

**이 코드의 심각한 문제점들:**
1. **코드 중복**: 평균 계산 로직이 3번 반복 🔄
2. **수정의 악몽**: 계산 방식을 바꾸려면 3곳을 모두 수정 😰
3. **실수 위험**: 복사-붙여넣기 할 때 변수명 실수 ❌
4. **확장성 제로**: 반이 10개면? 같은 코드 10번! 📈

#### 💡 **함수의 등장 - 코드 재사용의 마법**

**같은 기능을 함수로 작성하면:**

```python
# ✅ 함수를 사용한 깔끔한 코드

def calculate_average(scores):
    """점수 리스트를 받아서 평균을 계산하는 함수"""
    total = sum(scores)
    average = total / len(scores)
    return average

# 이제 한 줄로 평균 계산!
class1_scores = [85, 92, 78, 96, 88]
class1_avg = calculate_average(class1_scores)
print(f"1반 평균: {class1_avg:.1f}점")

class2_scores = [89, 76, 93, 81, 87]
class2_avg = calculate_average(class2_scores)
print(f"2반 평균: {class2_avg:.1f}점")

class3_scores = [82, 95, 77, 90, 84]
class3_avg = calculate_average(class3_scores)
print(f"3반 평균: {class3_avg:.1f}점")

# 🎉 10개 반? 100개 반? 함수 호출만 추가하면 끝!
```

**함수의 놀라운 효과:**
- 15줄 → 3줄로 압축! 📉
- 수정이 필요하면? 함수 내부만 수정! ⚡
- 실수 위험 제거! ✅
- 가독성 완벽! 👁️

### 📌 핵심 개념 2: 함수의 기본 구조와 작동 원리 (16분)

#### 🏗️ **함수의 기본 문법 구조**

```python
def 함수이름(매개변수들):
    """함수 설명 (Docstring)"""
    실행할 코드
    return 반환값  # 생략 가능
```

#### 📖 **실생활 비유로 이해하는 함수**

**함수 = 전문적인 기계 공장**

```python
# 🏭 "커피 제조 기계" 함수
def make_coffee(coffee_type, sugar_level, milk_type):
    """
    커피를 제조하는 함수
    
    입력재료(매개변수):
    - coffee_type: 커피 종류 ("아메리카노", "라떼" 등)
    - sugar_level: 설탕 단계 (0-5)
    - milk_type: 우유 종류 ("일반우유", "두유" 등)
    
    결과물(반환값):
    - 완성된 커피 정보 문자열
    """
    print(f"☕ {coffee_type} 제조 시작...")
    print(f"   설탕 {sugar_level}단계 추가")
    print(f"   {milk_type} 추가")
    
    result = f"{coffee_type} (설탕 {sugar_level}, {milk_type})"
    print(f"✅ 완성: {result}")
    
    return result

# 기계 사용하기 (함수 호출)
my_coffee = make_coffee("라떼", 2, "두유")
friend_coffee = make_coffee("아메리카노", 0, "일반우유")

print(f"\n내 커피: {my_coffee}")
print(f"친구 커피: {friend_coffee}")
```

#### 🎯 **함수의 핵심 구성 요소들**

**1. 함수 정의 (def)**: 기능을 만들어 등록하는 단계
**2. 매개변수 (Parameters)**: 함수가 받는 입력재료
**3. Docstring**: 함수 사용법 설명서
**4. 함수 본체**: 실제 처리하는 코드
**5. 반환값 (return)**: 함수가 돌려주는 결과물
**6. 함수 호출**: 만들어둔 기능을 실제로 사용하는 것

#### 🔄 **함수 실행 과정 단계별 분석**

```python
def calculate_bmi(weight, height):
    """BMI를 계산하는 함수"""
    print(f"📊 BMI 계산 시작: 몸무게 {weight}kg, 키 {height}cm")
    
    # 키를 미터로 변환
    height_m = height / 100
    print(f"   키 변환: {height}cm → {height_m}m")
    
    # BMI 계산
    bmi = weight / (height_m ** 2)
    print(f"   BMI 계산: {weight} ÷ ({height_m}²) = {bmi:.1f}")
    
    return bmi

# 함수 호출 과정 분석
print("=== 함수 호출 전 ===")
user_weight = float(input("몸무게를 입력하세요 (kg): "))
user_height = float(input("키를 입력하세요 (cm): "))

print("\n=== 함수 호출 중 ===")
result_bmi = calculate_bmi(user_weight, user_height)

print(f"\n=== 함수 호출 후 ===")
print(f"📋 계산 결과: BMI {result_bmi:.1f}")

# BMI 해석 추가
if result_bmi < 18.5:
    interpretation = "저체중"
elif result_bmi < 25:
    interpretation = "정상체중"
elif result_bmi < 30:
    interpretation = "과체중"
else:
    interpretation = "비만"

print(f"💡 해석: {interpretation}")
```

### 📌 핵심 개념 3: 매개변수와 반환값의 다양한 패턴 (16분)

#### 📥 **매개변수 패턴들**

**패턴 1: 매개변수 없는 함수**
```python
def show_welcome_message():
    """환영 메시지를 출력하는 함수"""
    print("=" * 40)
    print("🎉 학생 관리 시스템에 오신 것을 환영합니다!")
    print("=" * 40)

# 사용법
show_welcome_message()
```

**패턴 2: 여러 매개변수를 받는 함수**
```python
def calculate_total_price(price, quantity, discount_rate, tax_rate):
    """총 가격을 계산하는 함수"""
    print(f"💰 가격 계산 중...")
    print(f"   기본 가격: {price:,}원")
    print(f"   수량: {quantity}개")
    print(f"   할인율: {discount_rate*100}%")
    print(f"   세율: {tax_rate*100}%")
    
    subtotal = price * quantity
    discount_amount = subtotal * discount_rate
    after_discount = subtotal - discount_amount
    tax_amount = after_discount * tax_rate
    final_total = after_discount + tax_amount
    
    print(f"   소계: {subtotal:,}원")
    print(f"   할인금액: -{discount_amount:,}원")
    print(f"   세금: +{tax_amount:,}원")
    print(f"   최종 총액: {final_total:,}원")
    
    return final_total

# 사용 예시
product_price = int(input("상품 가격을 입력하세요: "))
buy_quantity = int(input("구매 수량을 입력하세요: "))
discount = float(input("할인율을 입력하세요 (예: 0.1): "))
tax = float(input("세율을 입력하세요 (예: 0.1): "))

total = calculate_total_price(product_price, buy_quantity, discount, tax)
print(f"\n💳 결제 금액: {total:,}원")
```

#### 📤 **반환값 패턴들**

**패턴 1: 반환값 없는 함수 (None 반환)**
```python
def print_student_info(name, age, grade):
    """학생 정보를 출력하는 함수 (반환값 없음)"""
    print(f"👨‍🎓 학생 정보")
    print(f"   이름: {name}")
    print(f"   나이: {age}세")
    print(f"   학년: {grade}학년")
    # return 문이 없으면 자동으로 None 반환

student_name = input("학생 이름을 입력하세요: ")
student_age = int(input("나이를 입력하세요: "))
student_grade = int(input("학년을 입력하세요: "))

print_student_info(student_name, student_age, student_grade)
```

**패턴 2: 여러 값을 반환하는 함수**
```python
def analyze_scores(scores):
    """점수 리스트를 분석하여 통계 정보를 반환하는 함수"""
    if not scores:
        return 0, 0, 0, 0, 0  # 빈 리스트인 경우
    
    total = sum(scores)
    average = total / len(scores)
    maximum = max(scores)
    minimum = min(scores)
    count = len(scores)
    
    print(f"📊 점수 분석 완료:")
    print(f"   총 {count}명의 점수 분석")
    print(f"   합계: {total}점")
    print(f"   평균: {average:.1f}점")
    print(f"   최고점: {maximum}점")
    print(f"   최저점: {minimum}점")
    
    return total, average, maximum, minimum, count

# 사용 예시 - "알고리즘 말투" 접근법

# 1단계: "점수들을 입력받는다"
print("=== 점수 입력 ===")
score_list = []
while True:
    score_input = input("점수를 입력하세요 (완료하려면 'end' 입력): ")
    if score_input.lower() == 'end':
        break
    try:
        score = int(score_input)
        if 0 <= score <= 100:
            score_list.append(score)
            print(f"   {score}점 추가됨 (현재 {len(score_list)}개)")
        else:
            print("   0-100 사이의 점수를 입력해주세요.")
    except ValueError:
        print("   숫자를 입력해주세요.")

# 2단계: "점수들을 분석한다"
if score_list:
    total_sum, avg, max_score, min_score, student_count = analyze_scores(score_list)
    
    # 3단계: "결과를 활용한다"
    print(f"\n🎯 최종 분석 결과:")
    print(f"   전체 학생: {student_count}명")
    print(f"   평균 점수: {avg:.1f}점")
    print(f"   점수 범위: {min_score}점 ~ {max_score}점")
    print(f"   점수 분포: {max_score - min_score}점 차이")
else:
    print("입력된 점수가 없습니다.")
```

---

## ☕ 휴식 시간 (10분)

---

## 🎯 2부: 리스트 슬라이싱 완전 정복과 함수 활용 (40분)

### 📌 핵심 개념 1: 리스트 슬라이싱 [] [:] [::] 완전 이해 (20분)

#### 📋 **슬라이싱이란? - 리스트의 일부분을 잘라내는 마법**

**실생활 비유: 빵 자르기**
```python
# 🍞 긴 바게트 빵을 상상해보세요
bread = ["첫번째", "두번째", "세번째", "네번째", "다섯번째", "여섯번째"]

# 🔪 다양한 방법으로 빵을 자를 수 있습니다
print("전체 빵:", bread)
```

#### 🎯 **기본 인덱싱 [] - 하나씩 접근하기**

```python
# 🎯 기본 인덱싱 - 특정 위치의 요소 하나만 가져오기
fruits = ["사과", "바나나", "오렌지", "포도", "딸기"]

print("=== 기본 인덱싱 [] ===")
print(f"첫 번째 과일: {fruits[0]}")    # 사과
print(f"세 번째 과일: {fruits[2]}")    # 오렌지
print(f"마지막 과일: {fruits[-1]}")    # 딸기 (음수 인덱스)
print(f"뒤에서 두 번째: {fruits[-2]}")  # 포도

# 사용자 입력으로 특정 위치 접근하기
user_input = input("\n몇 번째 과일을 보고 싶나요? (1-5): ")
try:
    index = int(user_input) - 1  # 사용자는 1부터 세지만 파이썬은 0부터
    if 0 <= index < len(fruits):
        print(f"선택한 과일: {fruits[index]}")
    else:
        print("올바른 범위(1-5)를 입력해주세요.")
except ValueError:
    print("숫자를 입력해주세요.")
```

#### ✂️ **기본 슬라이싱 [:] - 범위로 자르기**

```python
# ✂️ 슬라이싱 - 여러 요소를 범위로 가져오기
numbers = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]

print("\n=== 기본 슬라이싱 [:] ===")
print(f"전체 리스트: {numbers}")

# [시작:끝] - 시작 포함, 끝 제외
print(f"처음 3개: {numbers[0:3]}")     # [0, 1, 2]
print(f"중간 부분: {numbers[3:7]}")    # [3, 4, 5, 6] 
print(f"마지막 3개: {numbers[7:10]}")  # [7, 8, 9]

# 생략 형태들
print(f"처음부터 5번째까지: {numbers[:5]}")   # [0, 1, 2, 3, 4]
print(f"5번째부터 끝까지: {numbers[5:]}")    # [5, 6, 7, 8, 9]
print(f"전체 복사: {numbers[:]})")          # [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]

# 음수 인덱스 활용
print(f"뒤에서 3개: {numbers[-3:]}")        # [7, 8, 9]
print(f"뒤에서 5개 제외하고 앞부분: {numbers[:-5]}")  # [0, 1, 2, 3, 4]

# 사용자 입력으로 동적 슬라이싱
print(f"\n숫자 리스트: {numbers}")
start = int(input("시작 위치를 입력하세요 (0-9): "))
end = int(input("끝 위치를 입력하세요 (1-10): "))

if 0 <= start < len(numbers) and 1 <= end <= len(numbers) and start < end:
    sliced = numbers[start:end]
    print(f"결과: {sliced}")
else:
    print("올바른 범위를 입력해주세요.")
```

#### 🔄 **확장 슬라이싱 [::] - 간격을 두고 자르기**

```python
# 🔄 확장 슬라이싱 - 간격(step)을 지정해서 가져오기
alphabet = ['A', 'B', 'C', 'D', 'E', 'F', 'G', 'H', 'I', 'J']

print("\n=== 확장 슬라이싱 [::] ===")
print(f"전체 알파벳: {alphabet}")

# [시작:끝:간격]
print(f"2칸씩 건너뛰기: {alphabet[::2]}")      # ['A', 'C', 'E', 'G', 'I']
print(f"3칸씩 건너뛰기: {alphabet[::3]}")      # ['A', 'D', 'G', 'J']
print(f"1번째부터 2칸씩: {alphabet[1::2]}")    # ['B', 'D', 'F', 'H', 'J']

# 거꾸로 뒤집기 (마법의 음수 step!)
print(f"거꾸로 뒤집기: {alphabet[::-1]}")      # ['J', 'I', 'H', 'G', 'F', 'E', 'D', 'C', 'B', 'A']
print(f"뒤에서부터 2칸씩: {alphabet[::-2]}")   # ['J', 'H', 'F', 'D', 'B']

# 복잡한 패턴들
print(f"중간부분 거꾸로: {alphabet[2:8][::-1]}")  # ['H', 'G', 'F', 'E', 'D', 'C']
print(f"처음 5개에서 2칸씩: {alphabet[:5:2]}")   # ['A', 'C', 'E']

# 사용자 입력으로 패턴 만들기
print(f"\n알파벳 리스트: {alphabet}")
step = int(input("몇 칸씩 건너뛸까요? (1-5, 음수 가능): "))

if step != 0:
    if step > 0:
        result = alphabet[::step]
        print(f"{step}칸씩 건너뛴 결과: {result}")
    else:
        result = alphabet[::step]
        print(f"거꾸로 {abs(step)}칸씩 건너뛴 결과: {result}")
else:
    print("0은 사용할 수 없습니다.")
```

#### 🎮 **슬라이싱 활용 실습 - "알고리즘 말투" 접근법**

**문제**: 사용자로부터 문장을 입력받아 다양한 패턴으로 분석하기

**알고리즘 말투로 요구사항 정리:**
1. "사용자로부터 문장을 입력받는다"
2. "문장을 단어들로 분리한다"
3. "다양한 슬라이싱 패턴을 적용한다"
4. "결과를 보기 좋게 출력한다"

```python
def analyze_text_patterns(text):
    """
    텍스트를 다양한 슬라이싱 패턴으로 분석하는 함수
    
    매개변수:
        text (str): 분석할 텍스트
    
    반환값:
        dict: 분석 결과들을 담은 딕셔너리
    """
    # 1단계: 텍스트를 문자 리스트로 변환
    chars = list(text)
    words = text.split()
    
    print(f"📝 원본 텍스트: '{text}'")
    print(f"📋 문자 개수: {len(chars)}개")
    print(f"📋 단어 개수: {len(words)}개")
    
    # 2단계: 다양한 슬라이싱 패턴 적용
    patterns = {}
    
    # 기본 패턴들
    patterns['first_half'] = chars[:len(chars)//2]
    patterns['second_half'] = chars[len(chars)//2:]
    patterns['first_3_chars'] = chars[:3]
    patterns['last_3_chars'] = chars[-3:]
    
    # 확장 패턴들
    patterns['every_2nd_char'] = chars[::2]
    patterns['every_3rd_char'] = chars[::3]
    patterns['reversed'] = chars[::-1]
    patterns['middle_part'] = chars[len(chars)//4:-len(chars)//4] if len(chars) > 4 else chars
    
    # 단어 단위 패턴들
    if len(words) > 1:
        patterns['first_word'] = words[0]
        patterns['last_word'] = words[-1]
        patterns['words_reversed'] = words[::-1]
        patterns['every_2nd_word'] = words[::2]
    
    return patterns

def display_pattern_results(patterns):
    """패턴 분석 결과를 출력하는 함수"""
    print(f"\n🎯 슬라이싱 패턴 분석 결과:")
    print("="*50)
    
    for pattern_name, result in patterns.items():
        if isinstance(result, list):
            result_str = ''.join(result)
        else:
            result_str = str(result)
        
        pattern_desc = {
            'first_half': '앞쪽 절반',
            'second_half': '뒤쪽 절반', 
            'first_3_chars': '처음 3글자',
            'last_3_chars': '마지막 3글자',
            'every_2nd_char': '2글자마다',
            'every_3rd_char': '3글자마다',
            'reversed': '거꾸로 뒤집기',
            'middle_part': '중간 부분',
            'first_word': '첫 번째 단어',
            'last_word': '마지막 단어',
            'words_reversed': '단어 순서 뒤집기',
            'every_2nd_word': '2번째 단어마다'
        }
        
        desc = pattern_desc.get(pattern_name, pattern_name)
        print(f"  {desc:<15}: '{result_str}'")

# 메인 실행 부분
def run_slicing_demo():
    """슬라이싱 데모 프로그램"""
    print("✂️ 문자열 슬라이싱 분석기")
    print("="*40)
    
    while True:
        user_text = input("\n분석할 문장을 입력하세요 (종료: 'quit'): ").strip()
        
        if user_text.lower() == 'quit':
            print("👋 슬라이싱 분석기를 종료합니다!")
            break
        
        if not user_text:
            print("문장을 입력해주세요.")
            continue
        
        # 패턴 분석 실행
        patterns = analyze_text_patterns(user_text)
        display_pattern_results(patterns)
        
        # 추가 분석 제공
        print(f"\n🔍 추가 분석:")
        print(f"  회문 검사: {'예' if user_text.lower() == user_text.lower()[::-1] else '아니오'}")
        print(f"  모음 개수: {sum(1 for c in user_text.lower() if c in 'aeiou')}개")
        print(f"  자음 개수: {sum(1 for c in user_text.lower() if c.isalpha() and c not in 'aeiou')}개")

# 실행
# run_slicing_demo()  # 주석 해제하여 실행
```

### 📌 핵심 개념 2: 슬라이싱을 활용한 실용적인 함수들 (15분)

#### 🔍 **고급 팁: 제너레이터 표현식과 고급 문법 미리보기**

**잠깐! 코드에서 이상한 문법을 발견했나요?**

인터넷이나 책에서 파이썬 코드를 보다 보면 이런 복잡한 표현들을 발견할 수 있어요:

```python
# 🤔 이런 코드들을 보면 당황하지 마세요!

# 제너레이터 표현식
all(isinstance(score, (int, float)) for score in scores)
any(char.isdigit() for char in password)
sum(1 for char in text if char in 'aeiou')

# 리스트 컴프리헨션  
[char for char in text if char.isalnum()]
[score for score in scores if score >= 60]

# 람다 함수
lambda x: x * 2
max(words, key=lambda word: len(word))

# 📚 이것들은 모두 "고급 기법"들입니다!
# 지금은 이해하지 못해도 괜찮아요!
```

**🎯 각 고급 기법을 기초 방법으로 바꿔보기**

**1. 제너레이터 표현식 → for 루프**
```python
# ❌ 고급: 제너레이터 표현식
result = all(score >= 60 for score in scores)

# ✅ 기초: for 루프로 같은 기능
def check_all_passing(scores):
    for score in scores:
        if score < 60:
            return False
    return True

result = check_all_passing(scores)
```

**2. 리스트 컴프리헨션 → for 루프**
```python
# ❌ 고급: 리스트 컴프리헨션
passing_scores = [score for score in scores if score >= 60]

# ✅ 기초: for 루프로 같은 기능
def get_passing_scores(scores):
    passing_scores = []
    for score in scores:
        if score >= 60:
            passing_scores.append(score)
    return passing_scores

passing_scores = get_passing_scores(scores)
```

**3. 람다 함수 → 일반 함수**
```python
# ❌ 고급: 람다 함수
longest_word = max(words, key=lambda word: len(word))

# ✅ 기초: 일반 함수로 같은 기능
def find_longest_word(words):
    if not words:
        return ""
    
    longest = words[0]
    for word in words:
        if len(word) > len(longest):
            longest = word
    return longest

longest_word = find_longest_word(words)
```

**🔄 실습: 고급 코드를 기초 코드로 변환해보기**

```python
# 문제: 다음 고급 코드와 같은 기능을 기초 방법으로 작성해보세요

# 1. 고급 코드
vowel_count = sum(1 for char in text.lower() if char in 'aeiou')

# 기초 코드로 바꿔보세요:
def count_vowels_basic(text):
    count = 0
    vowels = 'aeiou'
    for char in text.lower():
        if char in vowels:
            count += 1
    return count

# 2. 고급 코드  
even_numbers = [num for num in numbers if num % 2 == 0]

# 기초 코드로 바꿔보세요:
def get_even_numbers_basic(numbers):
    even_numbers = []
    for num in numbers:
        if num % 2 == 0:
            even_numbers.append(num)
    return even_numbers

# 3. 고급 코드
has_uppercase = any(char.isupper() for char in text)

# 기초 코드로 바꿔보세요:
def has_uppercase_basic(text):
    for char in text:
        if char.isupper():
            return True
    return False
```

**왜 기초부터 배워야 할까요?**

1. **이해의 깊이**: 
   - 기초 방법을 완전히 이해해야 고급 방법도 제대로 이해할 수 있어요
   - 문제가 생겼을 때 무엇이 잘못되었는지 파악할 수 있어요

2. **디버깅 능력**: 
   - 기초 방법은 단계별로 확인할 수 있어서 오류를 찾기 쉬워요
   - 고급 방법은 한 줄에 모든 게 압축되어 있어서 디버깅이 어려워요

3. **응용력**: 
   - 기초를 탄탄히 하면 다양한 상황에 맞게 변형할 수 있어요
   - 특별한 조건이나 예외 상황을 처리하기 쉬워요

**🎓 언제 고급 기법을 배울까요?**
- **제너레이터 표현식**: 9주차 (데이터 처리 효율성)
- **리스트 컴프리헨션**: 8주차 (객체지향과 함께)
- **람다 함수**: 10주차 (함수형 프로그래밍 개념)

**📝 지금 단계에서의 학습 전략**
1. 기초 문법을 완벽하게 익히기
2. 함수와 슬라이싱을 자유자재로 사용하기
3. 고급 코드를 보면 기초 방법으로 바꿔보는 연습하기
4. 고급 기법은 나중에 배우더라도 충분해요!

**💡 마지막 조언**
고급 기법들은 결국 **"더 짧고 효율적으로 쓰는 방법"**일 뿐이에요. 기능 자체는 여러분이 지금 배우는 기초 방법과 완전히 동일합니다. 기초가 탄탄하면 고급 기법은 자연스럽게 따라올 거예요! 🌟

#### 🛠️ **슬라이싱 기반 유틸리티 함수들 (기초 방법으로 구현)**

```python
def split_list_into_chunks(data_list, chunk_size):
    """
    리스트를 지정된 크기의 덩어리들로 나누는 함수
    
    매개변수:
        data_list (list): 나눌 리스트
        chunk_size (int): 각 덩어리의 크기
    
    반환값:
        list: 덩어리들의 리스트
    
    사용 예시:
        >>> split_list_into_chunks([1,2,3,4,5,6,7,8,9], 3)
        [[1, 2, 3], [4, 5, 6], [7, 8, 9]]
    """
    chunks = []
    for i in range(0, len(data_list), chunk_size):
        chunk = data_list[i:i + chunk_size]
        chunks.append(chunk)
    return chunks

def get_list_statistics(numbers):
    """
    숫자 리스트의 다양한 통계를 슬라이싱으로 계산하는 함수
    
    매개변수:
        numbers (list): 분석할 숫자 리스트
    
    반환값:
        dict: 통계 정보 딕셔너리
    """
    if not numbers:
        return {"error": "빈 리스트입니다."}
    
    # 정렬된 리스트 생성 (원본 보존)
    sorted_nums = sorted(numbers)
    
    # 슬라이싱을 활용한 통계 계산
    total_count = len(numbers)
    
    # 상위/하위 통계
    top_25_percent = sorted_nums[int(total_count * 0.75):]
    bottom_25_percent = sorted_nums[:int(total_count * 0.25)]
    middle_50_percent = sorted_nums[int(total_count * 0.25):int(total_count * 0.75)]
    
    # 홀수/짝수 분리 (슬라이싱 활용)
    even_numbers = [num for i, num in enumerate(numbers) if i % 2 == 0]
    odd_position_numbers = [num for i, num in enumerate(numbers) if i % 2 == 1]
    
    return {
        "total_count": total_count,
        "first_half": numbers[:total_count//2],
        "second_half": numbers[total_count//2:],
        "top_25_percent": top_25_percent,
        "bottom_25_percent": bottom_25_percent,
        "middle_50_percent": middle_50_percent,
        "even_positions": even_numbers,
        "odd_positions": odd_position_numbers,
        "every_3rd": numbers[::3],
        "reversed": numbers[::-1]
    }

def create_pattern_display(text, pattern_type="normal"):
    """
    텍스트를 다양한 패턴으로 표시하는 함수
    
    매개변수:
        text (str): 표시할 텍스트
        pattern_type (str): 패턴 유형
    
    반환값:
        str: 패턴이 적용된 텍스트
    """
    chars = list(text)
    
    if pattern_type == "normal":
        return ''.join(chars)
    elif pattern_type == "reverse":
        return ''.join(chars[::-1])
    elif pattern_type == "alternate":
        return ''.join(chars[::2])
    elif pattern_type == "wave":
        # ✅ 기초적인 방법으로 대소문자 교체
        result = ""
        for i, char in enumerate(chars):
            if i % 2 == 0:
                result += char.upper()
            else:
                result += char.lower()
        return result
    elif pattern_type == "skip2":
        return ''.join(chars[::3])
    elif pattern_type == "middle_out":
        middle = len(chars) // 2
        return ''.join(chars[middle:] + chars[:middle])
    elif pattern_type == "bookends":
        if len(chars) > 2:
            return ''.join([chars[0], '...', chars[-1]])
        else:
            return ''.join(chars)
    else:
        return ''.join(chars)  # 기본값

# 실용적인 활용 예시
def process_student_scores():
    """학생 점수를 슬라이싱으로 분석하는 함수"""
    print("📊 학생 점수 분석 시스템")
    print("="*40)
    
    # 사용자로부터 점수 입력받기
    scores = []
    print("학생들의 점수를 입력하세요 (완료하려면 'done' 입력):")
    
    while True:
        score_input = input("점수 입력: ").strip()
        if score_input.lower() == 'done':
            break
        
        try:
            score = int(score_input)
            if 0 <= score <= 100:
                scores.append(score)
                print(f"  추가됨: {score}점 (총 {len(scores)}개)")
            else:
                print("  0-100 사이의 점수를 입력해주세요.")
        except ValueError:
            print("  숫자를 입력해주세요.")
    
    if not scores:
        print("입력된 점수가 없습니다.")
        return
    
    # 슬라이싱을 활용한 분석
    print(f"\n📈 점수 분석 결과:")
    print("="*40)
    
    # 기본 정보
    print(f"전체 점수: {scores}")
    print(f"총 학생 수: {len(scores)}명")
    
    # 청킹으로 그룹 나누기
    group_size = int(input(f"\n몇 명씩 그룹으로 나눌까요? (1-{len(scores)}): "))
    if 1 <= group_size <= len(scores):
        groups = split_list_into_chunks(scores, group_size)
        print(f"\n👥 {group_size}명씩 그룹 나누기:")
        for i, group in enumerate(groups, 1):
            avg = sum(group) / len(group)
            print(f"  그룹 {i}: {group} (평균: {avg:.1f}점)")
    
    # 통계 분석
    stats = get_list_statistics(scores)
    print(f"\n📊 상세 통계:")
    print(f"  상위 25%: {stats['top_25_percent']}")
    print(f"  하위 25%: {stats['bottom_25_percent']}")
    print(f"  중간 50%: {stats['middle_50_percent']}")
    print(f"  첫 번째 절반: {stats['first_half']}")
    print(f"  두 번째 절반: {stats['second_half']}")
    print(f"  3번째마다: {stats['every_3rd']}")
    print(f"  점수 역순: {stats['reversed']}")

# 텍스트 패턴 데모
def demonstrate_text_patterns():
    """텍스트 패턴 변환 데모"""
    print("🎨 텍스트 패턴 변환기")
    print("="*30)
    
    user_text = input("변환할 텍스트를 입력하세요: ")
    
    patterns = ["normal", "reverse", "alternate", "wave", "skip2", "middle_out", "bookends"]
    pattern_names = {
        "normal": "원본",
        "reverse": "거꾸로",
        "alternate": "2글자마다", 
        "wave": "물결 패턴",
        "skip2": "3글자마다",
        "middle_out": "중간부터",
        "bookends": "양끝만"
    }
    
    print(f"\n🎭 다양한 패턴 변환:")
    for pattern in patterns:
        result = create_pattern_display(user_text, pattern)
        name = pattern_names[pattern]
        print(f"  {name:<10}: '{result}'")

# 실행 예시 (주석 해제하여 사용)
# process_student_scores()
# demonstrate_text_patterns()
```

---

## ☕ 휴식 시간 (10분)

---

## 🎯 3부: 함수 명명 규칙과 문서화 (40분)

### 📌 핵심 개념 1: 함수 명명 규칙 (snake_case) (15분)

#### 🐍 **파이썬 함수 명명 규칙 (PEP 8)**

**기본 원칙: snake_case 사용**
- 모든 문자는 소문자
- 단어 사이는 언더스코어(_)로 연결
- 동사로 시작하여 "무엇을 하는지" 명확히 표현

#### ✅ **좋은 함수명 vs 나쁜 함수명**

```python
# ❌ 나쁜 함수명들
def f(x, y):  # 너무 짧고 의미 불명확
    return x + y

def CalculateStudentAverage(scores):  # PascalCase (클래스명 스타일)
    return sum(scores) / len(scores)

def calculate_student_average_score_with_validation_and_formatting(scores):  # 너무 길다
    return sum(scores) / len(scores)

def data(nums):  # 명사로 시작, 동작이 불분명
    return max(nums)

# ✅ 좋은 함수명들
def add_numbers(first_number, second_number):
    """두 숫자를 더하는 함수"""
    return first_number + second_number

def calculate_average(score_list):
    """점수 리스트의 평균을 계산하는 함수"""
    return sum(score_list) / len(score_list)

def find_maximum_score(score_list):
    """점수 리스트에서 최고점을 찾는 함수"""
    return max(score_list)

def validate_input_range(value, min_value, max_value):
    """입력값이 지정된 범위 내에 있는지 검증하는 함수"""
    return min_value <= value <= max_value

def format_currency(amount):
    """금액을 통화 형식으로 포맷하는 함수"""
    return f"{amount:,}원"
```

#### 🎯 **함수명 작성 실습 - "알고리즘 말투" 방식**

**문제**: 다음 기능들을 하는 함수들의 적절한 이름을 지어보세요.

**알고리즘 말투로 요구사항 정리:**

1. "문자열을 받아서 거꾸로 뒤집는다"
2. "나이를 받아서 성인인지 미성년자인지 판별한다"
3. "점수 리스트를 받아서 합격자 수를 센다 (60점 이상)"
4. "비밀번호를 받아서 안전한지 검사한다"
5. "온도를 섭씨에서 화씨로 변환한다"

**코드로 구현:**

```python
# 1. 문자열 뒤집기
def reverse_string(text):
    """문자열을 거꾸로 뒤집는 함수"""
    return text[::-1]

# 2. 성인 여부 판별
def check_adult_status(age):
    """나이를 받아서 성인 여부를 판별하는 함수"""
    return age >= 18

# 3. 합격자 수 계산
def count_passing_students(score_list, passing_score=60):
    """점수 리스트에서 합격자 수를 세는 함수"""
    count = 0
    for score in score_list:
        if score >= passing_score:
            count += 1
    return count

# 4. 비밀번호 안전성 검사
def validate_password_strength(password):
    """비밀번호의 안전성을 검사하는 함수"""
    if len(password) < 8:
        return False
    
    # ✅ 기초적인 방법으로 문자 검사
    has_letter = False
    for char in password:
        if char.isalpha():
            has_letter = True
            break
    
    has_digit = False
    for char in password:
        if char.isdigit():
            has_digit = True
            break
    
    has_special = False
    special_chars = "!@#$%^&*"
    for char in password:
        if char in special_chars:
            has_special = True
            break
    
    return has_letter and has_digit and has_special

# 5. 온도 변환
def convert_celsius_to_fahrenheit(celsius):
    """섭씨 온도를 화씨로 변환하는 함수"""
    fahrenheit = (celsius * 9/5) + 32
    return fahrenheit

# 실사용 예시
user_text = input("뒤집을 문자열을 입력하세요: ")
reversed_text = reverse_string(user_text)
print(f"뒤집힌 결과: {reversed_text}")

user_age = int(input("나이를 입력하세요: "))
is_adult = check_adult_status(user_age)
status = "성인" if is_adult else "미성년자"
print(f"상태: {status}")
```

### 📌 핵심 개념 2: Docstring을 활용한 함수 문서화 (15분)

#### 📚 **Docstring의 중요성과 작성법**

**Docstring = 함수 사용법 설명서**

```python
def calculate_loan_payment(principal, annual_rate, years):
    """
    대출 월 상환금을 계산하는 함수
    
    매개변수:
        principal (float): 대출 원금 (원)
        annual_rate (float): 연 이자율 (소수점 형태, 예: 0.05 = 5%)
        years (int): 대출 기간 (년)
    
    반환값:
        float: 월 상환금 (원)
    
    사용 예시:
        >>> calculate_loan_payment(10000000, 0.03, 5)
        179856.13
        
    주의사항:
        - 이자율은 소수점 형태로 입력 (5% → 0.05)
        - 대출 기간은 년 단위로 입력
    """
    monthly_rate = annual_rate / 12
    total_months = years * 12
    
    if monthly_rate == 0:  # 무이자 대출인 경우
        return principal / total_months
    
    monthly_payment = (principal * monthly_rate * 
                      (1 + monthly_rate) ** total_months) / \
                     ((1 + monthly_rate) ** total_months - 1)
    
    return round(monthly_payment, 2)
```

#### 🎯 **실용적인 함수 작성 실습**

**문제**: 학생 성적 관리를 위한 종합 함수 만들기

**알고리즘 말투로 요구사항 정리:**
1. "학생 정보와 점수들을 받는다"
2. "평균을 계산한다"
3. "등급을 결정한다 (A: 90+, B: 80+, C: 70+, D: 60+, F: 60-)"
4. "결과를 보기 좋게 포맷하여 반환한다"

**코드로 구현:**

```python
def create_student_report(student_name, student_id, scores):
    """
    학생의 성적표를 생성하는 함수
    
    매개변수:
        student_name (str): 학생 이름
        student_id (str): 학번
        scores (list): 점수 리스트 [국어, 영어, 수학]
    
    반환값:
        dict: 학생 성적 정보를 담은 딕셔너리
        {
            'name': 학생 이름,
            'id': 학번,
            'scores': 점수 리스트,
            'average': 평균 점수,
            'grade': 학점,
            'status': 합격/불합격
        }
    
    사용 예시:
        >>> scores = [85, 92, 78]
        >>> result = create_student_report("김철수", "2024001", scores)
        >>> print(result['average'])
        85.0
    """
    # 입력 검증
    if not scores or len(scores) != 3:
        return {"error": "점수는 정확히 3개(국어, 영어, 수학)를 입력해야 합니다."}
    
    if not all(0 <= score <= 100 for score in scores):
        return {"error": "모든 점수는 0-100 사이여야 합니다."}
    
    # 평균 계산
    average = sum(scores) / len(scores)
    
    # 등급 결정
    if average >= 90:
        grade = "A"
    elif average >= 80:
        grade = "B"
    elif average >= 70:
        grade = "C"
    elif average >= 60:
        grade = "D"
    else:
        grade = "F"
    
    # 합격/불합격 결정
    status = "합격" if average >= 60 else "불합격"
    
    # 결과 딕셔너리 생성
    report = {
        'name': student_name,
        'id': student_id,
        'scores': scores,
        'average': round(average, 1),
        'grade': grade,
        'status': status
    }
    
    return report

def print_formatted_report(report_data):
    """
    성적표 데이터를 보기 좋게 출력하는 함수
    
    매개변수:
        report_data (dict): create_student_report 함수의 반환값
    
    반환값:
        None (출력 전용 함수)
    """
    if 'error' in report_data:
        print(f"❌ 오류: {report_data['error']}")
        return
    
    print("=" * 40)
    print("📋 학생 성적표")
    print("=" * 40)
    print(f"👨‍🎓 이름: {report_data['name']}")
    print(f"🆔 학번: {report_data['id']}")
    print(f"📊 점수:")
    print(f"   국어: {report_data['scores'][0]}점")
    print(f"   영어: {report_data['scores'][1]}점")
    print(f"   수학: {report_data['scores'][2]}점")
    print(f"📈 평균: {report_data['average']}점")
    print(f"🎯 학점: {report_data['grade']}")
    print(f"✅ 결과: {report_data['status']}")
    print("=" * 40)

# 실사용 예시 - 사용자 입력과 함께
print("=== 학생 성적 입력 시스템 ===")
name = input("학생 이름을 입력하세요: ")
student_id = input("학번을 입력하세요: ")

print("\n📝 점수를 입력하세요:")
korean = int(input("국어 점수: "))
english = int(input("영어 점수: "))
math = int(input("수학 점수: "))

scores = [korean, english, math]

# 성적표 생성 및 출력
report = create_student_report(name, student_id, scores)
print_formatted_report(report)
```

### 📌 핵심 개념 3: 기본 매개변수와 키워드 매개변수 (10분)

#### 🔧 **기본 매개변수 (Default Parameters)**

```python
def greet_student(name, grade=1, school="우리학교"):
    """
    학생에게 인사하는 함수
    
    매개변수:
        name (str): 학생 이름 (필수)
        grade (int): 학년, 기본값은 1학년
        school (str): 학교명, 기본값은 "우리학교"
    """
    message = f"안녕하세요, {school} {grade}학년 {name}님!"
    print(message)
    return message

# 다양한 호출 방법
greet_student("김철수")  # 기본값 사용
greet_student("이영희", 3)  # 학년만 지정
greet_student("박민수", 2, "서울고등학교")  # 모든 값 지정

# 키워드 인수 사용
greet_student("최지영", school="부산중학교")  # 순서 바꿔서 지정
greet_student(grade=3, name="정수현", school="대구고등학교")  # 완전히 순서 바꿈
```

#### 🎯 **실용적인 계산기 함수 만들기**

```python
def calculate_with_options(num1, num2, operation="+", show_process=True, decimal_places=2):
    """
    두 수의 연산을 수행하는 고급 계산기 함수
    
    매개변수:
        num1 (float): 첫 번째 숫자
        num2 (float): 두 번째 숫자
        operation (str): 연산자 (+, -, *, /), 기본값은 "+"
        show_process (bool): 계산 과정 출력 여부, 기본값은 True
        decimal_places (int): 소수점 자리수, 기본값은 2
    
    반환값:
        float: 계산 결과
    """
    if show_process:
        print(f"🔢 계산 시작: {num1} {operation} {num2}")
    
    if operation == "+":
        result = num1 + num2
    elif operation == "-":
        result = num1 - num2
    elif operation == "*":
        result = num1 * num2
    elif operation == "/":
        if num2 == 0:
            print("❌ 오류: 0으로 나눌 수 없습니다!")
            return None
        result = num1 / num2
    else:
        print(f"❌ 지원하지 않는 연산자: {operation}")
        return None
    
    # 소수점 자리수 조정
    result = round(result, decimal_places)
    
    if show_process:
        print(f"✅ 결과: {result}")
    
    return result

# 사용 예시 - 사용자 입력과 함께
print("=== 고급 계산기 ===")
first_num = float(input("첫 번째 숫자를 입력하세요: "))
second_num = float(input("두 번째 숫자를 입력하세요: "))
op = input("연산자를 입력하세요 (+, -, *, /): ")

# 다양한 호출 방법
print("\n--- 기본 설정으로 계산 ---")
result1 = calculate_with_options(first_num, second_num, op)

print("\n--- 계산 과정 숨기고 소수점 4자리로 ---")
result2 = calculate_with_options(first_num, second_num, op, 
                                show_process=False, decimal_places=4)
print(f"조용한 계산 결과: {result2}")

print("\n--- 키워드 인수로 호출 ---")
result3 = calculate_with_options(
    num1=first_num, 
    num2=second_num, 
    operation=op, 
    decimal_places=1, 
    show_process=True
)
```

---

## ☕ 휴식 시간 (10분)

---

## 🎯 4부: 함수의 책임 분리와 실습 프로젝트 (40분)

### 📌 핵심 개념 1: 함수의 책임 분리와 단일 기능 원칙 (15분)

#### 🎯 **단일 책임 원칙 (Single Responsibility Principle)**

**나쁜 예: 하나의 함수가 너무 많은 일을 하는 경우**

```python
# ❌ 너무 많은 책임을 가진 함수
def manage_student_everything(name, scores):
    """학생 관련 모든 처리를 하는 함수 (잘못된 설계)"""
    # 입력 검증
    if not name or not scores:
        return "오류: 입력 데이터가 부족합니다"
    
    # 평균 계산
    average = sum(scores) / len(scores)
    
    # 등급 계산
    if average >= 90:
        grade = "A"
    elif average >= 80:
        grade = "B"
    else:
        grade = "C"
    
    # 데이터베이스 저장 (가상)
    print(f"데이터베이스에 저장: {name}, {average}, {grade}")
    
    # 이메일 발송 (가상)
    print(f"이메일 발송: {name}님의 성적표")
    
    # 출력
    print(f"학생: {name}, 평균: {average}, 등급: {grade}")
    
    return {"name": name, "average": average, "grade": grade}
```

**좋은 예: 책임을 분리한 여러 함수들**

```python
# ✅ 책임이 분리된 함수들
def validate_student_input(name, scores):
    """학생 입력 데이터를 검증하는 함수"""
    if not name or not name.strip():
        return False, "이름이 입력되지 않았습니다."
    
    if not scores or len(scores) == 0:
        return False, "점수가 입력되지 않았습니다."
    
    # ✅ 기초적인 방법으로 숫자 타입 검증
    for score in scores:
        if not isinstance(score, (int, float)):
            return False, "모든 점수는 숫자여야 합니다."
    
    # ✅ 기초적인 방법으로 범위 검증
    for score in scores:
        if not (0 <= score <= 100):
            return False, "모든 점수는 0-100 사이여야 합니다."
    
    return True, "입력 데이터가 유효합니다."

def calculate_average_score(scores):
    """점수들의 평균을 계산하는 함수"""
    if not scores:
        return 0
    return sum(scores) / len(scores)

def determine_grade(average):
    """평균 점수를 기반으로 등급을 결정하는 함수"""
    if average >= 90:
        return "A"
    elif average >= 80:
        return "B"
    elif average >= 70:
        return "C"
    elif average >= 60:
        return "D"
    else:
        return "F"

def create_student_record(name, scores):
    """학생 기록을 생성하는 함수"""
    average = calculate_average_score(scores)
    grade = determine_grade(average)
    
    return {
        "name": name,
        "scores": scores,
        "average": round(average, 1),
        "grade": grade
    }

def format_student_report(student_record):
    """학생 기록을 보고서 형태로 포맷하는 함수"""
    report = f"""
📋 학생 성적 보고서
================================
👨‍🎓 이름: {student_record['name']}
📊 점수: {', '.join(map(str, student_record['scores']))}
📈 평균: {student_record['average']}점
🎯 등급: {student_record['grade']}
================================
"""
    return report

# 메인 처리 함수
def process_student_data(name, scores):
    """학생 데이터를 종합적으로 처리하는 함수"""
    # 1단계: 입력 검증
    is_valid, message = validate_student_input(name, scores)
    if not is_valid:
        return None, f"❌ 오류: {message}"
    
    # 2단계: 학생 기록 생성
    student_record = create_student_record(name, scores)
    
    # 3단계: 보고서 생성
    report = format_student_report(student_record)
    
    return student_record, report

# 실사용 예시
print("=== 학생 성적 처리 시스템 ===")
student_name = input("학생 이름을 입력하세요: ")
subject_scores = []

subjects = ["국어", "영어", "수학", "과학", "사회"]
for subject in subjects:
    while True:
        try:
            score = int(input(f"{subject} 점수를 입력하세요 (0-100): "))
            if 0 <= score <= 100:
                subject_scores.append(score)
                break
            else:
                print("0-100 사이의 점수를 입력해주세요.")
        except ValueError:
            print("숫자를 입력해주세요.")

# 데이터 처리
record, report = process_student_data(student_name, subject_scores)

if record:
    print(report)
    print(f"💾 처리 완료: {record['name']}님의 데이터가 저장되었습니다.")
else:
    print(report)  # 오류 메시지
```

### 📌 핵심 개념 2: 실습 프로젝트 - 간단한 도서 관리 시스템 (25분)

#### 📚 **프로젝트 요구사항 - "알고리즘 말투"로 정리**

**기본 기능들:**
1. "새 도서를 등록한다"
2. "등록된 도서 목록을 조회한다"
3. "특정 도서를 검색한다"
4. "도서 정보를 수정한다"
5. "도서를 삭제한다"
6. "도서 통계를 확인한다"

#### 💻 **단계별 구현**

```python
# 도서 데이터를 저장할 전역 리스트
book_database = []

def create_book_record(title, author, year, genre):
    """
    새로운 도서 기록을 생성하는 함수
    
    매개변수:
        title (str): 도서명
        author (str): 저자명
        year (int): 출판연도
        genre (str): 장르
    
    반환값:
        dict: 도서 정보 딕셔너리
    """
    book = {
        "id": len(book_database) + 1,  # 자동 ID 생성
        "title": title,
        "author": author,
        "year": year,
        "genre": genre,
        "is_available": True  # 대출 가능 여부
    }
    return book

def add_book_to_database(title, author, year, genre):
    """
    도서관에 새 도서를 추가하는 함수
    
    매개변수:
        title (str): 도서명
        author (str): 저자명  
        year (int): 출판연도
        genre (str): 장르
    
    반환값:
        tuple: (성공여부, 메시지)
    """
    # 입력 검증
    if not title or not title.strip():
        return False, "도서명을 입력해주세요."
    
    if not author or not author.strip():
        return False, "저자명을 입력해주세요."
    
    if year < 1000 or year > 2024:
        return False, "올바른 출판연도를 입력해주세요."
    
    # 중복 도서 확인
    for book in book_database:
        if book["title"].lower() == title.lower() and book["author"].lower() == author.lower():
            return False, f"이미 등록된 도서입니다: {title} ({author})"
    
    # 새 도서 생성 및 추가
    new_book = create_book_record(title, author, year, genre)
    book_database.append(new_book)
    
    return True, f"도서가 성공적으로 등록되었습니다. (ID: {new_book['id']})"

def search_books_by_keyword(keyword, search_field="title"):
    """
    키워드로 도서를 검색하는 함수
    
    매개변수:
        keyword (str): 검색할 키워드
        search_field (str): 검색 필드 ("title", "author", "genre")
    
    반환값:
        list: 검색 결과 도서 리스트
    """
    keyword = keyword.lower()
    results = []
    
    for book in book_database:
        if search_field in book:
            if keyword in str(book[search_field]).lower():
                results.append(book)
    
    return results

def display_books(book_list, title="도서 목록"):
    """
    도서 리스트를 보기 좋게 출력하는 함수
    
    매개변수:
        book_list (list): 출력할 도서 리스트
        title (str): 출력할 제목
    """
    print(f"\n📚 {title}")
    print("=" * 80)
    
    if not book_list:
        print("📭 등록된 도서가 없습니다.")
        return
    
    print(f"{'ID':>3} {'제목':<20} {'저자':<15} {'출판연도':<8} {'장르':<10} {'상태':<8}")
    print("-" * 80)
    
    for book in book_list:
        status = "대출가능" if book["is_available"] else "대출중"
        print(f"{book['id']:>3} {book['title']:<20} {book['author']:<15} "
              f"{book['year']:<8} {book['genre']:<10} {status:<8}")
    
    print("-" * 80)
    print(f"총 {len(book_list)}권의 도서")

def get_book_statistics():
    """
    도서관 통계 정보를 계산하는 함수
    
    반환값:
        dict: 통계 정보 딕셔너리
    """
    if not book_database:
        return {
            "total_books": 0,
            "available_books": 0,
            "borrowed_books": 0,
            "genres": {},
            "recent_books": 0
        }
    
    total_books = len(book_database)
    available_books = sum(1 for book in book_database if book["is_available"])
    borrowed_books = total_books - available_books
    
    # 장르별 통계
    genres = {}
    for book in book_database:
        genre = book["genre"]
        genres[genre] = genres.get(genre, 0) + 1
    
    # 최근 도서 (2020년 이후)
    recent_books = sum(1 for book in book_database if book["year"] >= 2020)
    
    return {
        "total_books": total_books,
        "available_books": available_books,
        "borrowed_books": borrowed_books,
        "genres": genres,
        "recent_books": recent_books
    }

def display_statistics():
    """도서관 통계를 출력하는 함수"""
    stats = get_book_statistics()
    
    print("\n📊 도서관 통계")
    print("=" * 40)
    print(f"📚 전체 도서: {stats['total_books']}권")
    print(f"✅ 대출 가능: {stats['available_books']}권")
    print(f"📖 대출 중: {stats['borrowed_books']}권")
    print(f"🆕 최근 도서 (2020년 이후): {stats['recent_books']}권")
    
    if stats['genres']:
        print(f"\n📂 장르별 분포:")
        for genre, count in sorted(stats['genres'].items()):
            print(f"   {genre}: {count}권")

def run_library_system():
    """도서관 관리 시스템의 메인 함수"""
    print("🏛️ 도서관 관리 시스템에 오신 것을 환영합니다!")
    
    while True:
        print("\n" + "="*50)
        print("📋 메뉴")
        print("1. 새 도서 등록")
        print("2. 전체 도서 조회")
        print("3. 도서 검색")
        print("4. 도서관 통계")
        print("5. 프로그램 종료")
        print("="*50)
        
        choice = input("선택하세요 (1-5): ").strip()
        
        if choice == "1":
            print("\n📝 새 도서 등록")
            title = input("도서명: ").strip()
            author = input("저자명: ").strip()
            
            while True:
                try:
                    year = int(input("출판연도: "))
                    break
                except ValueError:
                    print("숫자를 입력해주세요.")
            
            genre = input("장르: ").strip()
            
            success, message = add_book_to_database(title, author, year, genre)
            if success:
                print(f"✅ {message}")
            else:
                print(f"❌ {message}")
        
        elif choice == "2":
            display_books(book_database, "전체 도서 목록")
        
        elif choice == "3":
            print("\n🔍 도서 검색")
            keyword = input("검색할 키워드를 입력하세요: ").strip()
            if keyword:
                results = search_books_by_keyword(keyword)
                display_books(results, f"'{keyword}' 검색 결과")
            else:
                print("검색 키워드를 입력해주세요.")
        
        elif choice == "4":
            display_statistics()
        
        elif choice == "5":
            print("👋 도서관 관리 시스템을 종료합니다. 감사합니다!")
            break
        
        else:
            print("❌ 올바른 메뉴 번호를 선택해주세요.")

# 시스템 실행
if __name__ == "__main__":
    # 테스트용 초기 데이터
    add_book_to_database("파이썬 입문", "김개발", 2023, "프로그래밍")
    add_book_to_database("데이터 분석", "이분석", 2022, "데이터사이언스")
    add_book_to_database("웹 개발", "박웹개발", 2021, "웹개발")
    
    # 메인 시스템 실행
    run_library_system()
```

---

## 🎯 실습 과제

### 과제 1: 기본 함수와 슬라이싱 작성 (쉬운 수준)

**요구사항을 "알고리즘 말투"로 표현:**
1. "두 숫자를 받아서 더 큰 수를 찾는다"
2. "문자열을 받아서 모음의 개수를 센다"
3. "숫자 리스트를 받아서 짝수들만 필터링한다"
4. "리스트를 받아서 앞뒤로 뒤집는다" (슬라이싱 활용)
5. "문자열을 받아서 2글자마다 추출한다" (슬라이싱 활용)

**구현해야 할 함수들:**

```python
def find_maximum(num1, num2):
    """두 숫자 중 더 큰 수를 반환하는 함수"""
    # 여기에 코드 작성

def count_vowels(text):
    """문자열에서 모음(a,e,i,o,u)의 개수를 세는 함수"""
    # 여기에 코드 작성

def filter_even_numbers(number_list):
    """숫자 리스트에서 짝수들만 골라서 새 리스트로 반환하는 함수"""
    # 여기에 코드 작성

def reverse_list(data_list):
    """리스트를 슬라이싱으로 뒤집어서 반환하는 함수"""
    # 여기에 코드 작성 (슬라이싱 [::-1] 사용)

def extract_every_second_char(text):
    """문자열에서 2글자마다 추출하는 함수"""
    # 여기에 코드 작성 (슬라이싱 [::2] 사용)

# 테스트 코드
print(find_maximum(10, 25))  # 25 출력
print(count_vowels("Hello World"))  # 3 출력  
print(filter_even_numbers([1, 2, 3, 4, 5, 6]))  # [2, 4, 6] 출력
print(reverse_list([1, 2, 3, 4, 5]))  # [5, 4, 3, 2, 1] 출력
print(extract_every_second_char("abcdefgh"))  # "aceg" 출력
```

### 과제 2: 슬라이싱 기반 텍스트 분석기 (중간 수준)

**요구사항을 "알고리즘 말투"로 표현:**
1. "사용자로부터 텍스트를 입력받는다"
2. "다양한 슬라이싱 패턴을 적용한다"
3. "회문 여부를 검사한다"
4. "텍스트 통계를 계산한다"
5. "결과를 보기 좋게 출력한다"

**구현해야 할 함수들:**

```python
def analyze_text_structure(text):
    """텍스트 구조를 슬라이싱으로 분석하는 함수"""
    # 여기에 코드 작성

def check_palindrome(text):
    """슬라이싱을 사용하여 회문 여부를 검사하는 함수"""
    # 여기에 코드 작성

def split_text_patterns(text):
    """텍스트를 다양한 패턴으로 분할하는 함수"""
    # 여기에 코드 작성

def create_text_summary(text):
    """텍스트 요약 정보를 생성하는 함수"""
    # 여기에 코드 작성
```

### 과제 3: 실용적인 데이터 처리 함수 작성 (중간 수준)

**요구사항을 "알고리즘 말투"로 표현:**
1. "사용자로부터 여러 학생의 정보를 입력받는다"
2. "각 학생의 성적을 분석한다"
3. "상위/하위 그룹을 슬라이싱으로 분리한다"
4. "전체 클래스의 통계를 계산한다"
5. "결과를 보기 좋게 출력한다"

**구현해야 할 함수들:**

```python
def input_student_data():
    """사용자로부터 학생 정보를 입력받는 함수"""
    # 여기에 코드 작성

def calculate_student_stats(scores):
    """개별 학생의 통계를 계산하는 함수"""
    # 여기에 코드 작성

def group_students_by_performance(all_students):
    """성적에 따라 학생들을 그룹으로 나누는 함수 (슬라이싱 활용)"""
    # 여기에 코드 작성

def calculate_class_stats(all_students):
    """전체 클래스의 통계를 계산하는 함수"""
    # 여기에 코드 작성

def display_results(student_stats, class_stats):
    """결과를 보기 좋게 출력하는 함수"""
    # 여기에 코드 작성
```

---

## 📚 모범답안

### 과제 1 모범답안

```python
def find_maximum(num1, num2):
    """
    두 숫자 중 더 큰 수를 반환하는 함수
    
    매개변수:
        num1 (float): 첫 번째 숫자
        num2 (float): 두 번째 숫자
    
    반환값:
        float: 더 큰 숫자
    """
    if num1 > num2:
        return num1
    else:
        return num2

def count_vowels(text):
    """
    문자열에서 모음(a,e,i,o,u)의 개수를 세는 함수
    
    매개변수:
        text (str): 분석할 문자열
    
    반환값:
        int: 모음의 개수
    """
    vowels = "aeiouAEIOU"
    count = 0
    
    for char in text:
        if char in vowels:
            count += 1
    
    return count

def filter_even_numbers(number_list):
    """
    숫자 리스트에서 짝수들만 골라서 새 리스트로 반환하는 함수
    
    매개변수:
        number_list (list): 정수들의 리스트
    
    반환값:
        list: 짝수들만 포함된 새 리스트
    """
    even_numbers = []
    
    for number in number_list:
        if number % 2 == 0:
            even_numbers.append(number)
    
    return even_numbers

def reverse_list(data_list):
    """
    리스트를 슬라이싱으로 뒤집어서 반환하는 함수
    
    매개변수:
        data_list (list): 뒤집을 리스트
    
    반환값:
        list: 뒤집힌 새 리스트
    """
    return data_list[::-1]

def extract_every_second_char(text):
    """
    문자열에서 2글자마다 추출하는 함수
    
    매개변수:
        text (str): 처리할 문자열
    
    반환값:
        str: 2글자마다 추출한 결과
    """
    return text[::2]
```

### 과제 2 모범답안

```python
def analyze_text_structure(text):
    """
    텍스트 구조를 슬라이싱으로 분석하는 함수
    
    매개변수:
        text (str): 분석할 텍스트
    
    반환값:
        dict: 분석 결과 딕셔너리
    """
    if not text:
        return {"error": "빈 텍스트입니다."}
    
    length = len(text)
    
    analysis = {
        "original": text,
        "length": length,
        "first_half": text[:length//2],
        "second_half": text[length//2:],
        "first_3": text[:3],
        "last_3": text[-3:],
        "every_2nd": text[::2],
        "every_3rd": text[::3],
        "reversed": text[::-1],
        "middle_part": text[length//4:-length//4] if length > 4 else text
    }
    
    return analysis

def check_palindrome(text):
    """
    슬라이싱을 사용하여 회문 여부를 검사하는 함수
    
    매개변수:
        text (str): 검사할 텍스트
    
    반환값:
        bool: 회문이면 True, 아니면 False
    """
    # ✅ 기초적인 방법으로 공백과 특수문자 제거
    cleaned = ""
    for char in text:
        if char.isalnum():  # 알파벳과 숫자만
            cleaned += char.lower()
    
    # 슬라이싱으로 뒤집어서 비교
    return cleaned == cleaned[::-1]

def split_text_patterns(text):
    """
    텍스트를 다양한 패턴으로 분할하는 함수
    
    매개변수:
        text (str): 분할할 텍스트
    
    반환값:
        dict: 다양한 패턴으로 분할된 결과
    """
    words = text.split()
    chars = list(text)
    
    # ✅ 기초적인 방법으로 모음과 자음 분리
    vowels_only = []
    for char in text:
        if char.lower() in 'aeiou':
            vowels_only.append(char)
    
    consonants_only = []
    for char in text:
        if char.isalpha() and char.lower() not in 'aeiou':
            consonants_only.append(char)
    
    patterns = {
        "words_first_half": words[:len(words)//2],
        "words_second_half": words[len(words)//2:],
        "words_every_2nd": words[::2],
        "words_reversed": words[::-1],
        "chars_alternating": chars[::2],
        "chars_reverse_alternating": chars[::-2],
        "vowels_only": vowels_only,
        "consonants_only": consonants_only
    }
    
    # 리스트를 문자열로 변환
    for key, value in patterns.items():
        if isinstance(value, list):
            if key.startswith('chars') or key.endswith('only'):
                patterns[key] = ''.join(value)
            else:
                patterns[key] = ' '.join(value)
    
    return patterns

def create_text_summary(text):
    """
    텍스트 요약 정보를 생성하는 함수
    
    매개변수:
        text (str): 요약할 텍스트
    
    반환값:
        dict: 요약 정보
    """
    words = text.split()
    
    # ✅ 기초적인 방법으로 모음과 자음 개수 계산
    vowel_count = 0
    for char in text.lower():
        if char in 'aeiou':
            vowel_count += 1
    
    consonant_count = 0
    for char in text.lower():
        if char.isalpha() and char not in 'aeiou':
            consonant_count += 1
    
    summary = {
        "total_chars": len(text),
        "total_words": len(words),
        "first_word": words[0] if words else "",
        "last_word": words[-1] if words else "",
        "longest_word": max(words, key=len) if words else "",
        "shortest_word": min(words, key=len) if words else "",
        "middle_words": words[len(words)//4:-len(words)//4] if len(words) > 4 else words,
        "is_palindrome": check_palindrome(text),
        "vowel_count": vowel_count,
        "consonant_count": consonant_count
    }
    
    return summary
```

### 과제 3 모범답안

```python
def input_student_data():
    """
    사용자로부터 학생 정보를 입력받는 함수
    
    반환값:
        list: 학생 정보 딕셔너리들의 리스트
    """
    students = []
    
    while True:
        print(f"\n=== {len(students) + 1}번째 학생 정보 입력 ===")
        name = input("학생 이름 (완료하려면 'done' 입력): ").strip()
        
        if name.lower() == 'done':
            break
        
        if not name:
            print("이름을 입력해주세요.")
            continue
        
        scores = []
        subjects = ["국어", "영어", "수학"]
        
        print(f"{name} 학생의 점수를 입력하세요:")
        for subject in subjects:
            while True:
                try:
                    score = int(input(f"  {subject}: "))
                    if 0 <= score <= 100:
                        scores.append(score)
                        break
                    else:
                        print("  0-100 사이의 점수를 입력해주세요.")
                except ValueError:
                    print("  숫자를 입력해주세요.")
        
        student = {
            "name": name,
            "scores": scores
        }
        students.append(student)
        print(f"✅ {name} 학생 정보가 저장되었습니다.")
    
    return students

def calculate_student_stats(scores):
    """
    개별 학생의 통계를 계산하는 함수
    
    매개변수:
        scores (list): 점수 리스트
    
    반환값:
        dict: 통계 정보 딕셔너리
    """
    if not scores:
        return {"average": 0, "total": 0, "max": 0, "min": 0, "grade": "F"}
    
    total = sum(scores)
    average = total / len(scores)
    maximum = max(scores)
    minimum = min(scores)
    
    # 등급 계산
    if average >= 90:
        grade = "A"
    elif average >= 80:
        grade = "B"
    elif average >= 70:
        grade = "C"
    elif average >= 60:
        grade = "D"
    else:
        grade = "F"
    
    return {
        "total": total,
        "average": round(average, 1),
        "max": maximum,
        "min": minimum,
        "grade": grade
    }

def group_students_by_performance(all_students):
    """
    성적에 따라 학생들을 그룹으로 나누는 함수 (슬라이싱 활용)
    
    매개변수:
        all_students (list): 모든 학생 데이터 리스트
    
    반환값:
        dict: 성적별 그룹 딕셔너리
    """
    if not all_students:
        return {"top": [], "middle": [], "bottom": []}
    
    # 평균 점수로 정렬
    students_with_avg = []
    for student in all_students:
        avg = sum(student["scores"]) / len(student["scores"])
        students_with_avg.append({
            "name": student["name"],
            "scores": student["scores"],
            "average": avg
        })
    
    # 평균 점수로 정렬
    sorted_students = sorted(students_with_avg, key=lambda x: x["average"], reverse=True)
    
    total_count = len(sorted_students)
    
    # 슬라이싱을 사용하여 그룹 나누기
    top_third = total_count // 3
    middle_third = (total_count * 2) // 3
    
    groups = {
        "top": sorted_students[:top_third] if top_third > 0 else [],
        "middle": sorted_students[top_third:middle_third] if middle_third > top_third else [],
        "bottom": sorted_students[middle_third:] if middle_third < total_count else []
    }
    
    return groups

def calculate_class_stats(all_students):
    """
    전체 클래스의 통계를 계산하는 함수
    
    매개변수:
        all_students (list): 모든 학생 데이터 리스트
    
    반환값:
        dict: 클래스 통계 정보
    """
    if not all_students:
        return {"student_count": 0}
    
    all_averages = []
    all_scores = []
    grade_counts = {"A": 0, "B": 0, "C": 0, "D": 0, "F": 0}
    
    for student in all_students:
        stats = calculate_student_stats(student["scores"])
        all_averages.append(stats["average"])
        all_scores.extend(student["scores"])
        grade_counts[stats["grade"]] += 1
    
    # 정렬된 평균 점수로 슬라이싱 활용
    sorted_averages = sorted(all_averages, reverse=True)
    top_25_percent = sorted_averages[:len(sorted_averages)//4] if len(sorted_averages) >= 4 else sorted_averages[:1]
    bottom_25_percent = sorted_averages[-len(sorted_averages)//4:] if len(sorted_averages) >= 4 else sorted_averages[-1:]
    
    class_average = sum(all_averages) / len(all_averages)
    class_max = max(all_scores)
    class_min = min(all_scores)
    
    return {
        "student_count": len(all_students),
        "class_average": round(class_average, 1),
        "class_max": class_max,
        "class_min": class_min,
        "top_25_percent_avg": round(sum(top_25_percent) / len(top_25_percent), 1) if top_25_percent else 0,
        "bottom_25_percent_avg": round(sum(bottom_25_percent) / len(bottom_25_percent), 1) if bottom_25_percent else 0,
        "grade_distribution": grade_counts
    }

def display_results(student_stats, class_stats):
    """
    결과를 보기 좋게 출력하는 함수
    
    매개변수:
        student_stats (list): 학생별 통계 리스트
        class_stats (dict): 클래스 통계
    """
    print("\n" + "="*60)
    print("📊 성적 분석 결과")
    print("="*60)
    
    # 개별 학생 결과
    print("\n👥 개별 학생 성적:")
    print("-"*60)
    print(f"{'이름':<10} {'평균':<6} {'최고':<4} {'최저':<4} {'학점':<4}")
    print("-"*60)
    
    for student_stat in student_stats:
        print(f"{student_stat['name']:<10} "
              f"{student_stat['stats']['average']:<6} "
              f"{student_stat['stats']['max']:<4} "
              f"{student_stat['stats']['min']:<4} "
              f"{student_stat['stats']['grade']:<4}")
    
    # 클래스 통계
    print(f"\n🏫 전체 클래스 통계:")
    print("-"*30)
    print(f"학생 수: {class_stats['student_count']}명")
    print(f"클래스 평균: {class_stats['class_average']}점")
    print(f"최고점: {class_stats['class_max']}점")
    print(f"최저점: {class_stats['class_min']}점")
    print(f"상위 25% 평균: {class_stats.get('top_25_percent_avg', 0)}점")
    print(f"하위 25% 평균: {class_stats.get('bottom_25_percent_avg', 0)}점")
    
    print(f"\n📈 학점 분포:")
    for grade, count in class_stats['grade_distribution'].items():
        if count > 0:
            percentage = (count / class_stats['student_count']) * 100
            print(f"  {grade}학점: {count}명 ({percentage:.1f}%)")

# 메인 실행 함수 (슬라이싱 활용 버전)
def run_grade_analysis_with_slicing():
    """성적 분석 프로그램의 메인 함수 (슬라이싱 기능 포함)"""
    print("📚 학생 성적 분석 프로그램 (슬라이싱 기능 포함)")
    
    # 1단계: 학생 데이터 입력
    students = input_student_data()
    
    if not students:
        print("입력된 학생 데이터가 없습니다.")
        return
    
    # 2단계: 각 학생별 통계 계산
    student_results = []
    for student in students:
        stats = calculate_student_stats(student["scores"])
        student_results.append({
            "name": student["name"],
            "stats": stats
        })
    
    # 3단계: 클래스 통계 계산
    class_stats = calculate_class_stats(students)
    
    # 4단계: 성적별 그룹 분리 (슬라이싱 활용)
    performance_groups = group_students_by_performance(students)
    
    # 5단계: 결과 출력
    display_results(student_results, class_stats)
    
    # 6단계: 그룹별 분석 출력
    print(f"\n🎯 성적별 그룹 분석 (슬라이싱 활용):")
    print("-"*40)
    
    group_names = {"top": "상위권", "middle": "중위권", "bottom": "하위권"}
    for group_key, group_students in performance_groups.items():
        if group_students:
            print(f"\n📊 {group_names[group_key]} ({len(group_students)}명):")
            for student in group_students:
                print(f"  {student['name']}: {student['average']:.1f}점")

# 프로그램 실행
if __name__ == "__main__":
    run_grade_analysis_with_slicing()
```

---

## 📚 오늘 배운 내용 정리

### ✅ 핵심 포인트

1. **함수의 필요성**:
   - 코드 중복 제거와 재사용성 향상
   - 프로그램의 모듈화와 구조화
   - 디버깅과 유지보수의 편의성

2. **리스트 슬라이싱 완전 정복**:
   - 기본 인덱싱 []: 특정 위치 요소 접근
   - 기본 슬라이싱 [:]: 범위 지정으로 여러 요소 추출
   - 확장 슬라이싱 [::]: 간격 지정과 역순 처리
   - 실용적인 데이터 분할과 패턴 추출

3. **함수 설계 원칙**:
   - 단일 책임 원칙: 하나의 함수는 하나의 기능만
   - 명확한 함수명: snake_case와 동사 중심
   - 적절한 매개변수와 반환값 설계

4. **Docstring 문서화**:
   - 함수의 목적과 사용법 명시
   - 매개변수와 반환값 설명
   - 사용 예시와 주의사항 포함

5. **기본 매개변수와 키워드 매개변수**:
   - 함수 호출의 유연성 제공
   - 기본값을 통한 편의성 증대
   - 가독성 있는 함수 호출

6. **함수와 슬라이싱의 조합**:
   - 슬라이싱을 활용한 데이터 처리 함수
   - 텍스트 분석과 패턴 추출
   - 리스트 그룹화와 통계 분석

7. **함수 조합과 모듈화**:
   - 작은 함수들을 조합하여 복잡한 기능 구현
   - 각 함수의 책임을 명확히 분리
   - 테스트와 디버깅이 용이한 구조

### 🏠 다음 주까지 해볼 과제

1. **함수 작성 연습**:
   - 일상생활의 계산을 함수로 만들어보기
   - 각 함수에 적절한 Docstring 작성하기

2. **슬라이싱 활용 연습**:
   - 다양한 슬라이싱 패턴으로 텍스트 처리하기
   - 리스트 분할과 재조합 함수 만들어보기
   - 슬라이싱을 활용한 데이터 분석 함수 작성하기

3. **기존 코드 리팩토링**:
   - 지금까지 작성한 프로그램들을 함수로 분리하기
   - 중복되는 코드들을 함수로 추출하기
   - 슬라이싱으로 개선할 수 있는 부분 찾아보기

4. **실습 과제 완성**:
   - 오늘의 실습 과제를 완전히 구현하기
   - 추가 기능을 함수로 구현해보기
   - 슬라이싱 기반 텍스트 분석기 완성하기

5. **함수와 슬라이싱 조합 연습**:
   - 여러 함수를 조합하여 복잡한 프로그램 만들기
   - 슬라이싱을 활용한 데이터 처리 파이프라인 구축하기
   - 메인 함수에서 다른 함수들을 체계적으로 호출하기

6. **창의적 활용**:
   - 슬라이싱으로 문자열 암호화/복호화 함수 만들기
   - 리스트 셔플링과 정렬 함수 구현하기
   - 패턴 인식과 분석 함수 개발하기

### 🔮 다음 주 예고

**8주차: 객체 지향 프로그래밍과 코딩 규칙**
- 클래스 개념과 객체 생성
- 속성과 메서드의 관계
- 생성자와 매직 메서드 활용
- 접근 제어와 캡슐화 개념

### 💡 마지막 정리

**지금까지의 성장 과정:**
```
1주차: "프로그래밍이 뭔지 알았다!"
2주차: "어디서든 코딩할 수 있게 되었다!"
3주차: "변수로 복잡한 문제를 해결할 수 있다!"
4주차: "조건문으로 똑똑한 프로그램을 만들 수 있다!"
5주차: "반복문으로 효율적인 프로그램을 만들 수 있다!"
6주차: "자료구조로 체계적인 데이터 관리를 할 수 있다!"
7주차: "함수와 슬라이싱으로 재사용 가능하고 강력한 코드를 만들 수 있다!"
```

**오늘 여러분이 할 수 있게 된 것들:**
- 🔧 복잡한 프로그램을 작은 기능 단위로 분해하기
- ✂️ 리스트와 문자열을 자유자재로 슬라이싱하여 원하는 부분 추출하기
- 🔄 [::-1] 같은 고급 슬라이싱으로 데이터 역순 처리하기
- 📊 슬라이싱을 활용한 데이터 그룹화와 통계 분석하기
- 📝 전문적인 문서화로 코드의 품질 높이기
- ♻️ 한 번 작성한 코드를 여러 곳에서 재사용하기
- 🎯 단일 책임 원칙으로 깔끔한 코드 설계하기
- 🔗 여러 함수를 조합하여 복잡한 시스템 구축하기
- 🎨 텍스트 패턴 분석과 변환 기능 구현하기

**함수의 진정한 가치:**
함수는 단순히 코드를 묶는 것이 아니라, **생각을 체계화하는 도구**입니다. 복잡한 문제를 작은 단위로 나누어 해결하는 것은 프로그래밍뿐만 아니라 모든 문제 해결의 핵심입니다.

**실무에서의 중요성:**
```python
# 실제 서비스에서는 수백, 수천 개의 함수가 협력합니다
def authenticate_user(username, password):
    """사용자 인증"""
    pass

def validate_input(data):
    """입력 데이터 검증"""
    pass

def process_user_data(user_data):
    """사용자 데이터 처리 (슬라이싱으로 배치 분할)"""
    batch_size = 100
    for i in range(0, len(user_data), batch_size):
        batch = user_data[i:i + batch_size]  # 슬라이싱으로 배치 처리
        process_batch(batch)

def extract_keywords(text):
    """텍스트에서 키워드 추출 (슬라이싱 활용)"""
    words = text.split()
    important_words = words[::3]  # 3번째마다 추출
    return important_words[:10]   # 상위 10개만

def save_to_database(data):
    """데이터베이스 저장"""
    pass

def send_notification(user, message):
    """알림 발송"""
    pass

# 이 모든 함수들이 조화롭게 동작하여 하나의 서비스를 만듭니다
```

**마지막 격려:**
함수를 마스터한다는 것은 프로그래밍의 핵심 철학인 **"분할 정복(Divide and Conquer)"**을 체득한 것입니다. 그리고 오늘 배운 슬라이싱은 데이터를 **"원하는 대로 자르고 조합하는"** 강력한 도구입니다. 이제 여러분은 어떤 복잡한 문제든 작은 단위로 나누어 차근차근 해결하고, 데이터를 자유자재로 다룰 수 있어요!

**슬라이싱의 마법:**
```python
# 이제 여러분은 이런 마법을 부릴 수 있습니다
data = "Hello World!"
print(data[::-1])      # "!dlroW olleH" - 순식간에 뒤집기
print(data[::2])       # "HloWrd" - 2글자마다 추출
print(data[1::2])      # "el ol!" - 다른 패턴으로 추출
```

오늘 배운 함수 설계 원칙들은 앞으로 배울 객체 지향 프로그래밍의 기초가 됩니다. 함수에서 시작된 모듈화 사고방식이 클래스와 객체로 발전하게 될 거예요! 그리고 슬라이싱은 데이터 처리의 핵심 기술로 계속 활용될 것입니다! 🌟

다음 주에는 클래스와 객체를 통해 더욱 체계적이고 현실적인 프로그래밍을 경험해봅시다! 💪

---

**🎯 7주차 학습 완료! 수고하셨습니다! 🎉**