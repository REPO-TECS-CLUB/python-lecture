# 5주차: 제어문 II - 반복문 및 코드 구조화
**총 강의시간: 3시간 20분 (200분)**
- 강의: 120분 (3부로 구성)
- 휴식: 20분 (10분씩 2회)
- 실습: 60분

---

## 🎯 1부: 반복문이 왜 필요할까? - 똑같은 일을 효율적으로 처리하는 방법 (40분)

### 📌 핵심 개념 1: 지금까지의 여정과 새로운 도전 (8분)

#### 🔄 **지금까지 우리가 마스터한 것들**

**1주차**: 프로그래밍의 3대 마법 구조 발견
- 순차: "차례대로 하나씩" ✅
- 선택: "상황에 따라 다르게" ✅
- 반복: "조건 만족할 때까지 계속" ← 오늘의 주인공!

**2주차**: 개발환경 완전 정복 ✅

**3주차**: 변수와 자료형으로 복잡한 데이터 처리 ✅

**4주차**: 조건문으로 똑똑한 판단력 구현 ✅

**오늘 해결할 문제**: 
똑같은 작업을 여러 번 해야 할 때, 코드를 복사-붙여넣기 하지 않고 어떻게 효율적으로 처리할 수 있을까?

#### 🤔 **현실적인 문제 상황: 반복 작업의 지옥**

**예시: "안녕하세요"를 5번 출력하기**

```python
# 😰 반복문 없이 (끔찍한 코드!)
print("안녕하세요")
print("안녕하세요")
print("안녕하세요")
print("안녕하세요")
print("안녕하세요")

# 만약 100번 출력한다면? 100줄...
# 만약 1000번 출력한다면? 1000줄...
```

**이 코드의 문제점들:**
1. **코드 중복**: 똑같은 코드를 여러 번 작성 🔄
2. **수정의 악몽**: 내용을 바꾸려면 모든 줄을 다 수정 😰
3. **확장성 제로**: 횟수를 바꾸려면 줄을 추가하거나 삭제 📈

#### 💡 **반복문의 등장 - 반복의 마법**

**같은 기능을 반복문으로 작성하면:**

```python
# ✅ 반복문을 사용한 깔끔한 코드
for i in range(5):
    print("안녕하세요")

# 🎉 100번? 1000번? 숫자만 바꾸면 끝!
for i in range(100):
    print("안녕하세요")
```

**반복문의 놀라운 효과:**
- 5줄 → 2줄로 압축! 📉
- 횟수 변경? 숫자 하나만 수정! ⚡
- 가독성 완벽! 👁️

### 📌 핵심 개념 2: for문 - 정해진 횟수만큼 반복하기 (16분)

#### 🔄 **for문의 기본 구조**

**for문의 기본 문법:**
```python
for 변수 in range(횟수):
    실행할 코드
```

**가장 기본적인 예시:**
```python
# 1부터 5까지 출력하기
for i in range(1, 6):
    print(i)

# 결과:
# 1
# 2
# 3
# 4
# 5
```

#### 📏 **range() 함수 완전 정복**

**range()의 3가지 형태:**

**1. range(끝숫자) - 0부터 시작**
```python
for i in range(5):  # 0, 1, 2, 3, 4
    print(i)
```

**2. range(시작, 끝) - 시작 숫자부터**
```python
for i in range(3, 8):  # 3, 4, 5, 6, 7
    print(i)
```

**3. range(시작, 끝, 간격) - 간격 지정**
```python
for i in range(0, 10, 2):  # 0, 2, 4, 6, 8
    print(i)
```

#### 🎯 **실용적인 for문 활용 예시들**

**예시 1: 구구단 프로그램**
```python
# 사용자로부터 단 입력받기
dan = int(input("몇 단을 출력할까요? (2-9): "))

if 2 <= dan <= 9:
    print(f"\n=== {dan}단 ===")
    for i in range(1, 10):
        result = dan * i
        print(f"{dan} × {i} = {result:2d}")
else:
    print("2부터 9 사이의 숫자를 입력해주세요.")
```

