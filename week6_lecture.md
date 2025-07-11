# 6주차: 자료구조와 객체 개념 소개
**총 강의시간: 3시간 20분 (200분)**
- 강의: 120분 (3부로 구성)
- 휴식: 20분 (10분씩 2회)
- 실습: 60분

---

## 🎯 1부: 자료구조의 필요성과 리스트 완전 정복 (40분)

### 📌 핵심 개념 1: 지금까지의 여정과 새로운 도전 (5분)

#### 🔄 **지금까지 우리가 마스터한 것들**

**1주차**: 프로그래밍의 3대 마법 구조 ✅
- 순차: "차례대로 하나씩"
- 선택: "상황에 따라 다르게"  
- 반복: "조건 만족할 때까지 계속"

**2주차**: 개발환경 완전 정복 ✅

**3주차**: 변수와 자료형으로 복잡한 데이터 처리 ✅

**4주차**: 조건문으로 똑똑한 판단력 구현 ✅

**5주차**: 반복문으로 효율적인 작업 처리 ✅

**오늘 해결할 문제**: 
많은 데이터를 체계적으로 관리하고, 관련된 데이터들을 하나로 묶어서 처리하려면 어떻게 해야 할까?

### 📌 핵심 개념 2: 왜 자료구조가 필요한가? - 데이터 관리의 한계 (15분)

#### 🤔 **현실적인 문제 상황: 변수의 한계**

**예시: 10명 학생의 점수 관리**

```python
# 😰 변수로만 관리하면... (끔찍한 코드!)
student1_score = 85
student2_score = 92
student3_score = 78
student4_score = 96
student5_score = 88
student6_score = 84
student7_score = 91
student8_score = 87
student9_score = 93
student10_score = 89

# 평균을 구하려면?
total = student1_score + student2_score + student3_score + student4_score + student5_score + student6_score + student7_score + student8_score + student9_score + student10_score
average = total / 10

# 최고점을 찾으려면?
max_score = student1_score
if student2_score > max_score:
    max_score = student2_score
if student3_score > max_score:
    max_score = student3_score
# ... 10번 반복! 😱

print(f"평균: {average}, 최고점: {max_score}")
```

**이 코드의 심각한 문제점들:**
1. **코드 중복**: 비슷한 변수를 10개나 만들어야 함 🔄
2. **확장성 제로**: 학생이 100명이라면? 변수 100개! 😰
3. **처리의 복잡성**: 간단한 계산도 엄청나게 복잡해짐 📈
4. **실수 위험**: 변수명을 하나라도 빼먹으면 오류 ❌

#### 💡 **자료구조의 등장 - 데이터 관리의 혁명**

**같은 기능을 리스트로 작성하면:**

```python
# ✅ 리스트를 사용한 깔끔한 코드
student_scores = [85, 92, 78, 96, 88, 84, 91, 87, 93, 89]

# 평균 구하기 - 한 줄로!
average = sum(student_scores) / len(student_scores)

# 최고점 찾기 - 한 줄로!
max_score = max(student_scores)

print(f"평균: {average}, 최고점: {max_score}")

# 🎉 학생이 100명? 1000명? 코드는 그대로!
```

**자료구조의 놀라운 효과:**
- 10개 변수 → 1개 리스트로 압축! 📉
- 복잡한 계산 → 내장 함수로 간단히! ⚡
- 확장성 무제한! 📈

#### 🏗️ **일상생활의 자료구조 개념**

**도서관의 책 정리 시스템:**
```
📚 책장 (리스트와 비슷)
- 소설 책장: [해리포터1, 해리포터2, 반지의제왕...]
- 과학 책장: [물리학개론, 화학기초, 생물학...]
- 순서가 중요하고, 같은 책도 여러 권 있을 수 있음

📖 도서 카탈로그 (딕셔너리와 비슷)  
- ISBN: 책 정보
- "978-89-..." : {제목: "파이썬 입문", 저자: "김개발", 위치: "3층 A-15"}
- 고유한 번호로 빠르게 찾기

👥 독서클럽 회원 (세트와 비슷)
- {김철수, 이영희, 박민수, 최지영}
- 중복 회원 없음, 순서는 중요하지 않음
```

### 📌 핵심 개념 3: 리스트 - 순서가 있는 데이터 모음 (20분)

#### 📋 **리스트의 기본 개념**

**리스트 = 순서가 있는 데이터 상자들**

```python
# 리스트 생성하기
fruits = ["사과", "바나나", "오렌지"]
numbers = [1, 3, 5, 7, 9]
mixed_data = ["김철수", 20, 85.5, True]  # 다른 타입도 함께 저장 가능

print(f"과일들: {fruits}")
print(f"숫자들: {numbers}")
print(f"혼합 데이터: {mixed_data}")
```

#### 🎯 **리스트 기본 조작 - "알고리즘 말투" 접근법**

**문제**: 사용자로부터 5명의 학생 이름을 입력받아 리스트에 저장하고 관리하기

**알고리즘 말투로 표현:**
1. "빈 리스트를 만든다"
2. "5번 반복한다:"
   - "사용자로부터 학생 이름을 입력받는다"
   - "입력받은 이름을 리스트에 추가한다"
3. "저장된 모든 이름을 출력한다"
4. "특정 이름을 검색할 수 있게 한다"

**코드로 구현:**

```python
# 1. 빈 리스트 만들기
student_names = []

print("=== 학생 이름 관리 시스템 ===")
print("5명의 학생 이름을 입력해주세요:")

# 2. 5번 반복하여 이름 입력받기
for i in range(5):
    name = input(f"{i+1}번째 학생 이름: ")
    student_names.append(name)  # 리스트에 추가
    print(f"  → '{name}' 저장됨")

# 3. 저장된 모든 이름 출력
print(f"\n📋 저장된 학생 목록:")
for i in range(len(student_names)):
    print(f"  {i+1}. {student_names[i]}")

# 4. 특정 이름 검색
search_name = input(f"\n🔍 검색할 학생 이름: ")
if search_name in student_names:
    position = student_names.index(search_name) + 1
    print(f"✅ '{search_name}' 학생을 {position}번째에서 찾았습니다!")
else:
    print(f"❌ '{search_name}' 학생을 찾을 수 없습니다.")
```

#### 📊 **리스트 인덱싱과 슬라이싱**

**인덱스 = 데이터의 위치 번호**

```python
# 다양한 과일 리스트로 실습
fruits = ["딸기", "바나나", "사과", "오렌지", "포도"]

print("=== 리스트 인덱싱 실습 ===")
print(f"전체 과일: {fruits}")

# 양수 인덱스 (앞에서부터)
print(f"첫 번째 과일: {fruits[0]}")    # 딸기
print(f"세 번째 과일: {fruits[2]}")    # 사과

# 음수 인덱스 (뒤에서부터)
print(f"마지막 과일: {fruits[-1]}")    # 포도
print(f"뒤에서 두 번째: {fruits[-2]}")  # 오렌지

# 슬라이싱 (일부분 잘라내기)
print(f"처음 3개: {fruits[:3]}")      # ['딸기', '바나나', '사과']
print(f"2번째부터 4번째까지: {fruits[1:4]}")  # ['바나나', '사과', '오렌지']
print(f"마지막 2개: {fruits[-2:]}")    # ['오렌지', '포도']
```

#### 🔧 **리스트 메서드 활용**

**문제**: 쇼핑 목록을 관리하는 프로그램 만들기

**알고리즘 말투로 표현:**
1. "쇼핑 목록 리스트를 만든다"
2. "사용자가 원하는 만큼 상품을 추가한다"
3. "필요하면 상품을 삭제할 수 있게 한다"
4. "목록을 정렬하여 보여준다"
5. "상품 개수와 통계를 출력한다"

