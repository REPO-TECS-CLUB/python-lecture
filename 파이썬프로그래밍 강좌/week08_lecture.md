# 8주차: 객체 지향 프로그래밍과 코딩 규칙
**총 강의시간: 3시간 20분 (200분)**
- 강의: 120분 (3부로 구성)
- 휴식: 20분 (10분씩 2회)
- 실습: 60분

---

## 🎯 1부: 추상화 - 실세계를 컴퓨터 세계로 옮기는 마법 (40분)

### 📌 핵심 개념 1: 지금까지의 여정과 새로운 도전 (8분)

#### 🔄 **우리가 정복한 프로그래밍의 세계**

**1-7주차 성장 기록:**
```
1주차: "프로그래밍이 뭔지 알았다!" (기본 구조) ✅
2주차: "어디서든 코딩할 수 있게 되었다!" (개발환경) ✅
3주차: "변수로 복잡한 문제를 해결할 수 있다!" (자료형) ✅
4주차: "조건문으로 똑똑한 프로그램을 만들 수 있다!" (선택구조) ✅
5주차: "반복문으로 효율적인 프로그램을 만들 수 있다!" (반복구조) ✅
6주차: "자료구조로 체계적인 데이터 관리를 할 수 있다!" (컬렉션) ✅
7주차: "함수로 재사용 가능한 코드를 만들 수 있다!" (모듈화) ✅
```

**오늘 해결할 문제**: 
복잡한 실세계의 "사물"과 "개념"들을 어떻게 컴퓨터 프로그램으로 표현할 수 있을까?

#### 🌍 **객체지향의 4대 핵심 요소**

**1. 추상화 (Abstraction)** - 🏗️ **가장 중요한 개념!**
- 실세계의 복잡한 사물에서 프로그램에 필요한 핵심만 뽑아내기
- "무엇을 표현할 것인가?"의 문제

**2. 정보은닉 (Information Hiding)** - 🔒 **객체 운영 요소**
- 객체의 내부 구현을 숨기고 필요한 기능만 공개하기
- "어떻게 안전하게 운영할 것인가?"의 문제

**3. 상속성 (Inheritance)** - 👨‍👦 **객체 운영 요소**
- 기존 객체의 특성을 물려받아 새로운 객체 만들기
- "어떻게 효율적으로 확장할 것인가?"의 문제

**4. 다형성 (Polymorphism)** - 🎭 **객체 운영 요소**
- 같은 명령으로 다른 객체들이 각자의 방식으로 동작하기
- "어떻게 유연하게 처리할 것인가?"의 문제

### 📌 핵심 개념 2: 추상화 - 실세계에서 본질만 뽑아내기 (20분)

#### 🔍 **추상화란 무엇인가?**

**추상화의 정의:**
복잡한 실세계의 사물에서 프로그램의 목적에 맞는 **핵심 특성만 선별**하여 컴퓨터가 이해할 수 있는 형태로 단순화하는 과정

**일상생활의 추상화 예시:**
```
🚗 실제 자동차:
   - 수만 개의 부품, 복잡한 엔진, 전자시스템, 배기가스, 소음...
   
🎯 내비게이션에서의 자동차 추상화:
   - 위치(GPS 좌표), 속도, 방향
   - 나머지는 모두 무시!
   
🎯 주차장 관리에서의 자동차 추상화:
   - 번호판, 입차시간, 차량크기
   - 속도나 연비는 관심 없음!
   
🎯 정비소에서의 자동차 추상화:
   - 엔진상태, 주행거리, 정비이력
   - 위치나 속도는 관심 없음!
```

**핵심 깨달음**: 같은 실세계 사물이라도 **목적에 따라 다르게 추상화**된다!

#### 🎯 **추상화 실습: 학생을 어떻게 표현할까?**

**알고리즘 말투로 추상화 과정 표현:**
1. "실세계의 학생을 관찰한다"
2. "프로그램의 목적을 명확히 한다"
3. "목적에 필요한 특성들만 선별한다"
4. "불필요한 정보는 과감히 제거한다"
5. "컴퓨터가 처리할 수 있는 형태로 변환한다"

**상황별 학생 추상화:**

```python
# 🎯 상황 1: 출석 관리 시스템
print("=== 출석 관리를 위한 학생 추상화 ===")

class StudentForAttendance:
    """출석 관리를 위한 학생 추상화"""
    
    def __init__(self, student_id, name):
        # 핵심 정보만 선별
        self.student_id = student_id    # 학번 (식별용)
        self.name = name                # 이름 (확인용)
        self.attendance_record = []     # 출석 기록
        
        # ❌ 불필요한 정보들은 제거
        # self.height = height          # 출석과 무관
        # self.favorite_color = color   # 출석과 무관
        # self.shoe_size = size         # 출석과 무관
    
    def mark_attendance(self, date, status):
        """출석 체크 - 목적에 맞는 핵심 기능"""
        self.attendance_record.append({
            'date': date, 
            'status': status  # '출석', '지각', '결석'
        })
        print(f"📅 {self.name} 학생 {date} {status} 처리 완료")
    
    def get_attendance_rate(self):
        """출석률 계산 - 목적에 맞는 핵심 기능"""
        if not self.attendance_record:
            return 0
        
        present_count = sum(1 for record in self.attendance_record 
                          if record['status'] in ['출석', '지각'])
        return (present_count / len(self.attendance_record)) * 100

# 사용자 입력으로 학생 생성
student_id = input("학번을 입력하세요: ")
student_name = input("학생 이름을 입력하세요: ")

student = StudentForAttendance(student_id, student_name)
print(f"✅ 출석관리용 학생 객체 생성: {student.name} ({student.student_id})")

# 출석 처리 예시
student.mark_attendance("2024-03-01", "출석")
student.mark_attendance("2024-03-02", "지각")
student.mark_attendance("2024-03-03", "출석")

print(f"📊 {student.name}의 출석률: {student.get_attendance_rate():.1f}%")
```

```python
# 🎯 상황 2: 성적 관리 시스템
print("\n=== 성적 관리를 위한 학생 추상화 ===")

class StudentForGrades:
    """성적 관리를 위한 학생 추상화"""
    
    def __init__(self, student_id, name, grade_level):
        # 성적 관리에 필요한 핵심 정보만
        self.student_id = student_id
        self.name = name
        self.grade_level = grade_level    # 학년 (성적 기준이 다름)
        self.subjects = {}                # 과목별 성적
        
        # ❌ 출석 정보는 여기서 불필요
        # self.attendance_record = []
    
    def add_subject_score(self, subject, score):
        """과목 성적 추가"""
        self.subjects[subject] = score
        print(f"📚 {self.name} - {subject}: {score}점 입력 완료")
    
    def calculate_average(self):
        """평균 계산 - 성적 관리의 핵심 기능"""
        if not self.subjects:
            return 0
        return sum(self.subjects.values()) / len(self.subjects)
    
    def get_grade_level_standard(self):
        """학년별 기준 - 추상화의 차별점"""
        standards = {
            1: {"우수": 85, "보통": 70},
            2: {"우수": 87, "보통": 72},
            3: {"우수": 90, "보통": 75}
        }
        return standards.get(self.grade_level, {"우수": 85, "보통": 70})

# 사용자 입력으로 성적 관리용 학생 생성
grade_level = int(input("\n학년을 입력하세요 (1-3): "))
grade_student = StudentForGrades(student_id, student_name, grade_level)

# 과목 성적 입력
subjects = ["국어", "영어", "수학"]
for subject in subjects:
    score = int(input(f"{subject} 점수를 입력하세요: "))
    grade_student.add_subject_score(subject, score)

average = grade_student.calculate_average()
print(f"📊 {grade_student.name}의 평균: {average:.1f}점")
```