**예시 2: 점수 입력 및 분석**
```python
# 학생 수 입력받기
student_count = int(input("학생 수를 입력하세요: "))

total_score = 0
print(f"\n{student_count}명의 점수를 입력해주세요:")

for i in range(student_count):
    score = int(input(f"{i+1}번째 학생 점수: "))
    total_score = total_score + score
    
    # 점수별 등급 출력
    if score >= 90:
        grade = "A"
    elif score >= 80:
        grade = "B"
    elif score >= 70:
        grade = "C"
    else:
        grade = "D"
    
    print(f"  → {score}점 ({grade}등급)")

# 평균 계산 및 출력
average = total_score / student_count
print(f"\n전체 평균: {average:.1f}점")
```

**예시 3: 패스워드 생성기**
```python
# 사용자로부터 길이 입력받기
length = int(input("패스워드 길이를 입력하세요: "))

import random

password = ""
characters = "0123456789ABCDEFabcdef"

print(f"\n{length}자리 패스워드 생성 중...")

for i in range(length):
    # 랜덤한 문자 선택
    random_char = random.choice(characters)
    password = password + random_char
    
    # 진행 상황 표시
    print(f"진행률: {i+1}/{length} - 현재: {password}")

print(f"\n완성된 패스워드: {password}")
```

### 📌 핵심 개념 3: while문 - 조건이 맞는 동안 계속 반복하기 (16분)

#### 🔄 **while문의 기본 구조**

**while문의 기본 문법:**
```python
while 조건:
    실행할 코드
    조건을 변경하는 코드  # 중요!
```

**간단한 예시:**
```python
# 1부터 5까지 출력하기 (while문 버전)
i = 1
while i <= 5:
    print(i)
    i = i + 1  # 조건 변경 필수!
```

#### ⚠️ **while문 주의사항 - 무한루프 방지**

```python
# ❌ 위험한 무한루프 (절대 실행하지 마세요!)
# i = 1
# while i <= 5:
#     print(i)
#     # i += 1 이 없어서 i가 계속 1!
#     # 프로그램이 영원히 끝나지 않음!

# ✅ 올바른 while문
i = 1
while i <= 5:
    print(i)
    i = i + 1  # 조건을 변경!
```

#### 🎯 **while문이 더 적합한 상황들**

**상황 1: 메뉴 기반 프로그램**
```python
print("=== 간단한 계산기 ===")

while True:
    print("\n1. 더하기")
    print("2. 빼기")
    print("3. 종료")
    
    choice = input("선택하세요 (1-3): ")
    
    if choice == "1":
        a = int(input("첫 번째 숫자: "))
        b = int(input("두 번째 숫자: "))
        print(f"결과: {a} + {b} = {a + b}")
    
    elif choice == "2":
        a = int(input("첫 번째 숫자: "))
        b = int(input("두 번째 숫자: "))
        print(f"결과: {a} - {b} = {a - b}")
    
    elif choice == "3":
        print("계산기를 종료합니다.")
        break
    
    else:
        print("잘못된 선택입니다.")
```

**상황 2: 숫자 맞추기 게임**
```python
import random

secret_number = random.randint(1, 10)
attempts = 0
max_attempts = 5

print("1부터 10 사이의 숫자를 맞춰보세요!")
print(f"최대 {max_attempts}번 시도할 수 있습니다.")

while attempts < max_attempts:
    attempts = attempts + 1
    guess = int(input(f"\n{attempts}번째 시도: "))
    
    if guess == secret_number:
        print(f"정답입니다! {attempts}번 만에 맞추셨네요!")
        break
    elif guess < secret_number:
        print("더 큰 숫자입니다!")
    else:
        print("더 작은 숫자입니다!")
    
    remaining = max_attempts - attempts
    if remaining > 0:
        print(f"남은 기회: {remaining}번")

if attempts >= max_attempts and guess != secret_number:
    print(f"아쉽네요! 정답은 {secret_number}였습니다.")
```

**상황 3: 목표 달성까지 반복**
```python
print("=== 용돈 모으기 게임 ===")

target_money = int(input("목표 금액을 입력하세요: "))
current_money = 0
day = 0

print(f"목표: {target_money}원")

while current_money < target_money:
    day = day + 1
    
    print(f"\n{day}일째")
    daily_earning = int(input("오늘 번 돈: "))
    current_money = current_money + daily_earning
    
    remaining = target_money - current_money
    
    if remaining > 0:
        print(f"현재 금액: {current_money}원")
        print(f"목표까지: {remaining}원 남음")
    else:
        print(f"축하합니다! {day}일 만에 목표 달성!")
        print(f"최종 금액: {current_money}원")
```