```python
# 쇼핑 목록 관리 프로그램
print("🛒 스마트 쇼핑 목록 관리")
print("=" * 25)

shopping_list = []

while True:
    print(f"\n현재 쇼핑 목록: {shopping_list if shopping_list else '(비어있음)'}")
    print("\n1. 상품 추가")
    print("2. 상품 삭제")
    print("3. 목록 정렬")
    print("4. 통계 보기")
    print("5. 종료")
    
    choice = input("선택하세요 (1-5): ")
    
    if choice == "1":
        # 상품 추가
        item = input("추가할 상품: ")
        shopping_list.append(item)
        print(f"✅ '{item}' 추가됨!")
        
    elif choice == "2":
        # 상품 삭제
        if not shopping_list:
            print("❌ 삭제할 상품이 없습니다.")
        else:
            item = input("삭제할 상품: ")
            if item in shopping_list:
                shopping_list.remove(item)
                print(f"🗑️ '{item}' 삭제됨!")
            else:
                print(f"❌ '{item}'을 찾을 수 없습니다.")
    
    elif choice == "3":
        # 목록 정렬
        if shopping_list:
            shopping_list.sort()
            print("📋 목록이 가나다 순으로 정렬되었습니다!")
        else:
            print("❌ 정렬할 상품이 없습니다.")
    
    elif choice == "4":
        # 통계 보기
        if shopping_list:
            print(f"\n📊 쇼핑 목록 통계:")
            print(f"  총 상품 수: {len(shopping_list)}개")
            print(f"  첫 번째 상품: {shopping_list[0]}")
            print(f"  마지막 상품: {shopping_list[-1]}")
            
            # 중복 상품 체크
            unique_items = list(set(shopping_list))
            if len(unique_items) < len(shopping_list):
                print(f"  중복 상품이 있습니다!")
            else:
                print(f"  모든 상품이 다릅니다.")
        else:
            print("📊 통계를 보려면 상품을 먼저 추가하세요.")
    
    elif choice == "5":
        print("🛒 쇼핑 목록 관리를 종료합니다!")
        print(f"최종 목록: {shopping_list}")
        break
    
    else:
        print("❌ 1부터 5 사이의 숫자를 입력해주세요.")
```

---

## ☕ 휴식 시간 (10분)

---

## 🎯 2부: 딕셔너리와 세트 - 더 스마트한 데이터 관리 (40분)

### 📌 핵심 개념 1: 딕셔너리 - 키와 값의 쌍 (20분)

#### 🗝️ **딕셔너리의 기본 개념**

**딕셔너리 = 키(key)와 값(value)의 쌍으로 이루어진 데이터**

**일상생활 예시:**
```
📞 전화번호부
- "김철수": "010-1234-5678"
- "이영희": "010-2345-6789"  
- "박민수": "010-3456-7890"

📖 영한사전
- "apple": "사과"
- "banana": "바나나"
- "orange": "오렌지"
```

#### 🎯 **딕셔너리 기본 사용법**

**문제**: 학생 정보 관리 시스템 만들기

**알고리즘 말투로 표현:**
1. "학생 정보를 저장할 딕셔너리를 만든다"
2. "사용자로부터 학생 이름, 나이, 전공을 입력받는다"
3. "입력받은 정보를 딕셔너리에 저장한다"
4. "저장된 정보를 예쁘게 출력한다"
5. "특정 정보를 검색하고 수정할 수 있게 한다"

```python
# 학생 정보 관리 시스템
print("👨‍🎓 학생 정보 관리 시스템")
print("=" * 25)

# 1. 빈 딕셔너리 생성
students = {}

# 2. 사용자로부터 정보 입력받기
num_students = int(input("관리할 학생 수: "))

for i in range(num_students):
    print(f"\n{i+1}번째 학생 정보:")
    
    # 기본 정보 입력
    name = input("  이름: ")
    age = int(input("  나이: "))
    major = input("  전공: ")
    gpa = float(input("  학점 (4.0 만점): "))
    
    # 3. 딕셔너리에 저장 (이름을 키로 사용)
    students[name] = {
        "age": age,
        "major": major,
        "gpa": gpa
    }
    
    print(f"  ✅ {name} 학생 정보 저장 완료!")

# 4. 저장된 모든 학생 정보 출력
print(f"\n📋 전체 학생 정보 ({len(students)}명)")
print("=" * 40)

for student_name, student_info in students.items():
    print(f"👤 {student_name}")
    print(f"   나이: {student_info['age']}세")
    print(f"   전공: {student_info['major']}")
    print(f"   학점: {student_info['gpa']:.1f}")
    
    # 학점에 따른 등급 표시
    if student_info['gpa'] >= 3.5:
        grade_comment = "🏆 우수"
    elif student_info['gpa'] >= 3.0:
        grade_comment = "👍 양호"
    elif student_info['gpa'] >= 2.5:
        grade_comment = "📚 보통"
    else:
        grade_comment = "💪 노력 필요"
    
    print(f"   평가: {grade_comment}")
    print()

# 5. 학생 검색 기능
search_name = input("🔍 검색할 학생 이름: ")

if search_name in students:
    info = students[search_name]
    print(f"\n✅ {search_name} 학생 정보:")
    print(f"   나이: {info['age']}세")
    print(f"   전공: {info['major']}")
    print(f"   학점: {info['gpa']:.1f}")
    
    # 정보 수정 옵션
    update = input("\n정보를 수정하시겠습니까? (y/n): ")
    if update.lower() == 'y':
        new_gpa = float(input("새로운 학점: "))
        students[search_name]['gpa'] = new_gpa
        print(f"✅ {search_name} 학생의 학점이 {new_gpa:.1f}로 수정되었습니다!")
else:
    print(f"❌ '{search_name}' 학생을 찾을 수 없습니다.")

# 통계 정보
print(f"\n📊 통계 정보:")
all_gpas = [student['gpa'] for student in students.values()]
average_gpa = sum(all_gpas) / len(all_gpas)
print(f"   전체 평균 학점: {average_gpa:.2f}")
print(f"   최고 학점: {max(all_gpas):.1f}")
print(f"   최저 학점: {min(all_gpas):.1f}")
```

#### 🔧 **딕셔너리 메서드 활용**

```python
# 딕셔너리 메서드 실습
print("📚 딕셔너리 메서드 완전 정복")
print("=" * 30)

# 기본 딕셔너리
course_scores = {
    "파이썬": 95,
    "자바": 88,
    "웹개발": 92,
    "데이터베이스": 87
}

print(f"원본 딕셔너리: {course_scores}")

# 1. keys() - 모든 키 가져오기
print(f"\n📋 수강 과목들:")
for course in course_scores.keys():
    print(f"  - {course}")

# 2. values() - 모든 값 가져오기
print(f"\n📊 모든 점수들:")
all_scores = list(course_scores.values())
print(f"  점수: {all_scores}")
print(f"  평균: {sum(all_scores) / len(all_scores):.1f}점")

# 3. items() - 키-값 쌍 가져오기
print(f"\n📈 과목별 상세 점수:")
for course, score in course_scores.items():
    if score >= 90:
        level = "🏆 우수"
    elif score >= 80:
        level = "👍 양호"
    else:
        level = "📚 노력 필요"
    
    print(f"  {course}: {score}점 ({level})")

# 4. get() - 안전한 값 가져오기
print(f"\n🔍 과목 점수 조회:")
search_course = input("조회할 과목명: ")

# get() 사용 - 키가 없어도 오류 없음
score = course_scores.get(search_course, "수강하지 않음")
print(f"  {search_course}: {score}")

# 5. update() - 딕셔너리 업데이트
print(f"\n📝 새 과목 추가:")
new_courses = {
    "알고리즘": 90,
    "운영체제": 85
}
course_scores.update(new_courses)
print(f"  업데이트 후: {course_scores}")
```