#### 🏗️ **추상화의 핵심 원칙**

**1. 목적 중심의 선별**
```python
# ✅ 좋은 추상화: 목적이 명확
class BankAccount:  # 은행 계좌 관리가 목적
    def __init__(self, account_number, owner_name, balance):
        self.account_number = account_number  # 계좌 식별
        self.owner_name = owner_name          # 소유자 확인
        self.balance = balance                # 잔액 관리
        
        # ❌ 은행 업무와 무관한 정보들 제외
        # self.owner_height = height
        # self.favorite_food = food

# ❌ 나쁜 추상화: 목적이 불분명
class Person:  # 사람의 모든 것을 다 담으려 함
    def __init__(self, name, age, height, weight, job, salary, hobby, ...):
        # 너무 많은 정보 → 복잡성 증가
        pass
```

**2. 적절한 수준의 단순화**
```python
# ✅ 적절한 추상화
class Car:
    def __init__(self, brand, model, speed):
        self.brand = brand
        self.model = model
        self.speed = speed
    
    def accelerate(self):
        self.speed += 10
    
    def brake(self):
        self.speed = max(0, self.speed - 10)

# ❌ 과도한 단순화
class Car:
    def move(self):  # 너무 단순 → 실용성 부족
        print("이동")

# ❌ 과도한 복잡화
class Car:
    def __init__(self, engine_rpm, fuel_injection_rate, ...):  # 너무 복잡
        # 수백 개의 변수와 메서드
        pass
```

### 📌 핵심 개념 3: 사용자 입력을 통한 동적 추상화 (12분)

#### 🎮 **실시간 추상화 실습: 나만의 애완동물 만들기**

**알고리즘 말투로 요구사항 표현:**
1. "애완동물 관리가 목적임을 명확히 한다"
2. "사용자로부터 애완동물 정보를 입력받는다"
3. "애완동물의 핵심 특성만 추상화한다"
4. "애완동물 관리에 필요한 기능만 구현한다"

**코드로 구현:**

```python
class Pet:
    """애완동물 추상화 - 애완동물 관리를 위한 핵심 특성만 선별"""
    
    def __init__(self, name, species, age, happiness_level=50):
        """
        애완동물 객체 생성
        
        추상화 기준: 애완동물 관리에 꼭 필요한 정보만
        """
        # 핵심 식별 정보
        self.name = name                    # 이름 (호출용)
        self.species = species              # 종류 (관리 방법이 다름)
        self.age = age                      # 나이 (관리 기준)
        
        # 상태 관리 정보
        self.happiness_level = happiness_level  # 행복도 (0-100)
        self.hunger_level = 30                  # 배고픔 (0-100)
        self.energy_level = 70                  # 에너지 (0-100)
        
        # ❌ 애완동물 관리와 무관한 정보는 제외
        # self.dna_sequence = ...           # 너무 복잡
        # self.exact_weight_in_grams = ...  # 너무 세밀
        # self.owner_bank_account = ...     # 관련성 없음
        
        print(f"🐾 {species} '{name}'이(가) 우리 가족이 되었습니다!")
        self.show_status()
    
    def feed(self):
        """먹이 주기 - 애완동물 관리의 핵심 기능"""
        if self.hunger_level <= 20:
            print(f"🍽️ {self.name}은(는) 배가 부르지 않아요!")
            return
        
        old_hunger = self.hunger_level
        self.hunger_level = max(0, self.hunger_level - 30)
        self.happiness_level = min(100, self.happiness_level + 10)
        
        print(f"🍖 {self.name}에게 맛있는 먹이를 주었습니다!")
        print(f"   배고픔: {old_hunger} → {self.hunger_level}")
        print(f"   행복도: {self.happiness_level}")
    
    def play(self):
        """놀아주기 - 애완동물 관리의 핵심 기능"""
        if self.energy_level <= 20:
            print(f"😴 {self.name}은(는) 너무 피곤해해요!")
            return
        
        old_happiness = self.happiness_level
        old_energy = self.energy_level
        
        self.happiness_level = min(100, self.happiness_level + 20)
        self.energy_level = max(0, self.energy_level - 15)
        self.hunger_level = min(100, self.hunger_level + 10)
        
        species_play = {
            "강아지": "공놀이를 했습니다! 🎾",
            "고양이": "실뭉치로 놀았습니다! 🧶", 
            "토끼": "점프 놀이를 했습니다! 🐰",
            "물고기": "수족관을 헤엄쳤습니다! 🐠"
        }
        
        play_message = species_play.get(self.species, "함께 놀았습니다! 🎮")
        print(f"🎉 {self.name}과(와) {play_message}")
        print(f"   행복도: {old_happiness} → {self.happiness_level}")
        print(f"   에너지: {old_energy} → {self.energy_level}")
    
    def rest(self):
        """휴식하기 - 애완동물 관리의 핵심 기능"""
        old_energy = self.energy_level
        self.energy_level = min(100, self.energy_level + 25)
        
        species_rest = {
            "강아지": "쿨쿨 잠을 잡니다 🐕‍🦺",
            "고양이": "햇볕에서 낮잠을 잡니다 😸",
            "토끼": "조용한 곳에서 쉽니다 🐰",
            "물고기": "수초 사이에서 쉽니다 🐠"
        }
        
        rest_message = species_rest.get(self.species, "편안히 쉽니다 😌")
        print(f"💤 {self.name}이(가) {rest_message}")
        print(f"   에너지: {old_energy} → {self.energy_level}")
    
    def show_status(self):
        """상태 확인 - 현재 추상화된 정보 표시"""
        print(f"\n🐾 === {self.name} ({self.species}) 상태 ===")
        print(f"   나이: {self.age}살")
        
        # 상태를 시각적으로 표현
        happiness_bar = "💚" * (self.happiness_level // 20) + "🤍" * (5 - self.happiness_level // 20)
        hunger_bar = "🍖" * (self.hunger_level // 20) + "⚪" * (5 - self.hunger_level // 20)
        energy_bar = "⚡" * (self.energy_level // 20) + "⚪" * (5 - self.energy_level // 20)
        
        print(f"   행복도: {happiness_bar} ({self.happiness_level}/100)")
        print(f"   배고픔: {hunger_bar} ({self.hunger_level}/100)")
        print(f"   에너지: {energy_bar} ({self.energy_level}/100)")
        
        # 종합 상태 평가
        avg_status = (self.happiness_level + (100 - self.hunger_level) + self.energy_level) / 3
        if avg_status >= 80:
            print(f"   상태: 매우 건강해요! 😊")
        elif avg_status >= 60:
            print(f"   상태: 괜찮아요! 🙂")
        elif avg_status >= 40:
            print(f"   상태: 관심이 필요해요 😐")
        else:
            print(f"   상태: 많이 돌봐주세요! 😢")
    
    def get_care_advice(self):
        """돌봄 조언 - 추상화된 정보를 바탕으로 한 지능적 판단"""
        advice = []
        
        if self.hunger_level > 70:
            advice.append("🍖 배가 많이 고파요! 먹이를 주세요.")
        
        if self.energy_level < 30:
            advice.append("💤 많이 피곤해해요! 쉬게 해주세요.")
            
        if self.happiness_level < 40:
            advice.append("🎮 심심해해요! 놀아주세요.")
        
        if not advice:
            advice.append("😊 지금 상태가 좋아요!")
        
        return advice

def create_pet_from_input():
    """사용자 입력을 통한 동적 추상화"""
    print("\n=== 새로운 애완동물 입양하기 ===")
    
    name = input("애완동물 이름: ")
    
    print("키울 수 있는 애완동물:")
    print("1. 강아지  2. 고양이  3. 토끼  4. 물고기")
    species_choice = input("선택 (1-4): ")
    
    species_map = {"1": "강아지", "2": "고양이", "3": "토끼", "4": "물고기"}
    species = species_map.get(species_choice, "강아지")
    
    try:
        age = int(input("나이 (살): "))
    except ValueError:
        age = 1
        print("잘못된 입력입니다. 1살로 설정합니다.")
    
    return Pet(name, species, age)

def pet_care_simulator():
    """애완동물 돌봄 시뮬레이터"""
    print("🐾 애완동물 돌봄 시뮬레이터에 오신 것을 환영합니다!")
    
    pet = create_pet_from_input()
    
    while True:
        print(f"\n{'='*50}")
        pet.show_status()
        
        advice = pet.get_care_advice()
        print(f"\n💡 돌봄 조언:")
        for tip in advice:
            print(f"   {tip}")
        
        print(f"\n📋 할 수 있는 일:")
        print("1. 먹이 주기")
        print("2. 놀아주기")
        print("3. 재우기")
        print("4. 상태 확인")
        print("5. 시뮬레이터 종료")
        
        choice = input("\n원하는 행동을 선택하세요 (1-5): ")
        
        if choice == "1":
            pet.feed()
        elif choice == "2":
            pet.play()
        elif choice == "3":
            pet.rest()
        elif choice == "4":
            pet.show_status()
        elif choice == "5":
            print(f"\n👋 {pet.name}와의 즐거운 시간이었습니다!")
            print("💝 애완동물과 함께한 추억은 평생 남을 거예요!")
            break
        else:
            print("❌ 잘못된 선택입니다. 1-5 중에서 선택해주세요.")

# 실행
if __name__ == "__main__":
    pet_care_simulator()
```