---

## ☕ 휴식 시간 (10분)

---

## 🎯 2부: break와 continue - 반복문 제어의 달인 (40분)

### 📌 핵심 개념 1: break문 - 반복문 즉시 종료 (15분)

#### 🛑 **break문의 역할**

**break문 = 반복문의 응급정지 버튼**

```python
# break 없는 반복
for i in range(1, 11):
    print(i)
# 1부터 10까지 모두 출력

# break 있는 반복
for i in range(1, 11):
    if i == 5:
        break  # 5에서 중단!
    print(i)
# 1, 2, 3, 4만 출력
```

#### 🎯 **break문 활용 예시들**

**예시 1: 리스트에서 특정 값 검색**
```python
# 학생 이름 리스트
students = ["김철수", "이영희", "박민수", "최지영", "정다은"]

search_name = input("찾을 학생 이름: ")
found = False

print("검색 중...")
for i in range(len(students)):
    print(f"{i+1}번째 확인: {students[i]}")
    
    if students[i] == search_name:
        print(f"✅ {search_name} 학생을 {i+1}번째에서 찾았습니다!")
        found = True
        break

if not found:
    print(f"❌ {search_name} 학생을 찾을 수 없습니다.")
```

**예시 2: 로그인 시스템**
```python
correct_password = "python123"
max_tries = 3

print("=== 로그인 시스템 ===")

for attempt in range(1, max_tries + 1):
    password = input(f"비밀번호를 입력하세요 ({attempt}/{max_tries}): ")
    
    if password == correct_password:
        print("✅ 로그인 성공!")
        print("환영합니다!")
        break
    else:
        remaining = max_tries - attempt
        if remaining > 0:
            print(f"❌ 틀렸습니다. {remaining}번 더 시도할 수 있습니다.")
        else:
            print("❌ 로그인 실패! 계정이 잠겼습니다.")
```

### 📌 핵심 개념 2: continue문 - 다음 반복으로 건너뛰기 (15분)

#### ⏭️ **continue문의 역할**

**continue문 = 현재 반복만 건너뛰고 다음 반복 계속**

```python
# continue 없는 반복
for i in range(1, 6):
    print(f"숫자: {i}")

# continue 있는 반복
for i in range(1, 6):
    if i == 3:
        continue  # 3은 건너뛰기
    print(f"숫자: {i}")
# 1, 2, 4, 5만 출력 (3은 건너뜀)
```

#### 🎯 **continue문 활용 예시들**

**예시 1: 조건부 데이터 처리**
```python
print("=== 시험 점수 분석 ===")

scores = [95, -1, 88, 150, 92, 78, 101, 85]  # 일부 잘못된 데이터 포함

valid_scores = []
print("점수 검증 중...")

for i in range(len(scores)):
    score = scores[i]
    print(f"{i+1}번째 점수: {score}")
    
    # 잘못된 점수는 건너뛰기
    if score < 0 or score > 100:
        print("  → 잘못된 점수입니다. 건너뜁니다.")
        continue
    
    # 유효한 점수만 처리
    valid_scores.append(score)
    
    if score >= 90:
        print("  → 우수한 점수입니다! ⭐")
    else:
        print("  → 유효한 점수로 저장되었습니다.")

print(f"\n유효한 점수들: {valid_scores}")
print(f"평균: {sum(valid_scores) / len(valid_scores):.1f}점")
```

**예시 2: 특정 조건만 처리하기**
```python
print("=== 짝수만 처리하는 프로그램 ===")

numbers = [1, 4, 7, 8, 12, 15, 20, 23, 24]

even_sum = 0
even_count = 0

for number in numbers:
    print(f"검사 중: {number}")
    
    # 홀수는 건너뛰기
    if number % 2 != 0:
        print(f"  → {number}는 홀수이므로 건너뜁니다.")
        continue
    
    # 짝수만 처리
    even_sum = even_sum + number
    even_count = even_count + 1
    print(f"  → {number}는 짝수입니다. 합계에 추가!")
    print(f"      현재 짝수 합계: {even_sum}")

print(f"\n최종 결과:")
print(f"짝수 개수: {even_count}개")
print(f"짝수 합계: {even_sum}")
print(f"짝수 평균: {even_sum / even_count:.1f}")
```