### 📌 핵심 개념 2: 세트 - 중복 없는 데이터 집합 (10분)

#### 🎯 **세트의 기본 개념**

**세트 = 중복이 없고 순서가 없는 데이터 집합**

**일상생활 예시:**
```
👥 동아리 회원들
- {김철수, 이영희, 박민수} 
- 같은 사람이 두 번 들어갈 수 없음
- 순서는 중요하지 않음

🎫 콘서트 관람객들
- {좌석A01, 좌석B15, 좌석C22}
- 중복 예약 불가능
- 좌석 순서보다는 "참석 여부"가 중요
```

#### 🔧 **세트 기본 활용**

**문제**: 두 반의 학생들 중 공통으로 수강하는 학생 찾기

**알고리즘 말투로 표현:**
1. "A반 학생들의 세트를 만든다"
2. "B반 학생들의 세트를 만든다"  
3. "두 세트의 교집합을 구하여 공통 학생을 찾는다"
4. "차집합을 구하여 각 반에만 있는 학생을 찾는다"
5. "합집합을 구하여 전체 학생 수를 센다"

```python
# 두 반 학생 비교 분석
print("👥 A반과 B반 학생 분석")
print("=" * 25)

# 1. A반 학생들 (사용자 입력받기)
print("A반 학생들을 입력하세요:")
a_class_input = input("이름들을 쉼표로 구분: ")
a_class = set(a_class_input.split(", "))

print("B반 학생들을 입력하세요:")
b_class_input = input("이름들을 쉼표로 구분: ")
b_class = set(b_class_input.split(", "))

print(f"\n📋 반별 학생 현황:")
print(f"A반: {a_class}")
print(f"B반: {b_class}")
print(f"A반 인원: {len(a_class)}명")
print(f"B반 인원: {len(b_class)}명")

# 3. 교집합 - 두 반 공통 학생
common_students = a_class & b_class  # 또는 a_class.intersection(b_class)
print(f"\n🤝 두 반 공통 학생: {common_students}")
print(f"공통 학생 수: {len(common_students)}명")

# 4. 차집합 - 각 반에만 있는 학생
only_a = a_class - b_class  # A반에만 있는 학생
only_b = b_class - a_class  # B반에만 있는 학생

print(f"\n🅰️ A반에만 있는 학생: {only_a}")
print(f"🅱️ B반에만 있는 학생: {only_b}")

# 5. 합집합 - 전체 학생
all_students = a_class | b_class  # 또는 a_class.union(b_class)
print(f"\n👥 전체 학생: {all_students}")
print(f"전체 학생 수: {len(all_students)}명")

# 분석 결과
print(f"\n📊 분석 결과:")
overlap_ratio = len(common_students) / len(all_students) * 100
print(f"겹치는 학생 비율: {overlap_ratio:.1f}%")

if len(common_students) > 0:
    print("두 반에 공통으로 참여하는 학생들이 있습니다!")
else:
    print("두 반은 완전히 다른 학생들로 구성되어 있습니다.")
```

### 📌 핵심 개념 3: 자료구조 선택 가이드 (10분)

#### 🎯 **언제 어떤 자료구조를 사용할까?**

**선택 기준표:**

| 상황 | 리스트 | 딕셔너리 | 세트 |
|------|--------|----------|------|
| **순서가 중요함** | ✅ | ❌ | ❌ |
| **중복 허용** | ✅ | ❌(키만) | ❌ |
| **빠른 검색 필요** | ❌ | ✅ | ✅ |
| **키-값 쌍 저장** | ❌ | ✅ | ❌ |
| **수학적 집합 연산** | ❌ | ❌ | ✅ |

#### 📋 **실제 상황별 선택 예시**

```python
# 상황별 자료구조 선택 가이드
print("🎯 자료구조 선택 가이드")
print("=" * 25)

# 상황 1: 성적 순위 관리 (순서 중요) → 리스트
print("📊 상황 1: 시험 순위 관리")
test_scores = [95, 92, 89, 87, 85]  # 순위대로 정렬됨
print(f"1등부터 5등까지: {test_scores}")

# 상황 2: 학생 정보 관리 (빠른 검색) → 딕셔너리  
print("\n👤 상황 2: 학생 정보 데이터베이스")
student_db = {
    "20240001": {"name": "김철수", "major": "컴공"},
    "20240002": {"name": "이영희", "major": "경영"}
}
print(f"학번 20240001 검색: {student_db['20240001']}")

# 상황 3: 참석자 명단 (중복 제거) → 세트
print("\n✅ 상황 3: 이벤트 참석자 확인")
attendees = {"김철수", "이영희", "김철수", "박민수"}  # 김철수 중복 자동 제거
print(f"실제 참석자: {attendees}")

# 복합 상황: 여러 자료구조 조합
print("\n🔄 상황 4: 온라인 쇼핑몰 장바구니")
cart = {
    "items": ["노트북", "마우스", "키보드"],  # 주문 순서 중요 (리스트)
    "user_info": {"name": "김고객", "grade": "VIP"},  # 사용자 정보 (딕셔너리)
    "visited_categories": {"전자제품", "도서", "의류"}  # 방문 카테고리 (세트)
}

print("장바구니 정보:")
print(f"  주문 상품: {cart['items']}")
print(f"  고객 정보: {cart['user_info']}")
print(f"  둘러본 카테고리: {cart['visited_categories']}")
```

---

## ☕ 휴식 시간 (10분)

---

## 🎯 3부: 객체와 메서드 - 데이터와 기능의 결합 (40분)

### 📌 핵심 개념 1: 객체란 무엇인가? (15분)

#### 🎯 **객체의 기본 개념**

**객체 = 데이터(속성) + 기능(메서드)가 하나로 묶인 것**

**일상생활 예시:**
```
📱 스마트폰 (객체)
├── 속성(데이터): 화면크기, 배터리잔량, 저장공간
└── 메서드(기능): 전화걸기(), 사진찍기(), 음악재생()

🚗 자동차 (객체)  
├── 속성(데이터): 속도, 연료량, 색상
└── 메서드(기능): 시동걸기(), 가속하기(), 브레이크()

👤 사람 (객체)
├── 속성(데이터): 이름, 나이, 키
└── 메서드(기능): 걷기(), 말하기(), 생각하기()
```

#### 🔍 **파이썬에서 객체 체험하기**

**문제**: 문자열도 사실은 객체! 문자열의 속성과 메서드 탐험하기

**알고리즘 말투로 표현:**
1. "문자열 객체를 생성한다"
2. "문자열의 다양한 메서드들을 호출한다"
3. "각 메서드가 어떤 기능을 하는지 확인한다"
4. "메서드 체이닝으로 여러 기능을 연결한다"