---

## ☕ 휴식 시간 (10분)

---

## 🎯 2부: 정보은닉과 캡슐화 - 객체를 안전하게 운영하는 방법 (40분)

### 📌 핵심 개념 1: 정보은닉이 왜 필요한가? (15분)

#### 🔒 **정보은닉의 개념**

**정보은닉 (Information Hiding):**
객체의 내부 구현 세부사항을 외부에서 직접 접근하지 못하도록 숨기고, 안전한 방법(메서드)을 통해서만 접근할 수 있게 하는 것

**일상생활의 정보은닉 예시:**
```
🏧 ATM 기계:
   ✅ 사용자가 할 수 있는 것:
      - 카드 삽입
      - 비밀번호 입력  
      - 출금/입금 버튼 누르기
   
   ❌ 사용자가 할 수 없는 것:
      - 내부 금고 직접 열기
      - 소프트웨어 코드 수정
      - 네트워크 설정 변경
   
   💡 이유: 보안과 안전성을 위해!
```

#### 🚨 **정보은닉 없이 프로그래밍하면 무슨 일이?**

**문제 상황 예시:**

```python
# ❌ 정보은닉이 없는 위험한 클래스
class DangerousBankAccount:
    def __init__(self, owner, balance):
        self.owner = owner
        self.balance = balance  # 외부에서 직접 접근 가능 - 위험!
        self.account_number = "123-456-789"
    
    def withdraw(self, amount):
        if amount <= self.balance:
            self.balance -= amount
            return True
        return False

# 사용자 입력으로 계좌 생성
owner_name = input("계좌 소유자 이름: ")
initial_balance = int(input("초기 잔액: "))

account = DangerousBankAccount(owner_name, initial_balance)
print(f"계좌 생성: {account.owner}, 잔액: {account.balance:,}원")

# 😱 위험한 상황들 시연
print("\n=== 위험한 상황들 ===")

# 위험 1: 잔액을 직접 수정
print("🚨 위험 1: 누군가 잔액을 직접 조작!")
account.balance = 999999999  # 직접 접근으로 잔액 조작!
print(f"조작 후 잔액: {account.balance:,}원")

# 위험 2: 음수 잔액 만들기
print("\n🚨 위험 2: 잔액을 음수로 만들기!")
account.balance = -50000
print(f"음수 잔액: {account.balance:,}원")

# 위험 3: 계좌번호 변경
print("\n🚨 위험 3: 다른 사람의 계좌번호로 변경!")
account.account_number = "999-999-999"  # 다른 사람 계좌로 변경
print(f"변조된 계좌번호: {account.account_number}")

print("\n💀 이런 식으로는 은행 시스템을 만들 수 없어요!")
```

### 📌 핵심 개념 2: 파이썬에서의 정보은닉 구현 (15분)

#### 🔐 **접근 제어 수준**

**1. Public (공개) - 밑줄 없음**
```python
class Example:
    def __init__(self):
        self.public_var = "누구나 접근 가능"
    
    def public_method(self):
        return "누구나 호출 가능"
```

**2. Protected (보호됨) - 밑줄 하나 (_)**
```python
class Example:
    def __init__(self):
        self._protected_var = "내부 사용 권장"
    
    def _protected_method(self):
        return "내부에서 사용하는 메서드"
```

**3. Private (비공개) - 밑줄 두 개 (__)**
```python
class Example:
    def __init__(self):
        self.__private_var = "외부 접근 불가"
    
    def __private_method(self):
        return "완전히 숨겨진 메서드"
```

#### 🏦 **안전한 은행 계좌 시스템 구현**

**알고리즘 말투로 요구사항 표현:**
1. "계좌의 중요한 정보를 외부에서 직접 수정할 수 없게 한다"
2. "안전한 메서드를 통해서만 거래가 가능하게 한다"
3. "사용자 입력을 검증하여 잘못된 거래를 방지한다"
4. "거래 내역을 기록하되 외부에서 조작할 수 없게 한다"

**코드로 구현:**