### 📌 핵심 개념 3: break와 continue 조합 활용 (10분)

#### 🎯 **복합적인 제어 흐름**

```python
print("1부터 100까지 숫자 처리")
print("- 10의 배수는 건너뛰기")
print("- 50에 도달하면 중단")

for i in range(1, 101):
    if i == 50:
        print("50에 도달! 중단합니다.")
        break
    
    if i % 10 == 0:
        print(f"{i}: 10의 배수 건너뜀")
        continue
    
    print(f"처리: {i}")
```

---

## ☕ 휴식 시간 (10분)

---

## 🎯 3부: 중첩 반복문과 고급 반복문 패턴 (40분)

### 📌 핵심 개념 1: 중첩 반복문 - 반복 안의 반복 (15분)

#### 🔄 **중첩 반복문의 개념**

**기본 중첩 반복문:**
```python
# 바깥쪽 반복문과 안쪽 반복문
for i in range(1, 4):  # 1, 2, 3
    print(f"바깥쪽: {i}")
    
    for j in range(1, 4):  # 1, 2, 3
        print(f"  안쪽: {j}")
    
    print()  # 빈 줄
```

#### 🎯 **중첩 반복문 활용 예시**

**예시 1: 전체 구구단 출력**
```python
# 사용자로부터 범위 입력받기
start_dan = int(input("시작 단 (2-9): "))
end_dan = int(input("끝 단 (2-9): "))

print(f"\n=== {start_dan}단부터 {end_dan}단까지 ===")

for dan in range(start_dan, end_dan + 1):  # 바깥쪽: 단 수
    print(f"\n[ {dan}단 ]")
    
    for num in range(1, 10):  # 안쪽: 곱할 수
        result = dan * num
        print(f"{dan} × {num} = {result:2d}")
    
    # 단이 끝날 때마다 구분선
    if dan < end_dan:
        print("-" * 15)
```

**예시 2: 성적표 만들기**
```python
# 학생 이름과 과목
students = ["김철수", "이영희", "박민수"]
subjects = ["국어", "영어", "수학"]

print("=== 성적 입력 ===")

# 성적을 저장할 2차원 리스트
grades = []

for i in range(len(students)):  # 각 학생에 대해
    student_name = students[i]
    print(f"\n{student_name} 학생의 성적:")
    
    student_grades = []
    for j in range(len(subjects)):  # 각 과목에 대해
        subject = subjects[j]
        score = int(input(f"  {subject} 점수: "))
        student_grades.append(score)
    
    grades.append(student_grades)

# 성적표 출력
print(f"\n{'='*40}")
print("성적표")
print(f"{'='*40}")
print(f"{'학생명':^8}", end="")
for subject in subjects:
    print(f"{subject:^6}", end="")
print(f"{'평균':^6}")

print("-" * 40)

for i in range(len(students)):
    print(f"{students[i]:^8}", end="")
    
    total = 0
    for j in range(len(subjects)):
        score = grades[i][j]
        print(f"{score:^6}", end="")
        total = total + score
    
    average = total / len(subjects)
    print(f"{average:^6.1f}")
```

**예시 3: 좌석 예약 시스템**
```python
# 영화관 좌석 (5행 8열)
rows = 5
cols = 8

# 좌석 상태 초기화 (False = 빈 좌석, True = 예약됨)
seats = []
for i in range(rows):
    row = []
    for j in range(cols):
        row.append(False)  # 모든 좌석을 빈 좌석으로 초기화
    seats.append(row)

print("=== 영화관 좌석 예약 시스템 ===")

while True:
    # 현재 좌석 상황 출력
    print(f"\n현재 좌석 상황:")
    print("    ", end="")
    for col in range(1, cols + 1):
        print(f"{col:2d}", end=" ")
    print()
    
    for row in range(rows):
        print(f"{row+1}행:", end=" ")
        for col in range(cols):
            if seats[row][col]:
                print(" X", end=" ")  # 예약된 좌석
            else:
                print(" O", end=" ")  # 빈 좌석
        print()
    
    # 사용자 입력
    print("\n1. 좌석 예약")
    print("2. 예약 취소") 
    print("3. 종료")
    
    choice = input("선택하세요: ")
    
    if choice == "1":
        row_num = int(input("행 번호 (1-5): ")) - 1
        col_num = int(input("열 번호 (1-8): ")) - 1
        
        if 0 <= row_num < rows and 0 <= col_num < cols:
            if not seats[row_num][col_num]:
                seats[row_num][col_num] = True
                print(f"✅ {row_num+1}행 {col_num+1}열 예약 완료!")
            else:
                print("❌ 이미 예약된 좌석입니다.")
        else:
            print("❌ 잘못된 좌석 번호입니다.")
    
    elif choice == "3":
        print("예약 시스템을 종료합니다.")
        break
```