```python
# 문자열 객체 탐험하기
print("🔤 문자열 객체의 세계")
print("=" * 25)

# 사용자로부터 문자열 입력받기
user_text = input("분석할 문자열을 입력하세요: ")

print(f"\n📝 입력된 문자열: '{user_text}'")
print(f"📏 문자열 길이: {len(user_text)}글자")

# 문자열 객체의 다양한 메서드들
print(f"\n🔧 문자열 메서드 분석:")

# 1. 대소문자 관련 메서드
print(f"대문자 변환: '{user_text.upper()}'")
print(f"소문자 변환: '{user_text.lower()}'")
print(f"첫글자만 대문자: '{user_text.capitalize()}'")
print(f"단어별 첫글자 대문자: '{user_text.title()}'")

# 2. 검사 메서드
print(f"\n🔍 문자열 특성 검사:")
print(f"모두 대문자인가? {user_text.isupper()}")
print(f"모두 소문자인가? {user_text.islower()}")
print(f"모두 숫자인가? {user_text.isdigit()}")
print(f"알파벳만 있나? {user_text.isalpha()}")

# 3. 검색과 치환 메서드
if len(user_text) > 0:
    search_char = input(f"\n🔍 '{user_text}'에서 찾을 문자: ")
    count = user_text.count(search_char)
    print(f"'{search_char}' 개수: {count}개")
    
    if count > 0:
        position = user_text.find(search_char)
        print(f"'{search_char}'의 첫 위치: {position}")
        
        # 치환해보기
        replace_char = input(f"'{search_char}'를 무엇으로 바꿀까요? ")
        replaced = user_text.replace(search_char, replace_char)
        print(f"치환 결과: '{replaced}'")

# 4. 분리와 결합 메서드
print(f"\n✂️ 문자열 분리와 결합:")
words = user_text.split()  # 공백으로 분리
print(f"단어들: {words}")
print(f"단어 개수: {len(words)}개")

if len(words) > 1:
    joined = "-".join(words)
    print(f"하이픈으로 연결: '{joined}'")
```

#### 🏗️ **리스트도 객체! 리스트 객체 탐험**

```python
# 리스트 객체 탐험하기
print("\n📋 리스트 객체의 세계")
print("=" * 25)

# 사용자로부터 숫자들 입력받기
numbers_input = input("숫자들을 쉼표로 구분해서 입력하세요: ")
numbers = [int(x.strip()) for x in numbers_input.split(",")]

print(f"입력된 숫자들: {numbers}")

# 리스트 객체의 다양한 메서드들
print(f"\n🔧 리스트 메서드 실습:")

# 1. 추가 관련 메서드
print("새 숫자 추가하기:")
new_number = int(input("추가할 숫자: "))
numbers.append(new_number)
print(f"append() 후: {numbers}")

# 2. 정렬 메서드
numbers_copy = numbers.copy()  # 원본 보존
numbers_copy.sort()
print(f"정렬된 리스트: {numbers_copy}")

numbers_copy.reverse()
print(f"역순 정렬: {numbers_copy}")

# 3. 검색과 개수 메서드
search_num = int(input("개수를 셀 숫자: "))
count = numbers.count(search_num)
print(f"'{search_num}'의 개수: {count}개")

if count > 0:
    index = numbers.index(search_num)
    print(f"'{search_num}'의 첫 위치: {index}")

# 4. 제거 메서드
if len(numbers) > 1:
    print(f"\n🗑️ 제거 기능 테스트:")
    print(f"현재 리스트: {numbers}")
    
    # 마지막 요소 제거
    removed = numbers.pop()
    print(f"pop()으로 제거된 값: {removed}")
    print(f"제거 후 리스트: {numbers}")
```

### 📌 핵심 개념 2: 메서드 체이닝과 활용 (15분)

#### 🔗 **메서드 체이닝 = 메서드를 연속으로 호출**

**문제**: 사용자 입력을 정제하고 분석하는 텍스트 처리기 만들기

**알고리즘 말투로 표현:**
1. "사용자로부터 텍스트를 입력받는다"
2. "앞뒤 공백을 제거하고, 소문자로 변환하고, 단어로 분리하는 작업을 연결한다"
3. "메서드 체이닝을 사용하여 한 줄로 처리한다"
4. "처리 결과를 분석하여 통계를 출력한다"

```python
# 텍스트 처리기 with 메서드 체이닝
print("📝 스마트 텍스트 처리기")
print("=" * 25)

# 사용자로부터 텍스트 입력받기
user_input = input("분석할 텍스트를 입력하세요: ")

print(f"원본 텍스트: '{user_input}'")

# 메서드 체이닝으로 텍스트 정제
# 1단계씩 나누어서 설명
print(f"\n🔧 단계별 텍스트 처리:")

step1 = user_input.strip()  # 앞뒤 공백 제거
print(f"1단계 (공백제거): '{step1}'")

step2 = step1.lower()  # 소문자 변환
print(f"2단계 (소문자): '{step2}'")

step3 = step2.replace(",", "").replace(".", "").replace("!", "").replace("?", "")  # 구두점 제거
print(f"3단계 (구두점제거): '{step3}'")

step4 = step3.split()  # 단어로 분리
print(f"4단계 (단어분리): {step4}")

# 위의 모든 과정을 메서드 체이닝으로 한 번에!
processed_words = (user_input
                  .strip()
                  .lower()
                  .replace(",", "")
                  .replace(".", "")
                  .replace("!", "")
                  .replace("?", "")
                  .split())

print(f"\n⚡ 메서드 체이닝 결과: {processed_words}")

# 처리된 데이터 분석
print(f"\n📊 텍스트 분석 결과:")
print(f"총 단어 수: {len(processed_words)}개")

# 각 단어의 길이 분석
word_lengths = [len(word) for word in processed_words]
print(f"단어 길이들: {word_lengths}")
print(f"평균 단어 길이: {sum(word_lengths) / len(word_lengths):.1f}글자")

# 가장 긴 단어와 짧은 단어
if processed_words:
    longest_word = max(processed_words, key=len)
    shortest_word = min(processed_words, key=len)
    print(f"가장 긴 단어: '{longest_word}' ({len(longest_word)}글자)")
    print(f"가장 짧은 단어: '{shortest_word}' ({len(shortest_word)}글자)")

# 중복 단어 제거 및 개수
unique_words = list(set(processed_words))
print(f"고유 단어 수: {len(unique_words)}개")
print(f"중복 단어가 있나요? {'예' if len(unique_words) < len(processed_words) else '아니오'}")
```

#### 🎨 **고급 메서드 체이닝 실습**

```python
# 숫자 리스트 고급 처리
print("\n🔢 숫자 리스트 고급 처리")
print("=" * 25)

# 사용자로부터 숫자 문자열 입력받기
numbers_input = input("숫자들을 공백으로 구분해서 입력하세요: ")

# 메서드 체이닝으로 숫자 리스트 생성 및 처리
try:
    # 1. 문자열 → 리스트 변환 및 정렬을 한 번에
    numbers = (numbers_input
              .strip()                    # 공백 제거
              .split())                   # 단어로 분리
    
    # 2. 문자열을 숫자로 변환
    numbers = [int(x) for x in numbers]
    
    print(f"입력된 숫자들: {numbers}")
    
    # 3. 다양한 리스트 처리
    original = numbers.copy()
    
    # 정렬된 버전
    sorted_numbers = sorted(numbers)
    print(f"정렬된 리스트: {sorted_numbers}")
    
    # 역순 정렬
    reverse_sorted = sorted(numbers, reverse=True)
    print(f"역순 정렬: {reverse_sorted}")
    
    # 짝수만 필터링
    even_numbers = [x for x in numbers if x % 2 == 0]
    print(f"짝수만: {even_numbers}")
    
    # 홀수만 필터링
    odd_numbers = [x for x in numbers if x % 2 == 1]
    print(f"홀수만: {odd_numbers}")
    
    # 통계 출력
    print(f"\n📊 통계:")
    print(f"총 개수: {len(numbers)}개")
    print(f"합계: {sum(numbers)}")
    print(f"평균: {sum(numbers) / len(numbers):.1f}")
    print(f"최댓값: {max(numbers)}")
    print(f"최솟값: {min(numbers)}")
    
except ValueError:
    print("❌ 올바른 숫자들을 입력해주세요!")
```