```python
class SecureBankAccount:
    """정보은닉을 적용한 안전한 은행 계좌"""
    
    def __init__(self, owner, initial_balance, account_number):
        # Public 정보 (외부에서 읽기만 가능하도록 설계)
        self.owner = owner
        
        # Private 정보 (외부 접근 완전 차단)
        self.__balance = initial_balance        # 잔액
        self.__account_number = account_number  # 계좌번호
        self.__pin = "1234"                     # 비밀번호
        self.__transaction_history = []         # 거래내역
        
        # Protected 정보 (내부 사용)
        self._daily_limit = 1000000            # 일일 한도
        self._transaction_count = 0            # 일일 거래 횟수
        
        print(f"✅ {owner}님의 계좌가 안전하게 생성되었습니다.")
        self.__add_transaction("계좌개설", initial_balance)
    
    def get_balance(self, pin):
        """잔액 조회 - 비밀번호 확인 후에만 가능"""
        if not self.__verify_pin(pin):
            print("❌ 비밀번호가 틀렸습니다.")
            return None
        
        print(f"💰 현재 잔액: {self.__balance:,}원")
        return self.__balance
    
    def deposit(self, amount, pin):
        """입금 - 안전한 메서드를 통해서만 가능"""
        if not self.__verify_pin(pin):
            print("❌ 비밀번호가 틀렸습니다.")
            return False
        
        if not self.__validate_amount(amount):
            return False
        
        old_balance = self.__balance
        self.__balance += amount
        self.__add_transaction("입금", amount)
        
        print(f"💰 입금 완료: {amount:,}원")
        print(f"   잔액: {old_balance:,}원 → {self.__balance:,}원")
        return True
    
    def withdraw(self, amount, pin):
        """출금 - 다양한 안전 검사 후 실행"""
        if not self.__verify_pin(pin):
            print("❌ 비밀번호가 틀렸습니다.")
            return False
        
        if not self.__validate_amount(amount):
            return False
        
        # 잔액 확인
        if amount > self.__balance:
            print(f"❌ 잔액 부족: 요청 {amount:,}원, 현재 {self.__balance:,}원")
            return False
        
        # 일일 한도 확인
        if amount > self._daily_limit:
            print(f"❌ 일일 출금 한도 초과: 한도 {self._daily_limit:,}원")
            return False
        
        # 안전하게 출금 실행
        old_balance = self.__balance
        self.__balance -= amount
        self._transaction_count += 1
        self.__add_transaction("출금", -amount)
        
        print(f"💸 출금 완료: {amount:,}원")
        print(f"   잔액: {old_balance:,}원 → {self.__balance:,}원")
        return True
    
    def transfer(self, target_account, amount, pin):
        """계좌이체"""
        if not self.__verify_pin(pin):
            print("❌ 비밀번호가 틀렸습니다.")
            return False
        
        # 출금과 동일한 검증
        if self.withdraw(amount, pin):
            print(f"💸 {target_account}로 {amount:,}원 이체 완료")
            return True
        return False
    
    def get_transaction_history(self, pin):
        """거래내역 조회 - 복사본 반환으로 원본 보호"""
        if not self.__verify_pin(pin):
            print("❌ 비밀번호가 틀렸습니다.")
            return None
        
        print(f"\n💳 {self.owner}님의 거래내역:")
        print("-" * 40)
        for i, transaction in enumerate(self.__transaction_history[-10:], 1):
            print(f"{i:2d}. {transaction}")
        
        return self.__transaction_history.copy()  # 복사본 반환
    
    def change_pin(self, old_pin, new_pin):
        """비밀번호 변경"""
        if not self.__verify_pin(old_pin):
            print("❌ 현재 비밀번호가 틀렸습니다.")
            return False
        
        if len(new_pin) != 4 or not new_pin.isdigit():
            print("❌ 새 비밀번호는 4자리 숫자여야 합니다.")
            return False
        
        self.__pin = new_pin
        self.__add_transaction("비밀번호 변경", 0)
        print("✅ 비밀번호가 안전하게 변경되었습니다.")
        return True
    
    # Private 메서드들 (외부에서 접근 불가)
    def __verify_pin(self, pin):
        """비밀번호 확인 - 보안 핵심 기능"""
        return pin == self.__pin
    
    def __validate_amount(self, amount):
        """금액 유효성 검사"""
        if not isinstance(amount, (int, float)):
            print("❌ 금액은 숫자여야 합니다.")
            return False
        
        if amount <= 0:
            print("❌ 금액은 0보다 커야 합니다.")
            return False
        
        if amount > 10000000:  # 1천만원 제한
            print("❌ 한 번에 처리할 수 있는 금액을 초과했습니다.")
            return False
        
        return True
    
    def __add_transaction(self, transaction_type, amount):
        """거래내역 추가 - 내부에서만 사용"""
        from datetime import datetime
        timestamp = datetime.now().strftime("%Y-%m-%d %H:%M:%S")
        
        if amount >= 0:
            record = f"{timestamp} | {transaction_type} | +{amount:,}원 | 잔액: {self.__balance:,}원"
        else:
            record = f"{timestamp} | {transaction_type} | {amount:,}원 | 잔액: {self.__balance:,}원"
        
        self.__transaction_history.append(record)
    
    def get_account_info(self):
        """계좌 기본 정보 (민감하지 않은 정보만)"""
        return {
            'owner': self.owner,
            'account_exists': True,
            'transaction_count': len(self.__transaction_history)
        }

def create_secure_account():
    """사용자 입력으로 안전한 계좌 생성"""
    print("=== 안전한 은행 계좌 개설 ===")
    
    owner = input("계좌 소유자 이름: ")
    
    try:
        initial_balance = int(input("초기 입금액: "))
        if initial_balance < 0:
            print("초기 입금액은 0 이상이어야 합니다.")
            initial_balance = 0
    except ValueError:
        print("잘못된 입력입니다. 초기 잔액을 0원으로 설정합니다.")
        initial_balance = 0
    
    account_number = input("계좌번호 (예: 123-456-789): ")
    
    return SecureBankAccount(owner, initial_balance, account_number)

def banking_system():
    """안전한 뱅킹 시스템 시뮬레이터"""
    print("🏦 안전한 뱅킹 시스템에 오신 것을 환영합니다!")
    
    account = create_secure_account()
    
    while True:
        print(f"\n{'='*50}")
        print(f"🏦 {account.owner}님의 계좌 관리")
        print(f"{'='*50}")
        print("📋 메뉴:")
        print("1. 잔액 조회")
        print("2. 입금")
        print("3. 출금")
        print("4. 거래내역 조회")
        print("5. 비밀번호 변경")
        print("6. 시스템 종료")
        
        choice = input("\n원하는 서비스를 선택하세요 (1-6): ")
        
        if choice == "1":
            pin = input("비밀번호 4자리: ")
            account.get_balance(pin)
        
        elif choice == "2":
            pin = input("비밀번호 4자리: ")
            try:
                amount = int(input("입금할 금액: "))
                account.deposit(amount, pin)
            except ValueError:
                print("❌ 금액은 숫자로 입력해주세요.")
        
        elif choice == "3":
            pin = input("비밀번호 4자리: ")
            try:
                amount = int(input("출금할 금액: "))
                account.withdraw(amount, pin)
            except ValueError:
                print("❌ 금액은 숫자로 입력해주세요.")
        
        elif choice == "4":
            pin = input("비밀번호 4자리: ")
            account.get_transaction_history(pin)
        
        elif choice == "5":
            old_pin = input("현재 비밀번호: ")
            new_pin = input("새 비밀번호 4자리: ")
            account.change_pin(old_pin, new_pin)
        
        elif choice == "6":
            print(f"\n👋 {account.owner}님, 안전한 뱅킹을 이용해 주셔서 감사합니다!")
            break
        
        else:
            print("❌ 잘못된 선택입니다. 1-6 중에서 선택해주세요.")

if __name__ == "__main__":
    banking_system()
```

### 📌 핵심 개념 3: 캡슐화의 실제 구현 (10분)

#### 📦 **캡슐화 (Encapsulation)**

**캡슐화의 정의:**
관련된 데이터(속성)와 기능(메서드)을 하나의 단위(클래스)로 묶고, 외부에서는 정해진 인터페이스를 통해서만 접근할 수 있게 하는 것

**캡슐화의 핵심 원칙:**
1. **데이터 보호**: 중요한 데이터는 직접 접근 불가
2. **메서드 제공**: 안전한 방법으로만 데이터 조작
3. **인터페이스 설계**: 사용하기 쉬운 공개 메서드 제공