### 📌 핵심 개념 2: 리스트와 반복문 (15분)

#### 📊 **리스트의 요소들을 하나씩 처리**

**기본 패턴:**
```python
# 리스트 생성
fruits = ["사과", "바나나", "오렌지"]

# 방법 1: 인덱스 사용
for i in range(len(fruits)):
    print(f"{i+1}번째: {fruits[i]}")

# 방법 2: 직접 접근 (더 좋음)
for fruit in fruits:
    print(f"과일: {fruit}")
```

#### 🎯 **리스트 처리 예시들**

**예시 1: 점수 처리하기**
```python
scores = [85, 92, 78, 96, 88]

# 모든 점수 출력
print("점수 목록:")
for score in scores:
    print(f"{score}점")

# 평균 계산
total = 0
for score in scores:
    total = total + score

average = total / len(scores)
print(f"평균: {average:.1f}점")
```

**예시 2: 조건에 맞는 값 찾기**
```python
numbers = [5, 12, 8, 20, 3, 15]

# 10보다 큰 수 찾기
print("10보다 큰 수들:")
for number in numbers:
    if number > 10:
        print(number)

# 짝수 개수 세기
even_count = 0
for number in numbers:
    if number % 2 == 0:
        even_count = even_count + 1

print(f"짝수 개수: {even_count}개")
```

### 📌 핵심 개념 3: 반복문 활용 패턴 (10분)

#### 🎯 **자주 사용되는 패턴들**

**패턴 1: 최대값 찾기**
```python
numbers = [23, 45, 12, 67, 34]

max_value = numbers[0]  # 첫 번째 값으로 시작

for number in numbers:
    if number > max_value:
        max_value = number

print(f"최대값: {max_value}")
```

**패턴 2: 조건 만족하는 첫 번째 값**
```python
numbers = [1, 3, 8, 5, 12, 7]

# 5보다 큰 첫 번째 수 찾기
for number in numbers:
    if number > 5:
        print(f"5보다 큰 첫 번째 수: {number}")
        break
```

**패턴 3: 그룹별 처리**
```python
numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]

odd_sum = 0   # 홀수 합
even_sum = 0  # 짝수 합

for number in numbers:
    if number % 2 == 0:
        even_sum = even_sum + number
    else:
        odd_sum = odd_sum + number

print(f"홀수 합: {odd_sum}")
print(f"짝수 합: {even_sum}")
```

---

## 🎯 실습 시간 (60분)

### 🎯 실습 과제 1: 숫자 맞추기 게임 (20분)

#### 📋 **과제 요구사항**

**알고리즘 말투로 표현:**
1. "1부터 10 사이의 비밀 숫자를 정한다"
2. "사용자로부터 숫자를 입력받는다"
3. "입력받은 숫자가 비밀 숫자와 같은지 확인한다"
4. "만약 같으면 '정답!'을 출력하고 게임을 끝낸다"
5. "만약 다르면 '틀렸습니다'를 출력하고 다시 입력받는다"
6. "최대 5번까지만 시도할 수 있게 한다"

**구체적 요구사항:**
- while문 또는 for문 사용
- break문으로 정답 시 게임 종료
- 시도 횟수 제한 (5번)
- 힌트 제공 (더 큰 수 / 더 작은 수)

### 🎯 실습 과제 2: 별 패턴 그리기 (20분)

#### 📋 **과제 요구사항**