### 📌 핵심 개념 3: 내장 함수와 메서드 활용 (10분)

#### 🛠️ **자주 사용하는 내장 함수들**

```python
# 내장 함수 완전 활용 가이드
print("🛠️ 파이썬 내장 함수 마스터")
print("=" * 30)

# 사용자로부터 숫자들 입력받기
print("다양한 숫자들을 입력해주세요:")
data_input = input("숫자들 (쉼표로 구분): ")
numbers = [int(x.strip()) for x in data_input.split(",")]

print(f"입력된 숫자들: {numbers}")

# 1. 수학적 내장 함수들
print(f"\n🧮 수학적 함수들:")
print(f"len(numbers): {len(numbers)} - 개수")
print(f"sum(numbers): {sum(numbers)} - 합계")
print(f"max(numbers): {max(numbers)} - 최댓값")
print(f"min(numbers): {min(numbers)} - 최솟값")
print(f"sorted(numbers): {sorted(numbers)} - 정렬")

# 2. 타입 변환 함수들
print(f"\n🔄 타입 변환 함수들:")
sample_number = numbers[0]
print(f"int(3.14): {int(3.14)} - 실수를 정수로")
print(f"float({sample_number}): {float(sample_number)} - 정수를 실수로")
print(f"str({sample_number}): '{str(sample_number)}' - 숫자를 문자열로")
print(f"list(range(5)): {list(range(5))} - range를 리스트로")

# 3. 검사 함수들
print(f"\n🔍 검사 함수들:")
test_values = [42, 3.14, "hello", [1, 2, 3], {"key": "value"}]

for value in test_values:
    print(f"type({value}): {type(value).__name__}")

# 4. 순회 관련 함수들
print(f"\n🔄 순회 함수들:")
names = ["김철수", "이영희", "박민수"]
scores = [85, 92, 78]

print("enumerate() 사용:")
for index, name in enumerate(names):
    print(f"  {index+1}번째: {name}")

print("\nzip() 사용:")
for name, score in zip(names, scores):
    print(f"  {name}: {score}점")

# 5. 필터링 함수들
print(f"\n🎯 필터링 함수들:")
mixed_data = [1, 2, 0, -1, 5, None, "", "hello", [], [1, 2]]

# filter() 함수로 참인 값만 걸러내기
true_values = list(filter(bool, mixed_data))
print(f"참인 값들: {true_values}")

# any()와 all() 함수
print(f"any([True, False, True]): {any([True, False, True])} - 하나라도 참이면 True")
print(f"all([True, True, True]): {all([True, True, True])} - 모두 참이면 True")
print(f"all([True, False, True]): {all([True, False, True])} - 모두 참이어야 True")

# 실용적 활용 예시
print(f"\n💡 실용적 활용:")
scores = [85, 92, 78, 96, 88]

# 모든 학생이 60점 이상인가?
all_passed = all(score >= 60 for score in scores)
print(f"모든 학생이 합격점인가? {all_passed}")

# 90점 이상인 학생이 있는가?
has_excellent = any(score >= 90 for score in scores)
print(f"우수한 학생이 있는가? {has_excellent}")

# 80점 이상인 학생들만 필터링
good_scores = list(filter(lambda x: x >= 80, scores))
print(f"80점 이상 점수들: {good_scores}")
```

---

## 🎯 실습 시간 (60분)

### 🎯 실습 과제 1: 학생 성적 관리 시스템 (20분)

#### 📋 **과제 요구사항**

**알고리즘 말투로 표현:**
1. "사용자로부터 학생 수를 입력받는다"
2. "각 학생의 이름과 3과목 점수를 입력받는다"
3. "학생별로 평균을 계산하고 등급을 매긴다"
4. "모든 정보를 딕셔너리에 저장한다"
5. "전체 학생 정보를 보기 좋게 출력한다"
6. "반 전체 통계를 계산하여 출력한다"
7. "특정 학생을 검색하여 상세 정보를 보여준다"

**구체적 요구사항:**
- 딕셔너리를 활용한 학생 데이터 관리
- 리스트를 활용한 점수 저장
- 내장 함수를 활용한 통계 계산
- 등급 판정: A(90이상), B(80이상), C(70이상), D(60이상), F(60미만)

### 🎯 실습 과제 2: 단어 빈도수 카운터 (20분)

#### 📋 **과제 요구사항**

**알고리즘 말투로 표현:**
1. "사용자로부터 긴 텍스트를 입력받는다"
2. "텍스트를 정제한다(소문자 변환, 구두점 제거, 공백 분리)"
3. "딕셔너리를 사용하여 각 단어의 출현 빈도를 센다"
4. "빈도수가 높은 순서로 정렬한다"
5. "상위 5개 단어와 빈도수를 출력한다"
6. "전체 단어 수와 고유 단어 수를 계산한다"
7. "특정 단어의 빈도수를 검색할 수 있게 한다"

**구체적 요구사항:**
- 문자열 메서드를 활용한 텍스트 정제
- 딕셔너리를 활용한 빈도수 계산
- 정렬 함수를 활용한 순위 매기기
- 사용자 검색 기능 구현

### 🎯 실습 과제 3: 친구 관계 네트워크 분석 (20분)

#### 📋 **과제 요구사항**

**알고리즘 말투로 표현:**
1. "여러 명의 친구 그룹 정보를 입력받는다"
2. "각 그룹을 세트로 저장한다"
3. "두 그룹 간의 공통 친구를 찾는다(교집합)"
4. "각 그룹에만 있는 친구를 찾는다(차집합)"
5. "전체 친구 네트워크를 파악한다(합집합)"
6. "가장 많은 그룹에 속한 인기 친구를 찾는다"
7. "친구 관계 통계를 출력한다"

**구체적 요구사항:**
- 세트를 활용한 그룹 관리
- 세트 연산(교집합, 차집합, 합집합) 활용
- 딕셔너리를 활용한 친구별 소속 그룹 수 계산
- 통계 분석 및 결과 출력

---

## 📚 실습 과제 모범답안

### 🎯 과제 1 모범답안: 학생 성적 관리 시스템