```python
class CapsulatedTimer:
    """캡슐화를 적용한 타이머 클래스"""
    
    def __init__(self, name):
        # Public 인터페이스
        self.name = name
        
        # Private 데이터 (보호됨)
        self.__start_time = None
        self.__end_time = None
        self.__is_running = False
        self.__total_elapsed = 0
        
        print(f"⏰ '{name}' 타이머가 준비되었습니다!")
    
    # Public 인터페이스 (외부에서 사용)
    def start(self):
        """타이머 시작"""
        if self.__is_running:
            print("⚠️ 타이머가 이미 실행 중입니다!")
            return False
        
        from time import time
        self.__start_time = time()
        self.__is_running = True
        print(f"▶️ {self.name} 타이머 시작!")
        return True
    
    def stop(self):
        """타이머 정지"""
        if not self.__is_running:
            print("⚠️ 타이머가 실행 중이 아닙니다!")
            return False
        
        from time import time
        self.__end_time = time()
        elapsed = self.__end_time - self.__start_time
        self.__total_elapsed += elapsed
        self.__is_running = False
        
        print(f"⏹️ {self.name} 타이머 정지!")
        print(f"   이번 측정: {elapsed:.2f}초")
        return elapsed
    
    def get_elapsed_time(self):
        """경과 시간 조회"""
        if self.__is_running:
            from time import time
            current_time = time()
            current_elapsed = current_time - self.__start_time
            print(f"⏰ 현재 경과시간: {current_elapsed:.2f}초 (실행 중)")
            return current_elapsed
        else:
            print(f"⏰ 총 경과시간: {self.__total_elapsed:.2f}초")
            return self.__total_elapsed
    
    def reset(self):
        """타이머 리셋"""
        self.__start_time = None
        self.__end_time = None
        self.__is_running = False
        self.__total_elapsed = 0
        print(f"🔄 {self.name} 타이머가 리셋되었습니다!")
    
    def get_status(self):
        """타이머 상태 조회"""
        status = "실행 중" if self.__is_running else "정지됨"
        print(f"📊 {self.name} 상태: {status}")
        print(f"   누적 시간: {self.__total_elapsed:.2f}초")
        return {
            'name': self.name,
            'is_running': self.__is_running,
            'total_elapsed': self.__total_elapsed
        }

# 사용 예시
def timer_demo():
    timer_name = input("타이머 이름을 입력하세요: ")
    timer = CapsulatedTimer(timer_name)
    
    print("\n명령어: start, stop, time, status, reset, quit")
    
    while True:
        command = input(f"\n[{timer.name}] 명령 입력: ").lower()
        
        if command == "start":
            timer.start()
        elif command == "stop":
            timer.stop()
        elif command == "time":
            timer.get_elapsed_time()
        elif command == "status":
            timer.get_status()
        elif command == "reset":
            timer.reset()
        elif command == "quit":
            print("타이머를 종료합니다.")
            break
        else:
            print("❌ 알 수 없는 명령어입니다.")

if __name__ == "__main__":
    timer_demo()
```

---

## ☕ 휴식 시간 (10분)

---

## 🎯 3부: 상속성과 다형성 기초 - 객체를 효율적으로 확장하는 방법 (40분)

### 📌 핵심 개념 1: 상속성 - 기존 객체의 특성 물려받기 (20분)

#### 👨‍👦 **상속성 (Inheritance)의 개념**

**상속성의 정의:**
기존 클래스(부모 클래스)의 속성과 메서드를 새로운 클래스(자식 클래스)가 물려받아 재사용하고 확장할 수 있게 하는 객체 운영 기법

**일상생활의 상속 예시:**
```
👨 아버지 (부모 클래스):
   - 특성: 키 180cm, 성격 온화, 요리 잘함
   - 능력: 운전하기, 수영하기, 피아노 치기

👦 아들 (자식 클래스):
   - 물려받은 특성: 키 크다, 성격 온화, 요리 잘함 ✅
   - 물려받은 능력: 운전하기, 수영하기, 피아노 치기 ✅
   - 새로운 특성: 컴퓨터 잘함 🆕
   - 새로운 능력: 게임하기, 프로그래밍하기 🆕
```

#### 🎮 **게임 캐릭터로 배우는 상속성**

**알고리즘 말투로 요구사항 표현:**
1. "기본 게임 캐릭터의 공통 특성을 정의한다"
2. "전사, 마법사, 궁수 등은 기본 특성을 물려받는다"
3. "각 직업별로 고유한 특성과 능력을 추가한다"
4. "사용자가 직업을 선택하여 캐릭터를 만들 수 있게 한다"

**코드로 구현:**