**알고리즘 말투로 표현:**
1. "사용자로부터 패턴의 크기를 입력받는다"
2. "크기만큼 줄을 반복한다"
3. "각 줄에서 필요한 만큼 별을 출력한다"
4. "다음 패턴 중 2개 이상 구현한다:"
   - "직각삼각형: 1개, 2개, 3개... 순서로 별 증가"
   - "역삼각형: 5개, 4개, 3개... 순서로 별 감소"
   - "이등변삼각형: 가운데 정렬하여 1개, 3개, 5개..."

**구체적 요구사항:**
- 중첩 반복문 사용
- 사용자 입력으로 크기 결정
- 최소 2가지 패턴 구현
- 각 패턴을 구분하여 출력

### 🎯 실습 과제 3: 간단한 성적 처리 (20분)

#### 📋 **과제 요구사항**

**알고리즘 말투로 표현:**
1. "사용자로부터 학생 수를 입력받는다"
2. "학생 수만큼 반복하여 각 학생의 점수를 입력받는다"
3. "입력받은 점수들을 리스트에 저장한다"
4. "모든 점수의 합계와 평균을 계산한다"
5. "가장 높은 점수와 가장 낮은 점수를 찾는다"
6. "80점 이상인 학생 수를 센다"
7. "결과를 출력한다"

**구체적 요구사항:**
- for문으로 점수 입력받기
- 리스트에 점수 저장
- 반복문으로 최대값, 최소값 찾기
- 조건문과 반복문으로 우수학생 수 계산
- 결과를 보기 좋게 출력

---

## 📚 실습 과제 모범답안

### 🎯 과제 1 모범답안: 숫자 맞추기 게임

```python
import random

# 숫자 맞추기 게임
print("🎯 숫자 맞추기 게임")
print("1부터 10 사이의 숫자를 맞춰보세요!")

# 게임 설정
secret_number = random.randint(1, 10)
max_attempts = 5
score = 100  # 시작 점수

print(f"최대 {max_attempts}번 시도할 수 있습니다.")
print("틀릴 때마다 점수가 20점씩 차감됩니다.")

for attempt in range(1, max_attempts + 1):
    print(f"\n{attempt}번째 시도 (남은 기회: {max_attempts - attempt}번)")
    print(f"현재 점수: {score}점")
    
    guess = int(input("숫자를 입력하세요 (1-10): "))
    
    # 입력값 검증
    if guess < 1 or guess > 10:
        print("1부터 10 사이의 숫자를 입력해주세요!")
        continue
    
    if guess == secret_number:
        print("🎉 정답입니다!")
        print(f"최종 점수: {score}점")
        
        if attempt == 1:
            print("🏆 대박! 한 번에 맞추셨네요!")
        elif attempt <= 3:
            print("👍 훌륭합니다!")
        else:
            print("💪 잘했어요!")
        break
    
    else:
        score = score - 20  # 점수 차감
        
        if guess < secret_number:
            print("📈 더 큰 숫자입니다!")
        else:
            print("📉 더 작은 숫자입니다!")
        
        # 힌트 제공
        if attempt >= 3:
            if secret_number <= 3:
                print("💡 힌트: 1~3 사이의 숫자예요.")
            elif secret_number <= 7:
                print("💡 힌트: 4~7 사이의 숫자예요.")
            else:
                print("💡 힌트: 8~10 사이의 숫자예요.")

else:
    print(f"\n😭 아쉽네요! 정답은 {secret_number}였습니다.")
    print("다음에 다시 도전해보세요!")

print("게임 종료")
```

### 🎯 과제 2 모범답안: 별 패턴 그리기