```python
#!/usr/bin/env python3
"""
학생 성적 관리 시스템
- 딕셔너리와 리스트를 활용한 체계적인 데이터 관리
- 내장 함수를 활용한 효율적인 통계 계산
- 사용자 친화적인 인터페이스 제공
"""

def get_grade(average):
    """평균 점수를 받아 등급을 반환하는 함수"""
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

def display_student_info(name, student_data):
    """개별 학생 정보를 보기 좋게 출력하는 함수"""
    scores = student_data["scores"]
    average = student_data["average"]
    grade = student_data["grade"]
    
    print(f"👤 {name}")
    print(f"   국어: {scores[0]:3d}점")
    print(f"   영어: {scores[1]:3d}점")  
    print(f"   수학: {scores[2]:3d}점")
    print(f"   평균: {average:5.1f}점")
    print(f"   등급: {grade}")
    
    # 과목별 우수/부족 표시
    subjects = ["국어", "영어", "수학"]
    for i, subject in enumerate(subjects):
        if scores[i] >= 90:
            status = "🏆 우수"
        elif scores[i] >= 80:
            status = "👍 양호"
        elif scores[i] < 60:
            status = "📚 보완필요"
        else:
            status = "📝 보통"
        print(f"   {subject} 평가: {status}")

# 메인 프로그램 시작
print("📊 학생 성적 관리 시스템")
print("=" * 40)

# 1. 학생 수 입력받기
while True:
    try:
        student_count = int(input("관리할 학생 수를 입력하세요: "))
        if student_count > 0:
            break
        else:
            print("1명 이상 입력해주세요.")
    except ValueError:
        print("올바른 숫자를 입력해주세요.")

# 2. 학생 정보 저장용 딕셔너리
students = {}

# 3. 각 학생의 정보 입력받기
for i in range(student_count):
    print(f"\n📝 {i+1}번째 학생 정보 입력:")
    
    # 이름 입력
    name = input("  이름: ").strip()
    
    # 3과목 점수 입력
    subjects = ["국어", "영어", "수학"]
    scores = []
    
    for subject in subjects:
        while True:
            try:
                score = int(input(f"  {subject} 점수 (0-100): "))
                if 0 <= score <= 100:
                    scores.append(score)
                    break
                else:
                    print("    0부터 100 사이의 점수를 입력해주세요.")
            except ValueError:
                print("    올바른 숫자를 입력해주세요.")
    
    # 평균 계산
    average = sum(scores) / len(scores)
    
    # 등급 계산
    grade = get_grade(average)
    
    # 딕셔너리에 저장
    students[name] = {
        "scores": scores,
        "average": average,
        "grade": grade
    }
    
    print(f"  ✅ {name} 학생 정보 저장 완료!")

# 4. 전체 학생 정보 출력
print(f"\n{'='*50}")
print(f"📋 전체 학생 성적표 ({len(students)}명)")
print(f"{'='*50}")

for name, student_data in students.items():
    display_student_info(name, student_data)
    print()

# 5. 반 전체 통계 계산
all_averages = [student["average"] for student in students.values()]
all_scores = []
for student in students.values():
    all_scores.extend(student["scores"])

class_average = sum(all_averages) / len(all_averages)
highest_student = max(students.items(), key=lambda x: x[1]["average"])
lowest_student = min(students.items(), key=lambda x: x[1]["average"])

# 등급별 분포
grade_counts = {"A": 0, "B": 0, "C": 0, "D": 0, "F": 0}
for student in students.values():
    grade_counts[student["grade"]] += 1

print(f"📊 반 전체 통계")
print("=" * 30)
print(f"학급 평균: {class_average:.1f}점")
print(f"전체 최고점: {max(all_scores)}점")
print(f"전체 최저점: {min(all_scores)}점")
print(f"1등: {highest_student[0]} ({highest_student[1]['average']:.1f}점)")
print(f"꼴등: {lowest_student[0]} ({lowest_student[1]['average']:.1f}점)")

print(f"\n🏆 등급별 분포:")
for grade in ["A", "B", "C", "D", "F"]:
    count = grade_counts[grade]
    percentage = (count / len(students)) * 100
    print(f"  {grade}등급: {count}명 ({percentage:.1f}%)")

# 6. 학생 검색 기능
while True:
    print(f"\n🔍 학생 검색 (종료하려면 'quit' 입력)")
    search_name = input("검색할 학생 이름: ").strip()
    
    if search_name.lower() == 'quit':
        break
    
    if search_name in students:
        print(f"\n✅ {search_name} 학생 상세 정보:")
        print("-" * 30)
        display_student_info(search_name, students[search_name])
        
        # 반에서의 순위 계산
        sorted_students = sorted(students.items(), key=lambda x: x[1]["average"], reverse=True)
        rank = next(i for i, (name, _) in enumerate(sorted_students, 1) if name == search_name)
        print(f"   반 순위: {rank}등/{len(students)}명")
        
    else:
        print(f"❌ '{search_name}' 학생을 찾을 수 없습니다.")
        print(f"등록된 학생: {', '.join(students.keys())}")

print("\n📊 성적 관리 시스템을 종료합니다!")
```

### 🎯 과제 2 모범답안: 단어 빈도수 카운터

```python
#!/usr/bin/env python3
"""
단어 빈도수 카운터
- 텍스트 정제 및 분석
- 딕셔너리를 활용한 빈도수 계산
- 정렬과 검색 기능 제공
"""

import string

def clean_text(text):
    """텍스트를 정제하는 함수 (메서드 체이닝 활용)"""
    # 소문자 변환 및 구두점 제거
    cleaned = (text
              .lower()
              .translate(str.maketrans('', '', string.punctuation))
              .strip())
    return cleaned

def count_word_frequency(words):
    """단어 리스트를 받아 빈도수 딕셔너리를 반환"""
    frequency = {}
    for word in words:
        if word:  # 빈 문자열 제외
            frequency[word] = frequency.get(word, 0) + 1
    return frequency

def display_top_words(frequency_dict, top_n=5):
    """상위 N개 단어를 출력"""
    # 빈도수가 높은 순으로 정렬
    sorted_words = sorted(frequency_dict.items(), key=lambda x: x[1], reverse=True)
    
    print(f"\n🏆 상위 {top_n}개 단어:")
    print("-" * 30)
    
    for i, (word, count) in enumerate(sorted_words[:top_n], 1):
        percentage = (count / sum(frequency_dict.values())) * 100
        print(f"{i:2d}. {word:<15} : {count:3d}회 ({percentage:4.1f}%)")
    
    return sorted_words

# 메인 프로그램
print("📝 단어 빈도수 분석기")
print("=" * 30)

# 1. 사용자로부터 텍스트 입력받기
print("분석할 텍스트를 입력하세요:")
print("(여러 줄 입력 가능, 빈 줄을 입력하면 종료)")

lines = []
while True:
    line = input()
    if line.strip() == "":
        break
    lines.append(line)

if not lines:
    text = input("한 줄로 텍스트를 입력하세요: ")
else:
    text = " ".join(lines)

print(f"\n📖 입력된 텍스트:")
print(f"'{text[:100]}{'...' if len(text) > 100 else ''}'")

# 2. 텍스트 정제
cleaned_text = clean_text(text)
words = cleaned_text.split()

print(f"\n🔧 텍스트 정제 완료:")
print(f"원본 길이: {len(text)}자")
print(f"정제 후 길이: {len(cleaned_text)}자")
print(f"추출된 단어 수: {len(words)}개")

if not words:
    print("❌ 분석할 단어가 없습니다.")
    exit()

# 3. 단어 빈도수 계산
word_frequency = count_word_frequency(words)

# 4. 기본 통계 출력
unique_words = len(word_frequency)
total_words = len(words)

print(f"\n📊 기본 통계:")
print(f"총 단어 수: {total_words}개")
print(f"고유 단어 수: {unique_words}개") 
print(f"중복률: {((total_words - unique_words) / total_words * 100):.1f}%")

# 5. 상위 단어들 출력
sorted_words = display_top_words(word_frequency, 10)

# 6. 단어 길이 분석
word_lengths = [len(word) for word in word_frequency.keys()]
print(f"\n📏 단어 길이 분석:")
print(f"평균 단어 길이: {sum(word_lengths) / len(word_lengths):.1f}글자")
print(f"가장 긴 단어: '{max(word_frequency.keys(), key=len)}' ({max(word_lengths)}글자)")
print(f"가장 짧은 단어: '{min(word_frequency.keys(), key=len)}' ({min(word_lengths)}글자)")

# 7. 빈도수별 분포
frequency_distribution = {}
for count in word_frequency.values():
    frequency_distribution[count] = frequency_distribution.get(count, 0) + 1

print(f"\n📈 빈도수 분포:")
for freq in sorted(frequency_distribution.keys(), reverse=True)[:5]:
    count = frequency_distribution[freq]
    print(f"  {freq}번 나타난 단어: {count}개")

# 8. 단어 검색 기능
print(f"\n🔍 단어 검색 기능")
print("(종료하려면 'quit' 입력)")

while True:
    search_word = input("\n검색할 단어: ").strip().lower()
    
    if search_word == 'quit':
        break
    
    if search_word in word_frequency:
        count = word_frequency[search_word]
        percentage = (count / total_words) * 100
        
        # 순위 찾기
        rank = next(i for i, (word, _) in enumerate(sorted_words, 1) 
                   if word == search_word)
        
        print(f"✅ '{search_word}' 분석 결과:")
        print(f"   출현 횟수: {count}회")
        print(f"   전체 비율: {percentage:.2f}%")
        print(f"   빈도 순위: {rank}위/{unique_words}개")
        
        # 비슷한 빈도의 다른 단어들
        similar_words = [word for word, freq in word_frequency.items() 
                        if freq == count and word != search_word]
        if similar_words:
            print(f"   같은 빈도 단어: {', '.join(similar_words[:3])}")
            
    else:
        print(f"❌ '{search_word}'를 찾을 수 없습니다.")
        
        # 유사한 단어 제안
        suggestions = [word for word in word_frequency.keys() 
                      if search_word in word or word in search_word]
        if suggestions:
            print(f"💡 혹시 이런 단어를 찾으셨나요? {', '.join(suggestions[:3])}")

print("\n📝 단어 빈도수 분석을 완료했습니다!")

# 9. 분석 결과 요약
print(f"\n📋 분석 결과 요약:")
print(f"가장 자주 사용된 단어: '{sorted_words[0][0]}' ({sorted_words[0][1]}회)")
print(f"어휘 다양성 지수: {unique_words/total_words:.3f}")
print(f"텍스트 복잡도: {'높음' if unique_words/total_words > 0.7 else '보통' if unique_words/total_words > 0.5 else '낮음'}")
```