```python
# 부모 클래스 (기본 캐릭터)
class GameCharacter:
    """모든 게임 캐릭터의 기본 클래스"""
    
    def __init__(self, name, level=1):
        self.name = name
        self.level = level
        self.hp = 100
        self.mp = 50
        self.exp = 0
        
        print(f"⚔️ 캐릭터 '{name}'이(가) 생성되었습니다!")
    
    def show_status(self):
        """기본 상태 표시"""
        print(f"\n👤 === {self.name} ===")
        print(f"   레벨: {self.level}")
        print(f"   HP: {self.hp}")
        print(f"   MP: {self.mp}")
        print(f"   경험치: {self.exp}")
    
    def level_up(self):
        """기본 레벨업"""
        self.level += 1
        self.hp += 20
        self.mp += 10
        print(f"🎉 {self.name}이(가) 레벨 {self.level}로 성장했습니다!")
    
    def basic_attack(self, target):
        """기본 공격"""
        damage = 10
        print(f"⚔️ {self.name}이(가) {target}을(를) 공격했습니다! (데미지: {damage})")
        return damage

# 자식 클래스 1: 전사
class Warrior(GameCharacter):  # GameCharacter를 상속받음
    """전사 클래스 - 높은 HP와 강한 물리 공격력"""
    
    def __init__(self, name, level=1):
        # 부모 클래스의 초기화 호출
        super().__init__(name, level)
        
        # 전사만의 특성 추가
        self.hp += 50        # 전사는 HP가 높음
        self.strength = 20   # 전사만의 힘 스탯
        self.armor = 15      # 전사만의 방어력
        
        print(f"🛡️ 강인한 전사로 각성했습니다!")
    
    def show_status(self):
        """전사 전용 상태 표시 (기본 상태 + 전사 특성)"""
        super().show_status()  # 부모의 메서드 호출
        print(f"   힘: {self.strength}")
        print(f"   방어력: {self.armor}")
        print(f"   직업: 전사 🛡️")
    
    def power_attack(self, target):
        """전사만의 특수 기술"""
        if self.mp < 10:
            print("💙 MP가 부족합니다!")
            return False
        
        self.mp -= 10
        damage = self.strength * 2
        print(f"💥 {self.name}이(가) {target}에게 강력한 일격을 가했습니다!")
        print(f"   데미지: {damage}! MP 소모: 10")
        return damage
    
    def defend(self):
        """전사만의 방어 기술"""
        shield_effect = self.armor
        print(f"🛡️ {self.name}이(가) 방패를 들어 {shield_effect}만큼 데미지를 막습니다!")
        return shield_effect

# 자식 클래스 2: 마법사
class Mage(GameCharacter):
    """마법사 클래스 - 높은 MP와 강한 마법 공격력"""
    
    def __init__(self, name, level=1):
        super().__init__(name, level)
        
        # 마법사만의 특성
        self.mp += 100       # 마법사는 MP가 높음
        self.intelligence = 25  # 마법사만의 지능 스탯
        self.mana_regen = 5     # 마법사만의 마나 회복력
        
        print(f"✨ 신비로운 마법사로 각성했습니다!")
    
    def show_status(self):
        """마법사 전용 상태 표시"""
        super().show_status()
        print(f"   지능: {self.intelligence}")
        print(f"   마나 회복: {self.mana_regen}")
        print(f"   직업: 마법사 ✨")
    
    def cast_fireball(self, target):
        """마법사만의 특수 마법"""
        if self.mp < 20:
            print("💙 MP가 부족합니다!")
            return False
        
        self.mp -= 20
        damage = self.intelligence * 1.5
        print(f"🔥 {self.name}이(가) {target}에게 화염구를 시전했습니다!")
        print(f"   마법 데미지: {damage}! MP 소모: 20")
        return damage
    
    def meditate(self):
        """마법사만의 명상 (MP 회복)"""
        mp_recovery = self.mana_regen * 3
        self.mp = min(150, self.mp + mp_recovery)  # 최대 MP 제한
        print(f"🧘 {self.name}이(가) 명상으로 MP를 {mp_recovery} 회복했습니다!")
        print(f"   현재 MP: {self.mp}")

# 자식 클래스 3: 궁수
class Archer(GameCharacter):
    """궁수 클래스 - 밸런스형이지만 민첩성이 높음"""
    
    def __init__(self, name, level=1):
        super().__init__(name, level)
        
        # 궁수만의 특성
        self.agility = 30    # 궁수만의 민첩 스탯
        self.accuracy = 85   # 궁수만의 명중률
        self.arrows = 50     # 궁수만의 화살 개수
        
        print(f"🏹 재빠른 궁수로 각성했습니다!")
    
    def show_status(self):
        """궁수 전용 상태 표시"""
        super().show_status()
        print(f"   민첩성: {self.agility}")
        print(f"   명중률: {self.accuracy}%")
        print(f"   화살: {self.arrows}개")
        print(f"   직업: 궁수 🏹")
    
    def shoot_arrow(self, target):
        """궁수만의 화살 공격"""
        if self.arrows <= 0:
            print("🏹 화살이 부족합니다!")
            return False
        
        self.arrows -= 1
        import random
        hit_chance = random.randint(1, 100)
        
        if hit_chance <= self.accuracy:
            damage = self.agility * 0.8
            print(f"🎯 {self.name}의 화살이 {target}에게 명중했습니다!")
            print(f"   데미지: {damage}! 남은 화살: {self.arrows}개")
            return damage
        else:
            print(f"💨 {self.name}의 화살이 빗나갔습니다! 남은 화살: {self.arrows}개")
            return 0
    
    def rapid_fire(self, target):
        """궁수만의 연속 사격"""
        if self.arrows < 3:
            print("🏹 연속 사격에 필요한 화살이 부족합니다! (3개 필요)")
            return False
        
        if self.mp < 15:
            print("💙 MP가 부족합니다!")
            return False
        
        self.arrows -= 3
        self.mp -= 15
        total_damage = 0
        
        print(f"🏹💨 {self.name}이(가) {target}에게 연속 사격을 가합니다!")
        for i in range(3):
            damage = self.agility * 0.6
            total_damage += damage
            print(f"   {i+1}번째 화살: {damage} 데미지!")
        
        print(f"   총 데미지: {total_damage}! 남은 화살: {self.arrows}개")
        return total_damage

def create_character():
    """사용자 입력으로 캐릭터 생성"""
    print("=== 캐릭터 생성 ===")
    name = input("캐릭터 이름: ")
    
    print("\n직업을 선택하세요:")
    print("1. 전사 🛡️ (높은 HP, 강한 물리 공격)")
    print("2. 마법사 ✨ (높은 MP, 강한 마법 공격)")  
    print("3. 궁수 🏹 (높은 민첩성, 원거리 공격)")
    
    class_choice = input("선택 (1-3): ")
    
    if class_choice == "1":
        return Warrior(name)
    elif class_choice == "2":
        return Mage(name)
    elif class_choice == "3":
        return Archer(name)
    else:
        print("잘못된 선택입니다. 기본 캐릭터로 생성합니다.")
        return GameCharacter(name)

def character_demo():
    """상속 데모 프로그램"""
    print("🎮 상속성 데모: RPG 캐릭터 시스템")
    
    character = create_character()
    character.show_status()
    
    print(f"\n🎯 {character.name}의 모험이 시작됩니다!")
    print("명령어: status, attack, special, quit")
    
    while True:
        command = input(f"\n[{character.name}] 행동 선택: ").lower()
        
        if command == "status":
            character.show_status()
        
        elif command == "attack":
            target = input("공격할 대상: ")
            character.basic_attack(target)
        
        elif command == "special":
            target = input("특수 공격할 대상: ")
            
            if isinstance(character, Warrior):
                character.power_attack(target)
            elif isinstance(character, Mage):
                character.cast_fireball(target)
            elif isinstance(character, Archer):
                character.shoot_arrow(target)
            else:
                print("특수 공격이 없습니다.")
        
        elif command == "quit":
            print(f"👋 {character.name}의 모험이 끝났습니다!")
            break
        
        else:
            print("❌ 알 수 없는 명령어입니다.")

if __name__ == "__main__":
    character_demo()
```

### 📌 핵심 개념 2: 다형성 - 같은 명령, 다른 동작 (20분)

#### 🎭 **다형성 (Polymorphism)의 개념**

**다형성의 정의:**
같은 이름의 메서드나 기능이 서로 다른 객체에서 각자의 방식으로 동작할 수 있게 하는 객체 운영 기법

**일상생활의 다형성 예시:**
```
🎵 "연주하기" 명령:
   🎹 피아노 → 건반을 누르며 연주
   🎸 기타 → 줄을 튕기며 연주  
   🥁 드럼 → 스틱으로 치며 연주
   
   같은 "연주하기" 명령이지만 각 악기마다 다른 방식!
```

#### 🚗 **교통수단으로 배우는 다형성**

**알고리즘 말투로 요구사항 표현:**
1. "모든 교통수단이 공통으로 가져야 할 기능을 정의한다"
2. "각 교통수단은 자신만의 방식으로 그 기능을 구현한다"
3. "사용자는 교통수단의 종류와 관계없이 같은 명령을 사용한다"
4. "프로그램이 자동으로 적절한 방식을 선택하여 실행한다"

**코드로 구현:**