```python
# 별 패턴 그리기
print("⭐ 별 패턴 그리기 프로그램")

# 사용자로부터 크기 입력받기
while True:
    size = int(input("패턴 크기를 입력하세요 (3-10): "))
    if 3 <= size <= 10:
        break
    else:
        print("3부터 10 사이의 숫자를 입력해주세요!")

print(f"\n크기 {size}의 다양한 패턴을 그립니다.")

# 패턴 1: 직각삼각형
print(f"\n1️⃣ 직각삼각형")
print("-" * 20)
for i in range(1, size + 1):
    for j in range(i):
        print("*", end="")
    print(f"  ← {i}개")

# 패턴 2: 역삼각형
print(f"\n2️⃣ 역삼각형")
print("-" * 20)
for i in range(size, 0, -1):
    for j in range(i):
        print("*", end="")
    print(f"  ← {i}개")

# 패턴 3: 이등변삼각형
print(f"\n3️⃣ 이등변삼각형")
print("-" * 20)
for i in range(1, size + 1):
    # 왼쪽 공백
    for j in range(size - i):
        print(" ", end="")
    
    # 별 출력
    for k in range(i):
        print("*", end="")
    
    print(f"  ← {i}개 별, {size-i}개 공백")

# 패턴 4: 속이 빈 사각형
print(f"\n4️⃣ 속이 빈 사각형")
print("-" * 20)
for i in range(size):
    for j in range(size):
        # 테두리만 별, 내부는 공백
        if i == 0 or i == size-1 or j == 0 or j == size-1:
            print("*", end="")
        else:
            print(" ", end="")
    print()

print("\n⭐ 모든 패턴 그리기 완료!")

# 통계 정보
total_stars = 0
# 직각삼각형: 1+2+3+...+size
for i in range(1, size + 1):
    total_stars = total_stars + i

print(f"📊 통계: 직각삼각형에는 총 {total_stars}개의 별이 사용되었습니다.")
```

### 🎯 과제 3 모범답안: 간단한 성적 처리

```python
# 성적 처리 프로그램
print("📊 학급 성적 관리 프로그램")
print("=" * 30)

# 학생 수 입력받기
while True:
    student_count = int(input("학생 수를 입력하세요 (1-30): "))
    if 1 <= student_count <= 30:
        break
    else:
        print("1명부터 30명 사이로 입력해주세요!")

# 점수들을 저장할 리스트
scores = []
student_names = []

# 각 학생의 정보 입력받기
print(f"\n{student_count}명의 정보를 입력해주세요:")
for i in range(student_count):
    print(f"\n{i+1}번째 학생:")
    
    # 이름 입력
    name = input("  이름: ")
    student_names.append(name)
    
    # 점수 입력 (유효성 검사 포함)
    while True:
        score = int(input("  점수 (0-100): "))
        if 0 <= score <= 100:
            scores.append(score)
            break
        else:
            print("  0부터 100 사이의 점수를 입력해주세요!")
    
    # 즉시 등급 표시
    if score >= 90:
        grade = "A"
    elif score >= 80:
        grade = "B"
    elif score >= 70:
        grade = "C"
    elif score >= 60:
        grade = "D"
    else:
        grade = "F"
    
    print(f"  → {name}: {score}점 ({grade}등급)")

# 통계 계산
total = 0
for score in scores:
    total = total + score
average = total / student_count

# 최고점과 최저점 찾기
highest = scores[0]
lowest = scores[0]
highest_student = ""
lowest_student = ""

for i in range(len(scores)):
    if scores[i] > highest:
        highest = scores[i]
        highest_student = student_names[i]
    
    if scores[i] < lowest:
        lowest = scores[i]
        lowest_student = student_names[i]

# 등급별 통계
grade_count = {"A": 0, "B": 0, "C": 0, "D": 0, "F": 0}

for score in scores:
    if score >= 90:
        grade_count["A"] = grade_count["A"] + 1
    elif score >= 80:
        grade_count["B"] = grade_count["B"] + 1
    elif score >= 70:
        grade_count["C"] = grade_count["C"] + 1
    elif score >= 60:
        grade_count["D"] = grade_count["D"] + 1
    else:
        grade_count["F"] = grade_count["F"] + 1

# 결과 출력
print(f"\n{'='*50}")
print(f"📊 {student_count}명 학급 성적 분석 결과")
print(f"{'='*50}")

# 기본 통계
print(f"📈 기본 통계:")
print(f"  총점: {total}점")
print(f"  평균: {average:.1f}점")
print(f"  최고점: {highest}점 ({highest_student})")
print(f"  최저점: {lowest}점 ({lowest_student})")

# 등급별 분포
print(f"\n🏆 등급별 분포:")
for grade in ["A", "B", "C", "D", "F"]:
    count = grade_count[grade]
    percentage = (count / student_count) * 100
    print(f"  {grade}등급: {count}명 ({percentage:.1f}%)")

# 우수학생 (80점 이상)
print(f"\n⭐ 우수학생 명단 (80점 이상):")
excellent_count = 0
for i in range(len(scores)):
    if scores[i] >= 80:
        excellent_count = excellent_count + 1
        print(f"  {student_names[i]}: {scores[i]}점")

if excellent_count == 0:
    print("  없음")

print(f"\n총 우수학생: {excellent_count}명 ({excellent_count/student_count*100:.1f}%)")

# 학급 평가
if average >= 85:
    evaluation = "매우 우수한 학급입니다! 🏆"
elif average >= 75:
    evaluation = "좋은 성적의 학급이에요! 👍"
elif average >= 65:
    evaluation = "평균적인 학급입니다. 💪"
else:
    evaluation = "더 열심히 공부해야겠어요! 📚"

print(f"\n🎯 학급 평가: {evaluation}")
```