### 🎯 과제 3 모범답안: 친구 관계 네트워크 분석

```python
#!/usr/bin/env python3
"""
친구 관계 네트워크 분석
- 세트를 활용한 그룹 관리
- 집합 연산을 통한 관계 분석
- 네트워크 통계 및 인기도 분석
"""

def get_group_input(group_name):
    """그룹 정보를 입력받아 세트로 반환"""
    print(f"\n👥 {group_name} 멤버들을 입력하세요:")
    members_input = input("이름들을 쉼표로 구분: ").strip()
    
    if not members_input:
        return set()
    
    # 쉼표로 분리하고 공백 제거 후 세트로 변환
    members = set(name.strip() for name in members_input.split(",") if name.strip())
    return members

def analyze_groups(groups):
    """그룹들을 분석하여 통계 정보 반환"""
    # 모든 친구들의 합집합
    all_friends = set()
    for group in groups.values():
        all_friends = all_friends.union(group)
    
    # 각 친구가 속한 그룹 수 계산
    friend_group_count = {}
    for friend in all_friends:
        count = sum(1 for group in groups.values() if friend in group)
        friend_group_count[friend] = count
    
    return all_friends, friend_group_count

def find_popular_friends(friend_group_count, top_n=3):
    """가장 인기 있는 친구들 찾기"""
    sorted_friends = sorted(friend_group_count.items(), 
                           key=lambda x: x[1], reverse=True)
    return sorted_friends[:top_n]

def compare_two_groups(group1, group2, name1, name2):
    """두 그룹을 비교 분석"""
    print(f"\n🔍 {name1} vs {name2} 비교 분석:")
    print("-" * 40)
    
    # 교집합 (공통 친구들)
    common_friends = group1 & group2
    print(f"🤝 공통 친구들: {common_friends if common_friends else '없음'}")
    print(f"    공통 친구 수: {len(common_friends)}명")
    
    # 차집합 (각 그룹에만 있는 친구들)
    only_group1 = group1 - group2
    only_group2 = group2 - group1
    
    print(f"\n👥 {name1}에만 있는 친구들: {only_group1 if only_group1 else '없음'}")
    print(f"👥 {name2}에만 있는 친구들: {only_group2 if only_group2 else '없음'}")
    
    # 합집합 (두 그룹 전체 친구들)
    all_friends = group1 | group2
    print(f"\n🌐 두 그룹 전체 친구들: {len(all_friends)}명")
    
    # 유사도 계산 (Jaccard 계수)
    if len(all_friends) > 0:
        similarity = len(common_friends) / len(all_friends)
        print(f"📊 그룹 유사도: {similarity:.2%}")
    
    return common_friends, only_group1, only_group2, all_friends

# 메인 프로그램
print("👥 친구 관계 네트워크 분석기")
print("=" * 35)

# 1. 그룹 수 입력받기
while True:
    try:
        group_count = int(input("분석할 친구 그룹 수 (2-5개): "))
        if 2 <= group_count <= 5:
            break
        else:
            print("2개부터 5개 사이로 입력해주세요.")
    except ValueError:
        print("올바른 숫자를 입력해주세요.")

# 2. 각 그룹 정보 입력받기
groups = {}
group_names = []

for i in range(group_count):
    group_name = input(f"\n{i+1}번째 그룹 이름: ").strip()
    if not group_name:
        group_name = f"그룹{i+1}"
    
    group_names.append(group_name)
    members = get_group_input(group_name)
    
    if len(members) > 0:
        groups[group_name] = members
        print(f"✅ {group_name}: {len(members)}명 ({', '.join(sorted(members))})")
    else:
        print(f"⚠️ {group_name}에 멤버가 없습니다.")

if not groups:
    print("❌ 분석할 그룹이 없습니다.")
    exit()

# 3. 전체 네트워크 분석
print(f"\n{'='*50}")
print(f"📊 친구 네트워크 전체 분석")
print(f"{'='*50}")

all_friends, friend_group_count = analyze_groups(groups)

print(f"총 그룹 수: {len(groups)}개")
print(f"전체 친구 수: {len(all_friends)}명")
print(f"평균 그룹 크기: {sum(len(group) for group in groups.values()) / len(groups):.1f}명")

# 4. 각 그룹 상세 정보
print(f"\n📋 그룹별 상세 정보:")
for group_name, members in groups.items():
    print(f"\n👥 {group_name}:")
    print(f"   멤버 수: {len(members)}명")
    print(f"   멤버들: {', '.join(sorted(members))}")
    
    # 이 그룹에서만 볼 수 있는 친구들
    unique_friends = members.copy()
    for other_name, other_group in groups.items():
        if other_name != group_name:
            unique_friends -= other_group
    
    if unique_friends:
        print(f"   독점 친구: {', '.join(unique_friends)}")
    else:
        print(f"   독점 친구: 없음 (모든 멤버가 다른 그룹과 겹침)")

# 5. 인기 친구 순위
print(f"\n🏆 친구 인기 순위:")
print("-" * 25)

popular_friends = find_popular_friends(friend_group_count, min(10, len(all_friends)))

for rank, (friend, group_count) in enumerate(popular_friends, 1):
    percentage = (group_count / len(groups)) * 100
    
    # 소속 그룹들 찾기
    belonging_groups = [name for name, group in groups.items() if friend in group]
    
    print(f"{rank:2d}. {friend:<12} : {group_count}개 그룹 ({percentage:4.1f}%)")
    print(f"     소속: {', '.join(belonging_groups)}")

# 6. 그룹 간 관계 분석
if len(groups) >= 2:
    print(f"\n🔍 그룹 간 관계 분석:")
    
    group_list = list(groups.items())
    
    # 모든 그룹 쌍 비교
    for i in range(len(group_list)):
        for j in range(i + 1, len(group_list)):
            name1, group1 = group_list[i]
            name2, group2 = group_list[j]
            
            common, only1, only2, all_both = compare_two_groups(
                group1, group2, name1, name2)

# 7. 네트워크 통계
print(f"\n📈 네트워크 통계:")
print("-" * 20)

# 그룹 크기 분포
group_sizes = [len(group) for group in groups.values()]
print(f"가장 큰 그룹: {max(group_sizes)}명")
print(f"가장 작은 그룹: {min(group_sizes)}명")
print(f"그룹 크기 편차: {max(group_sizes) - min(group_sizes)}명")

# 친구별 참여도 분포
participation_counts = list(friend_group_count.values())
max_participation = max(participation_counts)
min_participation = min(participation_counts)

print(f"\n👥 친구별 참여도:")
print(f"최대 참여 그룹 수: {max_participation}개")
print(f"최소 참여 그룹 수: {min_participation}개")

# 참여도별 친구 수
participation_distribution = {}
for count in participation_counts:
    participation_distribution[count] = participation_distribution.get(count, 0) + 1

for participation in sorted(participation_distribution.keys(), reverse=True):
    friend_count = participation_distribution[participation]
    print(f"  {participation}개 그룹 참여: {friend_count}명")

# 8. 클러스터 분석 (그룹 간 유사도)
if len(groups) >= 2:
    print(f"\n🔗 그룹 클러스터 분석:")
    
    similarities = []
    group_list = list(groups.items())
    
    for i in range(len(group_list)):
        for j in range(i + 1, len(group_list)):
            name1, group1 = group_list[i]
            name2, group2 = group_list[j]
            
            common = len(group1 & group2)
            total = len(group1 | group2)
            similarity = common / total if total > 0 else 0
            
            similarities.append((name1, name2, similarity))
    
    # 유사도가 높은 순으로 정렬
    similarities.sort(key=lambda x: x[2], reverse=True)
    
    print("그룹 간 유사도 순위:")
    for i, (group1, group2, sim) in enumerate(similarities[:3], 1):
        print(f"  {i}. {group1} ↔ {group2}: {sim:.1%}")

# 9. 추천 시스템
print(f"\n💡 친구 추천:")
print("-" * 15)

# 각 그룹에 추천할 수 있는 친구들
for group_name, group_members in groups.items():
    # 이 그룹에 없지만 다른 그룹에 있는 친구들
    potential_friends = all_friends - group_members
    
    if potential_friends:
        # 다른 그룹과의 연결이 많은 친구 우선 추천
        recommendations = []
        for friend in potential_friends:
            connections = sum(1 for other_group in groups.values() 
                            if friend in other_group and len(other_group & group_members) > 0)
            if connections > 0:
                recommendations.append((friend, connections))
        
        recommendations.sort(key=lambda x: x[1], reverse=True)
        
        if recommendations:
            print(f"\n{group_name}에게 추천하는 친구:")
            for friend, connections in recommendations[:3]:
                print(f"  - {friend} (공통 연결: {connections}개)")

print(f"\n🎉 친구 관계 네트워크 분석 완료!")
```