```python
# 부모 클래스 (기본 교통수단)
class Vehicle:
    """모든 교통수단의 기본 클래스"""
    
    def __init__(self, name, speed=0):
        self.name = name
        self.speed = speed
        self.is_moving = False
    
    def start_engine(self):
        """엔진 시작 - 각 교통수단마다 다르게 구현됨 (다형성)"""
        print(f"🔧 {self.name}의 엔진을 시작합니다.")
    
    def move(self):
        """이동 - 각 교통수단마다 다르게 구현됨 (다형성)"""
        if not self.is_moving:
            self.is_moving = True
            print(f"🚀 {self.name}이(가) 이동을 시작합니다.")
    
    def stop(self):
        """정지 - 공통 기능"""
        self.is_moving = False
        self.speed = 0
        print(f"⏹️ {self.name}이(가) 정지했습니다.")
    
    def show_status(self):
        """상태 표시 - 공통 기능"""
        status = "이동 중" if self.is_moving else "정지"
        print(f"📊 {self.name}: {status}, 속도: {self.speed}km/h")

# 자식 클래스들 (각각 다른 방식으로 동작)
class Car(Vehicle):
    """자동차 - 도로에서 운행"""
    
    def start_engine(self):
        """자동차만의 시동 방식"""
        print(f"🚗 {self.name}: 열쇠를 돌려 엔진을 시동걸었습니다!")
        print("   부르르르... 엔진 소리가 들립니다.")
    
    def move(self):
        """자동차만의 이동 방식"""
        super().move()
        self.speed = 60
        print(f"🛣️ {self.name}이(가) 도로에서 {self.speed}km/h로 달립니다!")
    
    def honk(self):
        """자동차만의 특수 기능"""
        print(f"📯 {self.name}: 빵빵! 경적을 울립니다!")

class Airplane(Vehicle):
    """비행기 - 하늘에서 비행"""
    
    def start_engine(self):
        """비행기만의 시동 방식"""
        print(f"✈️ {self.name}: 제트 엔진을 가동합니다!")
        print("   우우우웅... 강력한 엔진 소리가 울립니다.")
    
    def move(self):
        """비행기만의 이동 방식"""
        super().move()
        self.speed = 800
        print(f"☁️ {self.name}이(가) 하늘을 {self.speed}km/h로 날아갑니다!")
    
    def fly_high(self):
        """비행기만의 특수 기능"""
        print(f"🆙 {self.name}이(가) 고도를 높입니다! 구름 위를 날아갑니다!")

class Ship(Vehicle):
    """배 - 바다에서 항해"""
    
    def start_engine(self):
        """배만의 시동 방식"""
        print(f"🚢 {self.name}: 선박 엔진을 가동합니다!")
        print("   푸푸푸... 디젤 엔진 소리가 웅웅거립니다.")
    
    def move(self):
        """배만의 이동 방식"""
        super().move()
        self.speed = 30
        print(f"🌊 {self.name}이(가) 바다를 {self.speed}km/h로 항해합니다!")
    
    def anchor(self):
        """배만의 특수 기능"""
        print(f"⚓ {self.name}이(가) 닻을 내려 안전하게 정박합니다!")

class Bicycle(Vehicle):
    """자전거 - 사람이 직접 운전"""
    
    def start_engine(self):
        """자전거만의 시동 방식 (엔진이 없음!)"""
        print(f"🚲 {self.name}: 엔진이 없습니다! 페달을 밟을 준비를 합니다!")
        print("   다리에 힘을 주고... 준비 완료!")
    
    def move(self):
        """자전거만의 이동 방식"""
        super().move()
        self.speed = 20
        print(f"🚴 {self.name}을(를) 페달을 밟아 {self.speed}km/h로 달립니다!")
    
    def ring_bell(self):
        """자전거만의 특수 기능"""
        print(f"🔔 {self.name}: 딸랑딸랑! 자전거 벨을 울립니다!")

def create_vehicle():
    """사용자 입력으로 교통수단 생성"""
    print("=== 교통수단 선택 ===")
    
    print("이용 가능한 교통수단:")
    print("1. 자동차 🚗 (도로 이동)")
    print("2. 비행기 ✈️ (하늘 이동)")
    print("3. 배 🚢 (바다 이동)")
    print("4. 자전거 🚲 (친환경 이동)")
    
    choice = input("선택 (1-4): ")
    name = input("교통수단 이름: ")
    
    if choice == "1":
        return Car(name)
    elif choice == "2":
        return Airplane(name)
    elif choice == "3":
        return Ship(name)
    elif choice == "4":
        return Bicycle(name)
    else:
        print("잘못된 선택입니다. 기본 교통수단으로 생성합니다.")
        return Vehicle(name)

def polymorphism_demo():
    """다형성 데모 - 여러 교통수단 관리"""
    print("🚗✈️🚢🚲 다형성 데모: 교통수단 관리 시스템")
    
    vehicles = []  # 다양한 교통수단들을 저장
    
    # 여러 교통수단 생성
    print("\n교통수단들을 생성해봅시다!")
    for i in range(2):
        print(f"\n{i+1}번째 교통수단:")
        vehicle = create_vehicle()
        vehicles.append(vehicle)
    
    while True:
        print(f"\n{'='*60}")
        print("🚦 교통수단 관리 시스템")
        print(f"{'='*60}")
        
        # 현재 교통수단들 상태 표시
        print("📋 현재 교통수단들:")
        for i, vehicle in enumerate(vehicles, 1):
            print(f"  {i}. ", end="")
            vehicle.show_status()
        
        print("\n📋 메뉴:")
        print("1. 모든 교통수단 시동 걸기")
        print("2. 모든 교통수단 출발")
        print("3. 모든 교통수단 정지")
        print("4. 특정 교통수단 특수 기능 사용")
        print("5. 새 교통수단 추가")
        print("6. 시스템 종료")
        
        choice = input("\n원하는 기능을 선택하세요 (1-6): ")
        
        if choice == "1":
            print("\n🔧 === 모든 교통수단 시동 걸기 ===")
            for vehicle in vehicles:
                vehicle.start_engine()  # 다형성! 각자 다른 방식으로 시동
                print()
        
        elif choice == "2":
            print("\n🚀 === 모든 교통수단 출발! ===")
            for vehicle in vehicles:
                vehicle.move()  # 다형성! 각자 다른 방식으로 이동
                print()
        
        elif choice == "3":
            print("\n⏹️ === 모든 교통수단 정지 ===")
            for vehicle in vehicles:
                vehicle.stop()  # 공통 기능
        
        elif choice == "4":
            if not vehicles:
                print("❌ 등록된 교통수단이 없습니다.")
                continue
                
            print("\n🎯 특수 기능을 사용할 교통수단을 선택하세요:")
            for i, vehicle in enumerate(vehicles, 1):
                print(f"  {i}. {vehicle.name} ({type(vehicle).__name__})")
            
            try:
                vehicle_idx = int(input("번호 선택: ")) - 1
                if 0 <= vehicle_idx < len(vehicles):
                    selected = vehicles[vehicle_idx]
                    
                    # 타입에 따라 다른 특수 기능 실행 (다형성)
                    if isinstance(selected, Car):
                        selected.honk()
                    elif isinstance(selected, Airplane):
                        selected.fly_high()
                    elif isinstance(selected, Ship):
                        selected.anchor()
                    elif isinstance(selected, Bicycle):
                        selected.ring_bell()
                    else:
                        print("이 교통수단은 특수 기능이 없습니다.")
                else:
                    print("❌ 잘못된 번호입니다.")
            except ValueError:
                print("❌ 숫자를 입력해주세요.")
        
        elif choice == "5":
            print("\n➕ 새 교통수단 추가")
            new_vehicle = create_vehicle()
            vehicles.append(new_vehicle)
            print(f"✅ {new_vehicle.name}이(가) 추가되었습니다!")
        
        elif choice == "6":
            print("\n👋 교통수단 관리 시스템을 종료합니다.")
            print("🌟 다형성 덕분에 다양한 교통수단을 하나의 방식으로 관리할 수 있었습니다!")
            break
        
        else:
            print("❌ 잘못된 선택입니다. 1-6 중에서 선택해주세요.")

if __name__ == "__main__":
    polymorphism_demo()
```

---

## 🎯 실습과제 (60분)

### 📝 **과제 1: 스마트 디바이스 관리 시스템 (30분)**

**객체지향 4대 요소를 모두 적용한 종합 시스템 구현**

**알고리즘 말투로 요구사항 표현:**