---

## 📚 오늘 배운 내용 정리

### ✅ 핵심 포인트

1. **반복문의 필요성**:
   - 코드 중복 제거와 효율성 증대
   - 같은 작업을 여러 번 할 때 필수

2. **for문 활용**:
   - `range()` 함수로 횟수 지정
   - 리스트의 요소들을 하나씩 처리
   - 정해진 횟수만큼 반복할 때 사용

3. **while문 활용**:
   - 조건이 참인 동안 계속 반복
   - 사용자 입력 처리에 유용
   - 언제 끝날지 모를 때 사용

4. **break와 continue**:
   - break: 반복문 즉시 종료
   - continue: 현재 반복만 건너뛰고 계속
   - 반복문의 흐름을 정교하게 제어

5. **중첩 반복문**:
   - 반복문 안에 또 다른 반복문
   - 2차원 구조 처리에 필수
   - 패턴 그리기, 표 만들기 등에 활용

### 🏠 다음 주까지 해볼 과제

1. **반복문 기초 연습**:
   - 오늘 배운 예제들을 직접 실행해보기
   - 숫자를 바꿔가며 다양한 결과 확인하기

2. **패턴 그리기 도전**:
   - 다른 모양의 별 패턴 만들어보기
   - 숫자나 다른 문자로 패턴 그리기

3. **간단한 게임 만들기**:
   - 숫자 맞추기 게임에 기능 추가
   - 가위바위보 게임 만들어보기

4. **리스트 처리 연습**:
   - 다양한 데이터로 최대값, 최소값 찾기
   - 조건에 맞는 데이터 개수 세기

### 🔮 다음 주 예고

**6주차: 자료구조와 객체 개념 소개**
- 리스트, 딕셔너리, 세트의 특징과 활용
- 각 자료구조를 언제 사용할지 판단하기
- 객체지향 프로그래밍의 기초 개념
- 메서드와 속성의 개념

### 💡 마지막 정리

**지금까지의 성장 과정:**
```
1주차: "프로그래밍이 뭔지 알았다!"
2주차: "어디서든 코딩할 수 있게 되었다!"
3주차: "변수로 복잡한 문제를 해결할 수 있다!"
4주차: "조건문으로 똑똑한 프로그램을 만들 수 있다!"
5주차: "반복문으로 효율적인 프로그램을 만들 수 있다!"
```

**오늘 여러분이 할 수 있게 된 것들:**
- 🔄 같은 작업을 자동으로 여러 번 처리하기
- 🎮 사용자와 계속 상호작용하는 프로그램 만들기
- 🎨 복잡한 패턴을 코드로 그리기
- 📊 여러 데이터를 한번에 처리하기
- 🎯 조건에 따라 반복을 제어하기

**프로그래밍의 3대 구조 완성:**
오늘로써 프로그래밍의 핵심인 **순차-선택-반복** 구조를 모두 마스터했습니다! 이제 어떤 문제든 이 3가지의 조합으로 해결할 수 있어요.

**마지막 격려:**
반복문을 배우면서 진짜 프로그래밍의 힘을 느꼈을 거예요. 이제 컴퓨터가 지치지 않고 수천 번, 수만 번 작업을 해주는 마법을 부릴 수 있습니다! 🌟

다음 주에는 데이터를 더 체계적으로 관리하는 방법을 배워봅시다! 💪

---

**🎯 5주차 학습 완료! 수고하셨습니다! 🎉**