---

## 📚 오늘 배운 내용 정리

### ✅ 핵심 포인트

1. **자료구조의 필요성**:
   - 단순한 변수의 한계를 극복
   - 관련된 데이터를 체계적으로 관리
   - 코드의 효율성과 가독성 향상

2. **리스트 완전 정복**:
   - 순서가 있는 데이터 모음
   - 인덱싱, 슬라이싱, 다양한 메서드 활용
   - 반복문과의 완벽한 조합

3. **딕셔너리 활용**:
   - 키-값 쌍으로 데이터 저장
   - 빠른 검색과 데이터 접근
   - 실제 데이터베이스와 유사한 구조

4. **세트의 활용**:
   - 중복 제거와 집합 연산
   - 교집합, 합집합, 차집합 활용
   - 네트워크 분석과 관계 파악

5. **객체와 메서드**:
   - 데이터와 기능이 결합된 객체 개념
   - 메서드 체이닝으로 효율적인 처리
   - 내장 함수와 메서드의 적절한 활용

### 🏠 다음 주까지 해볼 과제

1. **자료구조 기초 연습**:
   - 일상생활의 데이터를 리스트, 딕셔너리, 세트로 정리해보기
   - 각 자료구조의 장단점을 실제로 체험해보기

2. **메서드 활용 연습**:
   - 문자열과 리스트의 다양한 메서드들 실험해보기
   - 메서드 체이닝으로 복잡한 작업을 간단하게 표현해보기

3. **실습 과제 확장**:
   - 오늘의 실습 과제에 더 많은 기능 추가하기
   - 사용자 인터페이스와 에러 처리 개선하기

4. **조합 활용 연습**:
   - 여러 자료구조를 조합하여 복잡한 데이터 구조 만들어보기
   - 실제 프로젝트에 적용 가능한 예시 구상하기

### 🔮 다음 주 예고

**7주차: 함수 정의와 문서화**
- 함수 설계의 원칙과 방법론
- 매개변수와 반환값의 고급 활용
- Docstring을 활용한 전문적인 문서화
- 함수의 책임 분리와 모듈화 설계

### 💡 마지막 정리

**지금까지의 성장 과정:**
```
1주차: "프로그래밍이 뭔지 알았다!"
2주차: "어디서든 코딩할 수 있게 되었다!"
3주차: "변수로 복잡한 문제를 해결할 수 있다!"
4주차: "조건문으로 똑똑한 프로그램을 만들 수 있다!"
5주차: "반복문으로 효율적인 프로그램을 만들 수 있다!"
6주차: "자료구조로 체계적인 데이터 관리를 할 수 있다!"
```

**오늘 여러분이 할 수 있게 된 것들:**
- 📊 많은 데이터를 체계적으로 정리하고 관리하기
- 🔍 빠른 검색과 효율적인 데이터 접근하기
- 🤝 관련된 데이터들을 하나로 묶어 처리하기
- 🔗 복잡한 관계를 분석하고 패턴 찾기
- ⚡ 메서드 체이닝으로 간결하고 우아한 코드 작성하기

**프로그래밍의 진정한 파워:**
오늘 배운 자료구조는 프로그래밍의 진정한 힘을 보여줍니다. 단순히 계산만 하는 것이 아니라, 복잡한 현실 세계의 데이터를 컴퓨터 안에서 체계적으로 모델링하고 관리할 수 있게 되었어요!

**실무에서의 중요성:**
```python
# 실제 서비스에서는 이런 복잡한 데이터 구조들이 사용됩니다
user_data = {
    "profile": {"name": "김사용자", "age": 25},
    "orders": [
        {"product": "노트북", "price": 1200000, "date": "2024-03-15"},
        {"product": "마우스", "price": 35000, "date": "2024-03-20"}
    ],
    "interests": {"전자제품", "도서", "스포츠"},
    "friends": {"이친구", "박친구", "최친구"}
}
```

이제 여러분도 이런 복잡한 데이터를 자유자재로 다룰 수 있습니다!

**마지막 격려:**
자료구조를 마스터한다는 것은 데이터의 바다에서 원하는 정보를 빠르고 정확하게 찾아낼 수 있는 능력을 갖춘 것입니다. 현대의 모든 소프트웨어는 자료구조 위에 구축되어 있어요!

여러분은 이제 진짜 개발자의 첫 번째 관문을 통과했습니다! 🌟

다음 주에는 함수를 통해 코드를 더욱 체계적이고 재사용 가능하게 만드는 방법을 배워봅시다! 💪

---

**🎯 6주차 학습 완료! 수고하셨습니다! 🎉**