1. **추상화**: "스마트 디바이스의 공통 특성과 기능을 추상화한다"
2. **정보은닉**: "디바이스의 중요한 정보는 보호하고 안전한 인터페이스만 제공한다"
3. **상속성**: "기본 디바이스 클래스를 상속받아 특화된 디바이스들을 만든다"
4. **다형성**: "같은 명령으로 다양한 디바이스들이 각자의 방식으로 동작한다"

**구현해야 할 클래스들:**
- `SmartDevice` (부모 클래스): 모든 스마트 디바이스의 기본 특성
- `SmartPhone` (자식): 전화, 문자, 앱 관리 기능
- `SmartTV` (자식): 채널, 볼륨, 스트리밍 기능  
- `SmartSpeaker` (자식): 음성 인식, 음악 재생, 스마트홈 제어
- `SmartWatch` (자식): 건강 관리, 알림, 운동 추적

**필수 구현 기능:**
- 모든 디바이스 공통: 전원 on/off, 상태 확인, 배터리 관리
- 각 디바이스별 고유 기능 3개 이상
- 사용자 입력을 통한 디바이스 생성 및 조작
- 여러 디바이스를 동시에 관리하는 시스템

### 📝 **과제 2: 온라인 학습 플랫폼 시스템 (30분)**

**알고리즘 말투로 요구사항 표현:**

1. **추상화**: "온라인 학습의 핵심 요소들을 추상화한다"
2. **정보은닉**: "학습자의 개인정보와 성적은 보호하되 필요한 기능만 제공한다"
3. **상속성**: "기본 사용자에서 학습자, 강사, 관리자 역할을 상속으로 구현한다"
4. **다형성**: "같은 '학습하기' 명령으로 다양한 학습 방식을 지원한다"

**구현해야 할 클래스들:**
- `User` (부모 클래스): 기본 사용자 정보
- `Student` (자식): 강의 수강, 과제 제출, 성적 관리
- `Instructor` (자식): 강의 생성, 성적 입력, 피드백 제공
- `Course` (강의 클래스): 강의 정보 및 학습 자료 관리
- `Assignment` (과제 클래스): 과제 정보 및 제출 관리

**필수 구현 기능:**
- 사용자별 로그인 시스템 (정보은닉 적용)
- 강의 등록 및 수강 시스템
- 과제 제출 및 채점 시스템
- 학습 진도 추적 및 통계
- 역할별 다른 메뉴 시스템 (다형성 적용)

---

## 📚 오늘 배운 내용 정리

### ✅ 핵심 포인트

**객체지향의 4대 요소:**

1. **추상화 (Abstraction)** - 🏗️ **가장 중요한 개념**
   - 실세계의 복잡한 사물에서 프로그램 목적에 맞는 핵심만 선별
   - 불필요한 정보는 과감히 제거하여 단순화
   - 목적에 따라 같은 사물도 다르게 추상화 가능

2. **정보은닉 (Information Hiding)** - 🔒 **객체 운영 요소**
   - 객체의 내부 구현을 외부에서 직접 접근하지 못하도록 보호
   - Private (__), Protected (_), Public 접근 제어 수준 활용
   - 안전한 메서드를 통해서만 데이터 조작 허용

3. **상속성 (Inheritance)** - 👨‍👦 **객체 운영 요소**
   - 기존 클래스의 속성과 메서드를 새로운 클래스가 물려받기
   - 코드 재사용성과 확장성 향상
   - super()를 통한 부모 클래스 메서드 호출

4. **다형성 (Polymorphism)** - 🎭 **객체 운영 요소**
   - 같은 이름의 메서드가 객체마다 다른 방식으로 동작
   - 유연하고 확장 가능한 시스템 설계 가능
   - isinstance()를 통한 타입 확인과 적절한 처리

### 🏠 다음 주까지 해볼 과제

1. **객체지향 4대 요소 실습**:
   - 일상생활의 다양한 개념들을 4대 요소를 적용하여 설계
   - 각 요소가 왜 필요한지 실제로 체험해보기

2. **추상화 연습**:
   - 같은 실세계 객체를 다른 목적으로 여러 번 추상화해보기
   - 목적에 따른 추상화의 차이점 분석하기

3. **실습 과제 완성**:
   - 스마트 디바이스 관리 시스템 완전 구현
   - 온라인 학습 플랫폼 시스템 완전 구현

4. **심화 학습**:
   - 메서드 오버라이딩과 오버로딩 개념 학습
   - 추상 클래스와 인터페이스 개념 미리 학습

### 🔮 다음 주 예고

**9주차: 모듈, 패키지 및 파일 관리**
- 클래스들을 여러 파일로 분리하는 방법
- import 문과 패키지 구조 설계
- 파일 입출력과 데이터 영속성
- 예외 처리를 통한 안정적인 프로그램 작성

### 💡 마지막 정리

**지금까지의 성장 과정:**
```
1주차: "프로그래밍이 뭔지 알았다!" (기본 구조) ✅
2주차: "어디서든 코딩할 수 있게 되었다!" (개발환경) ✅
3주차: "변수로 복잡한 문제를 해결할 수 있다!" (자료형) ✅
4주차: "조건문으로 똑똑한 프로그램을 만들 수 있다!" (선택구조) ✅
5주차: "반복문으로 효율적인 프로그램을 만들 수 있다!" (반복구조) ✅
6주차: "자료구조로 체계적인 데이터 관리를 할 수 있다!" (컬렉션) ✅
7주차: "함수로 재사용 가능한 코드를 만들 수 있다!" (모듈화) ✅
8주차: "객체지향으로 현실 세계를 프로그램으로 만들 수 있다!" ✅
```

**오늘 여러분이 할 수 있게 된 것들:**
- 🏗️ **추상화**: 복잡한 현실을 프로그램 목적에 맞게 단순화하기
- 🔒 **정보은닉**: 중요한 데이터를 보호하고 안전한 인터페이스 제공하기
- 👨‍👦 **상속성**: 기존 코드를 재사용하여 효율적으로 확장하기
- 🎭 **다형성**: 같은 명령으로 다양한 객체들이 각자의 방식으로 동작하게 하기

**객체지향 프로그래밍의 진정한 가치:**
오늘 배운 객체지향의 4대 요소는 단순한 프로그래밍 기법이 아닙니다. 이는 복잡한 현실 세계를 체계적으로 모델링하고, 유지보수 가능한 대규모 소프트웨어를 설계하는 핵심 사고방식입니다.

**실무에서의 활용:**
```python
# 실제 기업 시스템에서는 이런 구조를 사용합니다
class User:           # 추상화: 사용자의 핵심 특성만
    pass
    
class Customer(User): # 상속성: 사용자를 확장
    pass
    
class Employee(User): # 상속성: 사용자를 확장
    pass

# 다형성: 같은 login() 메서드로 다른 처리
def process_login(user):
    user.login()  # Customer든 Employee든 각자의 방식으로 로그인
```

**마지막 격려:**
객체지향의 4대 요소를 마스터한다는 것은 프로그래밍에서 소프트웨어 엔지니어링으로 한 단계 성장하는 것입니다. 이제 여러분은 Netflix, 카카오톡, 게임 같은 복잡한 시스템의 설계 원리를 이해할 수 있어요!

**추상화**로 현실을 모델링하고, **정보은닉**으로 안전하게 보호하며, **상속**으로 효율적으로 확장하고, **다형성**으로 유연하게 처리하는 진정한 객체지향 개발자가 되셨습니다! 🌟

다음 주에는 이런 멋진 클래스들을 체계적으로 관리하는 방법을 배워봅시다! 💪

---

**🎯 8주차 학습 완료! 수고하셨습니다! 🎉**