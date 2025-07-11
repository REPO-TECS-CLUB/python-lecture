# 9주차: 모듈, 패키지 및 파일 관리
**총 강의시간: 3시간 20분 (200분)**
- 강의: 120분 (3부로 구성)
- 휴식: 20분 (10분씩 2회)
- 실습: 60분

---

## 🛠️ 개발환경 준비: Docker + VSCode로 모듈 개발하기 (20분)

### 📌 환경 설정의 중요성

**모듈과 패키지 학습을 위해서는 반드시 폴더 구조와 여러 파일을 관리할 수 있는 환경이 필요합니다!**

- ❌ **Colab의 한계**: 단일 노트북 파일만 지원, 복잡한 폴더 구조 관리 어려움
- ✅ **Docker + VSCode 환경**: 실제 개발 환경과 동일한 폴더/파일 구조 관리 가능

### 🐳 **단계별 Docker + VSCode 환경 구축**

#### **1단계: Docker 컨테이너 생성 및 실행**

```bash
# 파이썬 개발용 Docker 컨테이너 실행
docker run -it --name python-dev \
  -p 2222:22 \
  -v $(pwd)/python_projects:/workspace \
  python:3.11 /bin/bash

# 컨테이너 내부에서 필요한 패키지 설치
apt update
apt install -y openssh-server nano vim git

# SSH 서버 설정
echo 'root:password123' | chpasswd
echo 'PermitRootLogin yes' >> /etc/ssh/sshd_config
echo 'PasswordAuthentication yes' >> /etc/ssh/sshd_config
service ssh start

# 작업 디렉토리로 이동
cd /workspace
```

#### **2단계: VSCode에서 Remote-SSH 연결**

**VSCode 확장 프로그램 설치:**
1. VSCode 실행
2. 확장 프로그램 탭에서 "Remote - SSH" 검색 및 설치
3. "Remote Development" 패키지도 함께 설치

**SSH 연결 설정:**
1. `Ctrl+Shift+P` → "Remote-SSH: Connect to Host" 선택
2. "Add New SSH Host" 선택
3. SSH 연결 정보 입력: `ssh root@localhost -p 2222`
4. 설정 파일 저장 위치 선택 (기본값 선택)
5. 연결 시도 → 비밀번호 입력: `password123`

#### **3단계: 작업 폴더 열기**

```bash
# VSCode에서 터미널 열기 (Ctrl+`)
# 프로젝트 루트 폴더 생성
mkdir -p /workspace/week9_projects
cd /workspace/week9_projects

# 오늘 실습할 프로젝트 폴더들 미리 생성
mkdir -p game_character_system
mkdir -p online_bookstore
mkdir -p diary_system
mkdir -p library_system

# 현재 디렉토리 확인
pwd
ls -la
```

**VSCode에서 폴더 열기:**
1. `File` → `Open Folder`
2. `/workspace/week9_projects` 선택
3. "Trust the authors" 클릭

#### **4단계: 첫 번째 모듈 프로젝트 구조 만들기**

**VSCode의 파일 탐색기에서 폴더와 파일 생성:**

```
game_character_system/
├── character_stats.py
├── character_actions.py
└── main_game.py
```

**VSCode에서 폴더 및 파일 생성 방법:**
1. 좌측 파일 탐색기에서 `game_character_system` 폴더 선택
2. 우클릭 → "New File"
3. 파일명 입력 (예: `character_stats.py`)
4. 파일 내용 작성 후 `Ctrl+S`로 저장

#### **5단계: 터미널에서 Python 실행 테스트**

```bash
# VSCode 터미널에서 Python 실행 테스트
cd /workspace/week9_projects/game_character_system

# Python 파일 실행
python main_game.py

# 또는 대화형 Python으로 모듈 테스트
python
>>> import character_stats
>>> import character_actions
>>> exit()
```

#### **6단계: 패키지 구조 만들기 실습**

```bash
# 복잡한 패키지 구조 생성
mkdir -p online_bookstore/{books,users,orders,utils}

# __init__.py 파일들 생성
touch online_bookstore/__init__.py
touch online_bookstore/books/__init__.py
touch online_bookstore/users/__init__.py
touch online_bookstore/orders/__init__.py
touch online_bookstore/utils/__init__.py

# 최종 구조 확인
tree online_bookstore  # 또는 find online_bookstore -type f
```

### 🎯 **환경 구축 완료 확인**

**다음 명령들이 모두 성공해야 합니다:**

```bash
# 1. Python 실행 확인
python --version

# 2. 현재 작업 디렉토리 확인
pwd

# 3. 폴더 구조 확인
ls -la

# 4. 모듈 import 테스트
python -c "import sys; print('\n'.join(sys.path))"
```

**✅ 환경 구축 성공 시 나타나는 현상:**
- VSCode에서 여러 폴더와 파일을 동시에 볼 수 있음
- 터미널에서 Python 모듈 실행 가능
- 파일 간 import가 정상적으로 작동
- 실시간으로 파일 편집 및 저장 가능

---

## 🎯 1부: 모듈과 패키지 - 코드를 체계적으로 조직하기 (40분)

### 📌 핵심 개념 1: 지금까지의 여정과 새로운 도전 (8분)

#### 🔄 **우리가 정복한 프로그래밍의 세계**

**1-8주차 성장 기록:**
```
1주차: "프로그래밍이 뭔지 알았다!" (기본 구조) ✅
2주차: "어디서든 코딩할 수 있게 되었다!" (개발환경) ✅
3주차: "변수로 복잡한 문제를 해결할 수 있다!" (자료형) ✅
4주차: "조건문으로 똑똑한 프로그램을 만들 수 있다!" (선택구조) ✅
5주차: "반복문으로 효율적인 프로그램을 만들 수 있다!" (반복구조) ✅
6주차: "자료구조로 체계적인 데이터 관리를 할 수 있다!" (컬렉션) ✅
7주차: "함수로 재사용 가능한 코드를 만들 수 있다!" (모듈화) ✅
8주차: "객체지향으로 현실 세계를 프로그램으로 만들 수 있다!" (OOP) ✅
```

**오늘 해결할 문제**: 
여러 파일에 흩어진 함수와 클래스들을 어떻게 체계적으로 관리하고, 안전하게 파일을 읽고 쓸 수 있을까?

#### 🏗️ **실제 프로젝트에서의 파일 구조 문제**

**예시: 온라인 쇼핑몰 프로젝트**
```
😰 모든 코드가 한 파일에 있으면...

main.py (5000줄!)
├── 사용자 관리 함수들 (500줄)
├── 상품 관리 클래스들 (800줄)
├── 주문 처리 함수들 (600줄)
├── 결제 시스템 클래스들 (700줄)
├── 데이터베이스 함수들 (400줄)
├── 이메일 발송 함수들 (300줄)
├── 리포트 생성 클래스들 (600줄)
└── 기타 유틸리티 함수들 (1100줄)

문제점:
❌ 코드 찾기가 지옥!
❌ 여러 명이 동시에 작업하기 불가능!
❌ 한 부분만 수정해도 전체 파일 재실행!
❌ 코드 재사용 불가능!
```

**✅ 모듈과 패키지로 체계적으로 관리하면:**
```
shopping_mall_project/
├── users/
│   ├── __init__.py
│   ├── user_manager.py      # 사용자 관리
│   └── auth.py              # 인증 처리
├── products/
│   ├── __init__.py
│   ├── product_manager.py   # 상품 관리
│   └── inventory.py         # 재고 관리
├── orders/
│   ├── __init__.py
│   ├── order_processor.py   # 주문 처리
│   └── payment.py           # 결제 시스템
├── utils/
│   ├── __init__.py
│   ├── database.py          # 데이터베이스
│   ├── email_sender.py      # 이메일 발송
│   └── report_generator.py  # 리포트 생성
└── main.py                  # 메인 실행 파일 (100줄!)

장점:
✅ 기능별로 명확한 분리!
✅ 팀 협업 가능!
✅ 부분 수정과 테스트 용이!
✅ 코드 재사용성 극대화!
```

### 📌 핵심 개념 2: 모듈 - 파이썬 파일 하나가 곧 모듈 (15분)

#### 📄 **모듈의 기본 개념**

**모듈 = 함수, 클래스, 변수가 들어있는 파이썬 파일**

**알고리즘 말투로 모듈 만들기 과정 표현:**
1. "특정 기능을 담당할 파이썬 파일을 만든다"
2. "관련된 함수들과 클래스들을 그 파일에 모은다"
3. "다른 파일에서 import문으로 불러와 사용한다"
4. "코드 재사용과 관리의 효율성을 극대화한다"

#### 🎯 **흥미로운 실습: 게임 캐릭터 관리 시스템**

**문제**: 게임 캐릭터들의 능력치와 행동을 모듈별로 분리하여 관리하기

**🖥️ VSCode에서 실제 프로젝트 구조 만들기:**

1. **VSCode 좌측 파일 탐색기에서 `game_character_system` 폴더 선택**
2. **우클릭 → "New File" → `character_stats.py` 입력**
3. **같은 방법으로 `character_actions.py`, `main_game.py` 파일 생성**

**최종 폴더 구조:**
```
game_character_system/
├── character_stats.py      ← 캐릭터 능력치 관리
├── character_actions.py    ← 캐릭터 행동 관리  
└── main_game.py           ← 메인 실행 파일
```

**1단계: character_stats.py 모듈 만들기**

```python
# character_stats.py - 캐릭터 능력치 관리 모듈

def create_character():
    """새로운 캐릭터 생성"""
    print("🎮 새로운 캐릭터를 만들어보세요!")
    
    name = input("캐릭터 이름: ")
    print("\n⭐ 직업을 선택하세요:")
    print("1. 전사 (높은 체력, 낮은 마나)")
    print("2. 마법사 (낮은 체력, 높은 마나)")
    print("3. 도적 (균형잡힌 능력치)")
    
    choice = input("선택 (1-3): ")
    
    if choice == "1":
        character = {
            "name": name,
            "class": "전사",
            "hp": 100,
            "mp": 30,
            "attack": 80,
            "defense": 70
        }
    elif choice == "2":
        character = {
            "name": name,
            "class": "마법사",
            "hp": 60,
            "mp": 100,
            "attack": 90,
            "defense": 40
        }
    else:
        character = {
            "name": name,
            "class": "도적",
            "hp": 80,
            "mp": 60,
            "attack": 85,
            "defense": 55
        }
    
    print(f"\n🎉 {character['class']} {name}이(가) 생성되었습니다!")
    display_character_info(character)
    return character

def display_character_info(character):
    """캐릭터 정보 출력"""
    print(f"\n📊 === {character['name']}의 정보 ===")
    print(f"직업: {character['class']}")
    print(f"체력: {character['hp']}")
    print(f"마나: {character['mp']}")
    print(f"공격력: {character['attack']}")
    print(f"방어력: {character['defense']}")

def level_up_character(character):
    """캐릭터 레벨업"""
    print(f"\n🌟 {character['name']}이(가) 레벨업했습니다!")
    
    # 능력치 증가
    hp_increase = 10
    mp_increase = 5
    attack_increase = 8
    defense_increase = 6
    
    character['hp'] += hp_increase
    character['mp'] += mp_increase
    character['attack'] += attack_increase
    character['defense'] += defense_increase
    
    print(f"📈 능력치가 상승했습니다!")
    print(f"  체력 +{hp_increase}, 마나 +{mp_increase}")
    print(f"  공격력 +{attack_increase}, 방어력 +{defense_increase}")
    
    return character

# 모듈 내에서 사용할 전역 변수
DEFAULT_CHARACTER = {
    "name": "기본캐릭터",
    "class": "초보자",
    "hp": 50,
    "mp": 50,
    "attack": 50,
    "defense": 50
}
```

**2단계: character_actions.py 모듈 만들기**

```python
# character_actions.py - 캐릭터 행동 관리 모듈

import random

def attack_monster(character, monster_name="몬스터"):
    """몬스터 공격"""
    print(f"\n⚔️ {character['name']}이(가) {monster_name}을(를) 공격합니다!")
    
    # 공격 성공 확률 계산 (공격력에 따라)
    success_rate = min(90, character['attack'] // 10 * 10 + 50)
    
    if random.randint(1, 100) <= success_rate:
        damage = random.randint(character['attack'] - 10, character['attack'] + 10)
        print(f"💥 성공! {damage}의 데미지를 입혔습니다!")
        return damage
    else:
        print("😅 공격이 빗나갔습니다!")
        return 0

def use_magic(character, spell_name="파이어볼"):
    """마법 사용"""
    magic_cost = 20
    
    if character['mp'] < magic_cost:
        print(f"\n💔 마나가 부족합니다! (현재: {character['mp']}, 필요: {magic_cost})")
        return False
    
    character['mp'] -= magic_cost
    magic_damage = character['attack'] + random.randint(10, 30)
    
    print(f"\n✨ {character['name']}이(가) {spell_name}을(를) 시전했습니다!")
    print(f"🔥 {magic_damage}의 마법 데미지! (마나 -{magic_cost})")
    
    return magic_damage

def rest_character(character):
    """캐릭터 휴식 (체력/마나 회복)"""
    print(f"\n😴 {character['name']}이(가) 휴식을 취합니다...")
    
    hp_recovery = 25
    mp_recovery = 30
    
    character['hp'] = min(character['hp'] + hp_recovery, 200)  # 최대 200으로 제한
    character['mp'] = min(character['mp'] + mp_recovery, 200)
    
    print(f"💚 체력 +{hp_recovery}, 마나 +{mp_recovery} 회복!")
    print(f"   현재 상태 - 체력: {character['hp']}, 마나: {character['mp']}")

def get_user_action():
    """사용자로부터 행동 선택 받기"""
    print("\n🎯 어떤 행동을 하시겠습니까?")
    print("1. 몬스터 공격 ⚔️")
    print("2. 마법 사용 ✨")
    print("3. 휴식하기 😴")
    print("4. 상태 확인 📊")
    print("5. 종료하기 🚪")
    
    choice = input("선택 (1-5): ")
    return choice
```

**3단계: main_game.py - 메인 실행 파일**

```python
# main_game.py - 메인 게임 실행 파일

# 모듈 import하기
import character_stats
import character_actions

def main_game():
    """메인 게임 함수"""
    print("🎮 ================================")
    print("   🏰 텍스트 RPG 게임에 오신 것을 환영합니다! 🏰")
    print("🎮 ================================")
    
    # 캐릭터 생성
    my_character = character_stats.create_character()
    
    # 게임 루프
    while True:
        action = character_actions.get_user_action()
        
        if action == "1":
            # 몬스터 공격
            monsters = ["고블린", "오크", "드래곤", "슬라임", "스켈레톤"]
            import random
            monster = random.choice(monsters)
            damage = character_actions.attack_monster(my_character, monster)
            
        elif action == "2":
            # 마법 사용
            spells = ["파이어볼", "아이스볼트", "라이트닝", "힐링"]
            import random
            spell = random.choice(spells)
            character_actions.use_magic(my_character, spell)
            
        elif action == "3":
            # 휴식
            character_actions.rest_character(my_character)
            
        elif action == "4":
            # 상태 확인
            character_stats.display_character_info(my_character)
            
        elif action == "5":
            print("\n👋 게임을 종료합니다. 수고하셨습니다!")
            break
            
        else:
            print("❌ 잘못된 선택입니다. 1-5 중에서 선택해주세요.")
        
        # 랜덤 레벨업 기회
        import random
        if random.randint(1, 100) <= 15:  # 15% 확률
            my_character = character_stats.level_up_character(my_character)

# 프로그램 실행
if __name__ == "__main__":
    main_game()
```

**🖥️ VSCode에서 실행하기:**

1. **터미널 열기**: `Ctrl + ` (백틱) 또는 `Terminal` → `New Terminal`
2. **프로젝트 폴더로 이동**:
   ```bash
   cd /workspace/week9_projects/game_character_system
   ```
3. **Python 파일 실행**:
   ```bash
   python main_game.py
   ```
4. **모듈 개별 테스트**:
   ```bash
   # 대화형 Python에서 모듈 테스트
   python
   >>> import character_stats
   >>> import character_actions
   >>> # 각 함수들을 개별적으로 테스트 가능
   >>> exit()
   ```

**✅ 실행 성공 확인:**
- 게임 시작 메시지가 출력됨
- 캐릭터 생성 화면이 나타남
- 사용자 입력을 받아 캐릭터 생성 가능
- 게임 메뉴가 정상적으로 표시됨

### 📌 핵심 개념 3: import문 작성 규칙과 다양한 방법 (17분)

#### 📥 **import문의 다양한 형태**

**1. 전체 모듈 가져오기**
```python
# 방법 1: 전체 모듈 import
import character_stats
import character_actions

# 사용할 때마다 모듈명 명시
my_char = character_stats.create_character()
character_actions.attack_monster(my_char)
```

**2. 특정 함수만 가져오기**
```python
# 방법 2: 필요한 함수만 import
from character_stats import create_character, display_character_info
from character_actions import attack_monster, use_magic

# 함수명만으로 직접 사용 가능
my_char = create_character()
attack_monster(my_char)
display_character_info(my_char)
```

**3. 별명(alias) 사용하기**
```python
# 방법 3: 별명으로 import (긴 모듈명을 줄일 때)
import character_stats as cs
import character_actions as ca

# 짧은 별명으로 사용
my_char = cs.create_character()
ca.attack_monster(my_char)
```

**4. 모든 함수 가져오기 (⚠️ 주의 필요)**
```python
# 방법 4: 모든 함수 import (권장하지 않음)
from character_stats import *
from character_actions import *

# 직접 함수명 사용 (하지만 이름 충돌 위험!)
my_char = create_character()
attack_monster(my_char)
```

#### 📋 **import문 작성 규칙 (PEP 8 가이드라인)**

**표준 import 순서:**
```python
# 1. 표준 라이브러리 (Python 내장)
import os
import random
import datetime

# 2. 써드파티 라이브러리 (pip로 설치한 것들)
import numpy as np
import pandas as pd
import requests

# 3. 로컬 모듈 (내가 만든 모듈들)
import character_stats
import character_actions
from utils import database_helper
```

#### 🎯 **실습: 스마트 계산기 모듈 시스템**

**문제**: 다양한 계산 기능을 모듈로 분리하여 체계적인 계산기 만들기

**🖥️ VSCode에서 계산기 프로젝트 구조 만들기:**

```bash
# VSCode 터미널에서 새 프로젝트 폴더 생성
cd /workspace/week9_projects
mkdir smart_calculator
cd smart_calculator
```

**VSCode 파일 탐색기에서 다음 파일들 생성:**
```
smart_calculator/
├── basic_calculator.py      ← 기본 사칙연산
├── advanced_calculator.py   ← 고급 수학함수
├── input_handler.py        ← 사용자 입력 처리
└── main_calculator.py      ← 메인 실행 파일
```

**알고리즘 말투로 요구사항 표현:**
1. "기본 사칙연산을 담당하는 모듈을 만든다"
2. "고급 수학 함수를 담당하는 모듈을 만든다"
3. "사용자 입력을 처리하는 모듈을 만든다"
4. "메인 프로그램에서 모든 모듈을 조합하여 완전한 계산기를 구현한다"

**basic_calculator.py 모듈:**

```python
# basic_calculator.py - 기본 계산 기능 모듈

def add(a, b):
    """두 수를 더합니다"""
    result = a + b
    print(f"📊 {a} + {b} = {result}")
    return result

def subtract(a, b):
    """두 수를 뺍니다"""
    result = a - b
    print(f"📊 {a} - {b} = {result}")
    return result

def multiply(a, b):
    """두 수를 곱합니다"""
    result = a * b
    print(f"📊 {a} × {b} = {result}")
    return result

def divide(a, b):
    """두 수를 나눕니다"""
    if b == 0:
        print("❌ 0으로 나눌 수 없습니다!")
        return None
    
    result = a / b
    print(f"📊 {a} ÷ {b} = {result}")
    return result

def get_calculation_history():
    """계산 기록을 반환합니다 (간단한 버전)"""
    return "기본 계산기 사용 중..."
```

**advanced_calculator.py 모듈:**

```python
# advanced_calculator.py - 고급 계산 기능 모듈

import math

def power(base, exponent):
    """거듭제곱 계산"""
    result = base ** exponent
    print(f"📊 {base}^{exponent} = {result}")
    return result

def square_root(number):
    """제곱근 계산"""
    if number < 0:
        print("❌ 음수의 제곱근은 계산할 수 없습니다!")
        return None
    
    result = math.sqrt(number)
    print(f"📊 √{number} = {result}")
    return result

def factorial(n):
    """팩토리얼 계산"""
    if n < 0:
        print("❌ 음수의 팩토리얼은 계산할 수 없습니다!")
        return None
    
    if n == 0 or n == 1:
        result = 1
    else:
        result = math.factorial(n)
    
    print(f"📊 {n}! = {result}")
    return result

def percentage(part, whole):
    """백분율 계산"""
    if whole == 0:
        print("❌ 전체값이 0이면 백분율을 계산할 수 없습니다!")
        return None
    
    result = (part / whole) * 100
    print(f"📊 {part}/{whole} × 100 = {result}%")
    return result
```

---

## ☕ 휴식 시간 (10분)

---

## 🎯 2부: 패키지와 파일 구조화 (40분)

### 📌 핵심 개념 1: 패키지 - 모듈들의 집합 (20분)

#### 📁 **패키지의 기본 개념**

**패키지 = 관련된 모듈들을 하나의 폴더로 묶은 것**

**예시: 학교 관리 시스템 패키지 구조**

```
school_system/                    # 루트 패키지
├── __init__.py                   # 패키지 초기화 파일
├── students/                     # 학생 관리 서브패키지
│   ├── __init__.py
│   ├── student_manager.py        # 학생 등록/수정/삭제
│   ├── grade_manager.py          # 성적 관리
│   └── attendance_tracker.py     # 출석 관리
├── teachers/                     # 교사 관리 서브패키지
│   ├── __init__.py
│   ├── teacher_manager.py        # 교사 정보 관리
│   └── schedule_manager.py       # 시간표 관리
├── courses/                      # 수업 관리 서브패키지
│   ├── __init__.py
│   ├── course_manager.py         # 수업 개설/관리
│   └── curriculum.py             # 교육과정 관리
└── utils/                        # 공통 유틸리티
    ├── __init__.py
    ├── database.py               # 데이터베이스 연결
    ├── file_handler.py           # 파일 입출력
    └── validators.py             # 데이터 검증
```

#### 🎯 **패키지 실습: 미니 온라인 서점**

**문제**: 온라인 서점의 다양한 기능을 패키지로 체계적으로 구성하기

**🖥️ VSCode에서 패키지 구조 만들기:**

1. **터미널에서 기본 구조 생성**:
   ```bash
   cd /workspace/week9_projects
   mkdir -p online_bookstore/{books,users,orders,utils}
   cd online_bookstore
   ```

2. **VSCode 파일 탐색기에서 __init__.py 파일들 생성**:
   - `online_bookstore/__init__.py`
   - `online_bookstore/books/__init__.py`
   - `online_bookstore/users/__init__.py`
   - `online_bookstore/orders/__init__.py`
   - `online_bookstore/utils/__init__.py`

3. **터미널에서 구조 확인**:
   ```bash
   # 패키지 구조 확인
   find . -name "*.py" | sort
   
   # 또는 tree 명령어 (설치되어 있다면)
   tree .
   ```

**최종 패키지 구조:**
```
online_bookstore/
├── __init__.py
├── books/
│   ├── __init__.py
│   ├── book_manager.py
│   └── search_engine.py
├── users/
│   ├── __init__.py
│   ├── user_manager.py
│   └── authentication.py
├── orders/
│   ├── __init__.py
│   ├── cart.py
│   └── payment.py
└── utils/
    ├── __init__.py
    ├── file_manager.py
    └── data_validator.py
```

**알고리즘 말투로 패키지 설계 과정:**
1. "전체 시스템의 주요 기능들을 식별한다"
2. "관련된 기능들을 그룹별로 묶는다"
3. "각 그룹을 패키지(폴더)로 만든다"
4. "패키지 내에 관련 모듈들을 배치한다"
5. "__init__.py 파일로 패키지를 초기화한다"

**1단계: 패키지 구조 만들기**

**2단계: books/book_manager.py**

```python
# books/book_manager.py

class Book:
    """책 정보를 관리하는 클래스"""
    
    def __init__(self, isbn, title, author, price, stock=0):
        self.isbn = isbn
        self.title = title
        self.author = author
        self.price = price
        self.stock = stock
    
    def display_info(self):
        """책 정보 출력"""
        print(f"📚 === {self.title} ===")
        print(f"   저자: {self.author}")
        print(f"   가격: {self.price:,}원")
        print(f"   재고: {self.stock}권")
        print(f"   ISBN: {self.isbn}")

class BookManager:
    """책 관리를 담당하는 클래스"""
    
    def __init__(self):
        self.books = {}  # ISBN을 키로 하는 책 딕셔너리
        self._initialize_sample_books()
    
    def _initialize_sample_books(self):
        """샘플 책 데이터 초기화"""
        sample_books = [
            ("978-89-1234-567-8", "파이썬 완전 정복", "김개발", 25000, 5),
            ("978-89-1234-568-5", "웹 개발의 모든 것", "이코딩", 30000, 3),
            ("978-89-1234-569-2", "데이터 사이언스 입문", "박분석", 28000, 7),
            ("978-89-1234-570-8", "AI와 머신러닝", "최인공", 35000, 2),
            ("978-89-1234-571-5", "게임 개발 실전", "정게임", 32000, 4)
        ]
        
        for isbn, title, author, price, stock in sample_books:
            book = Book(isbn, title, author, price, stock)
            self.books[isbn] = book
    
    def add_book(self, isbn, title, author, price, stock=0):
        """새 책 추가"""
        if isbn in self.books:
            print(f"❌ 이미 등록된 책입니다: {isbn}")
            return False
        
        book = Book(isbn, title, author, price, stock)
        self.books[isbn] = book
        print(f"✅ 책이 성공적으로 등록되었습니다: {title}")
        return True
    
    def get_book(self, isbn):
        """ISBN으로 책 조회"""
        return self.books.get(isbn)
    
    def list_all_books(self):
        """모든 책 목록 출력"""
        if not self.books:
            print("📚 등록된 책이 없습니다.")
            return
        
        print("\n📚 === 전체 도서 목록 ===")
        for book in self.books.values():
            book.display_info()
            print("-" * 30)
    
    def update_stock(self, isbn, new_stock):
        """재고 업데이트"""
        if isbn in self.books:
            old_stock = self.books[isbn].stock
            self.books[isbn].stock = new_stock
            print(f"📦 재고 업데이트: {old_stock} → {new_stock}")
            return True
        else:
            print(f"❌ 책을 찾을 수 없습니다: {isbn}")
            return False
```

**3단계: users/user_manager.py**

```python
# users/user_manager.py

class User:
    """사용자 정보를 관리하는 클래스"""
    
    def __init__(self, user_id, name, email, phone):
        self.user_id = user_id
        self.name = name
        self.email = email
        self.phone = phone
        self.order_history = []
    
    def display_info(self):
        """사용자 정보 출력"""
        print(f"👤 === {self.name}님의 정보 ===")
        print(f"   아이디: {self.user_id}")
        print(f"   이메일: {self.email}")
        print(f"   전화번호: {self.phone}")
        print(f"   주문 횟수: {len(self.order_history)}번")

class UserManager:
    """사용자 관리를 담당하는 클래스"""
    
    def __init__(self):
        self.users = {}
        self.current_user = None
    
    def register_user(self):
        """새 사용자 등록"""
        print("\n👤 === 회원가입 ===")
        
        user_id = input("아이디를 입력하세요: ")
        if user_id in self.users:
            print("❌ 이미 존재하는 아이디입니다.")
            return False
        
        name = input("이름을 입력하세요: ")
        email = input("이메일을 입력하세요: ")
        phone = input("전화번호를 입력하세요: ")
        
        user = User(user_id, name, email, phone)
        self.users[user_id] = user
        
        print(f"✅ 회원가입이 완료되었습니다! 환영합니다, {name}님!")
        return True
    
    def login(self):
        """사용자 로그인"""
        print("\n🔐 === 로그인 ===")
        
        user_id = input("아이디를 입력하세요: ")
        
        if user_id in self.users:
            self.current_user = self.users[user_id]
            print(f"✅ 로그인 성공! 환영합니다, {self.current_user.name}님!")
            return True
        else:
            print("❌ 존재하지 않는 아이디입니다.")
            return False
    
    def logout(self):
        """로그아웃"""
        if self.current_user:
            print(f"👋 {self.current_user.name}님, 안전하게 로그아웃되었습니다.")
            self.current_user = None
        else:
            print("❌ 현재 로그인된 사용자가 없습니다.")
    
    def get_current_user(self):
        """현재 로그인된 사용자 반환"""
        return self.current_user
```

**4단계: __init__.py 파일들 작성**

```python
# online_bookstore/__init__.py
"""
온라인 서점 패키지
책 관리, 사용자 관리, 주문 처리 기능을 제공합니다.
"""

__version__ = "1.0.0"
__author__ = "서점 개발팀"

# 주요 클래스들을 패키지 레벨에서 바로 사용할 수 있게 import
from .books.book_manager import BookManager, Book
from .users.user_manager import UserManager, User

# 패키지 정보
print("📚 온라인 서점 시스템이 로드되었습니다!")
```

```python
# books/__init__.py
"""책 관리 서브패키지"""

from .book_manager import BookManager, Book
from .search_engine import SearchEngine
```

```python
# users/__init__.py
"""사용자 관리 서브패키지"""

from .user_manager import UserManager, User
from .authentication import AuthManager
```

### 📌 핵심 개념 2: 패키지 import 방법들 (20분)

#### 📥 **패키지 import의 다양한 방법**

**1. 전체 패키지 import**
```python
# main.py

# 방법 1: 패키지 전체 import
import online_bookstore

# 사용법
book_manager = online_bookstore.BookManager()
user_manager = online_bookstore.UserManager()
```

**2. 서브패키지별 import**
```python
# 방법 2: 서브패키지별 import
from online_bookstore import books, users

# 사용법
book_manager = books.BookManager()
user_manager = users.UserManager()
```

**3. 특정 클래스만 import**
```python
# 방법 3: 필요한 클래스만 import
from online_bookstore.books import BookManager, Book
from online_bookstore.users import UserManager

# 사용법
book_manager = BookManager()
user_manager = UserManager()
```

**4. 깊은 경로의 모듈 import**
```python
# 방법 4: 전체 경로로 import
from online_bookstore.books.book_manager import BookManager
from online_bookstore.users.user_manager import UserManager

# 사용법
book_manager = BookManager()
user_manager = UserManager()
```

#### 🎯 **실습: 완전한 온라인 서점 메인 프로그램**

```python
# main_bookstore.py - 메인 실행 파일

# 패키지에서 필요한 클래스들 import
from online_bookstore.books.book_manager import BookManager
from online_bookstore.users.user_manager import UserManager

def display_main_menu():
    """메인 메뉴 출력"""
    print("\n📚 === 온라인 서점 메인 메뉴 ===")
    print("1. 도서 목록 보기 📖")
    print("2. 도서 검색 🔍")
    print("3. 회원가입 👤")
    print("4. 로그인 🔐")
    print("5. 로그아웃 👋")
    print("6. 내 정보 보기 📋")
    print("7. 관리자 메뉴 ⚙️")
    print("0. 종료 🚪")

def admin_menu(book_manager):
    """관리자 메뉴"""
    print("\n⚙️ === 관리자 메뉴 ===")
    print("1. 도서 추가")
    print("2. 재고 관리")
    print("3. 돌아가기")
    
    choice = input("선택하세요: ")
    
    if choice == "1":
        # 도서 추가
        print("\n📚 새 도서 추가")
        isbn = input("ISBN: ")
        title = input("제목: ")
        author = input("저자: ")
        price = int(input("가격: "))
        stock = int(input("재고: "))
        
        book_manager.add_book(isbn, title, author, price, stock)
    
    elif choice == "2":
        # 재고 관리
        print("\n📦 재고 관리")
        isbn = input("재고를 수정할 책의 ISBN: ")
        new_stock = int(input("새로운 재고 수량: "))
        book_manager.update_stock(isbn, new_stock)

def main():
    """메인 함수"""
    print("🎉 온라인 서점에 오신 것을 환영합니다! 🎉")
    
    # 관리 객체들 생성
    book_manager = BookManager()
    user_manager = UserManager()
    
    while True:
        display_main_menu()
        choice = input("\n메뉴를 선택하세요: ")
        
        if choice == "1":
            # 도서 목록 보기
            book_manager.list_all_books()
        
        elif choice == "2":
            # 도서 검색
            keyword = input("검색어를 입력하세요: ")
            print(f"🔍 '{keyword}' 검색 결과:")
            # 간단한 제목 검색
            found = False
            for book in book_manager.books.values():
                if keyword.lower() in book.title.lower():
                    book.display_info()
                    found = True
            if not found:
                print("❌ 검색 결과가 없습니다.")
        
        elif choice == "3":
            # 회원가입
            user_manager.register_user()
        
        elif choice == "4":
            # 로그인
            user_manager.login()
        
        elif choice == "5":
            # 로그아웃
            user_manager.logout()
        
        elif choice == "6":
            # 내 정보 보기
            current_user = user_manager.get_current_user()
            if current_user:
                current_user.display_info()
            else:
                print("❌ 로그인이 필요합니다.")
        
        elif choice == "7":
            # 관리자 메뉴
            admin_menu(book_manager)
        
        elif choice == "0":
            print("👋 서점을 이용해 주셔서 감사합니다!")
            break
        
        else:
            print("❌ 잘못된 선택입니다. 다시 선택해주세요.")

if __name__ == "__main__":
    main()
```

**🖥️ VSCode에서 패키지 테스트하기:**

1. **패키지 구조가 올바른지 확인**:
   ```bash
   cd /workspace/week9_projects/online_bookstore
   python -c "import online_bookstore; print('패키지 로드 성공!')"
   ```

2. **개별 모듈 테스트**:
   ```bash
   # 대화형 Python에서 테스트
   python
   >>> from online_bookstore.books.book_manager import BookManager
   >>> book_manager = BookManager()
   >>> book_manager.list_all_books()
   >>> exit()
   ```

3. **메인 프로그램 실행**:
   ```bash
   # 온라인 서점 시스템 실행
   python main_bookstore.py
   ```

4. **패키지 import 오류 해결**:
   ```bash
   # 현재 디렉토리가 Python 경로에 있는지 확인
   python -c "import sys; print('\\n'.join(sys.path))"
   
   # 필요시 PYTHONPATH 환경변수 설정
   export PYTHONPATH=/workspace/week9_projects:$PYTHONPATH
   ```

**✅ 패키지 실행 성공 확인:**
- 패키지 import가 오류 없이 실행됨
- 서점 메인 메뉴가 정상 출력됨
- 도서 관리 기능이 정상 작동함
- 회원 관리 기능이 정상 작동함

---

## ☕ 휴식 시간 (10분)

---

## 🎯 3부: 파일 입출력과 예외 처리 (40분)

### 📌 핵심 개념 1: 파일 입출력 - 데이터를 영구 저장하기 (25분)

#### 💾 **파일 입출력의 필요성**

**문제 상황**: 프로그램이 종료되면 모든 데이터가 사라진다!

```python
# 😰 이런 상황이 발생합니다...
students = ["김철수", "이영희", "박민수"]  # 메모리에만 저장
print("학생 목록:", students)

# 프로그램 종료 → 모든 데이터 사라짐! 😱
# 다시 실행하면 학생 목록이 빈 리스트가 됩니다.
```

**해결책**: 파일에 데이터를 저장하고 읽어오기!

#### 📝 **텍스트 파일 다루기**

**알고리즘 말투로 파일 처리 과정 표현:**
1. "파일을 연다 (읽기/쓰기 모드 지정)"
2. "파일에 데이터를 쓰거나 읽는다"
3. "작업이 끝나면 파일을 닫는다"
4. "예외 상황에 대비하여 안전하게 처리한다"

#### 🎯 **실습: 학생 성적 관리 시스템**

**문제**: 학생들의 성적을 파일에 저장하고 불러오는 시스템 만들기

**1단계: 파일 쓰기 기능**

```python
# file_manager.py - 파일 관리 모듈

def save_student_grades(filename, students_data):
    """학생 성적을 파일에 저장"""
    print(f"💾 {filename}에 학생 성적을 저장합니다...")
    
    try:
        with open(filename, 'w', encoding='utf-8') as file:
            # 헤더 작성
            file.write("학생이름,국어,영어,수학,평균\n")
            
            # 각 학생 데이터 작성
            for student in students_data:
                name = student['name']
                korean = student['korean']
                english = student['english']
                math = student['math']
                average = (korean + english + math) / 3
                
                line = f"{name},{korean},{english},{math},{average:.1f}\n"
                file.write(line)
        
        print(f"✅ 성공적으로 저장되었습니다! ({len(students_data)}명)")
        return True
        
    except Exception as e:
        print(f"❌ 파일 저장 중 오류 발생: {e}")
        return False

def load_student_grades(filename):
    """파일에서 학생 성적을 불러오기"""
    print(f"📂 {filename}에서 학생 성적을 불러옵니다...")
    
    students_data = []
    
    try:
        with open(filename, 'r', encoding='utf-8') as file:
            lines = file.readlines()
            
            # 첫 번째 줄(헤더) 건너뛰기
            for line in lines[1:]:
                line = line.strip()  # 앞뒤 공백 제거
                if line:  # 빈 줄이 아닌 경우
                    parts = line.split(',')
                    
                    student = {
                        'name': parts[0],
                        'korean': int(parts[1]),
                        'english': int(parts[2]),
                        'math': int(parts[3])
                    }
                    students_data.append(student)
        
        print(f"✅ 성공적으로 불러왔습니다! ({len(students_data)}명)")
        return students_data
        
    except FileNotFoundError:
        print(f"❌ {filename} 파일을 찾을 수 없습니다.")
        return []
    except Exception as e:
        print(f"❌ 파일 읽기 중 오류 발생: {e}")
        return []

def get_student_input():
    """사용자로부터 학생 정보 입력받기"""
    print("\n📝 학생 성적 입력")
    name = input("학생 이름: ")
    
    # 성적 입력 (예외 처리 포함)
    try:
        korean = int(input("국어 점수 (0-100): "))
        english = int(input("영어 점수 (0-100): "))
        math = int(input("수학 점수 (0-100): "))
        
        # 점수 유효성 검사
        if not (0 <= korean <= 100 and 0 <= english <= 100 and 0 <= math <= 100):
            print("❌ 점수는 0-100 사이여야 합니다.")
            return None
        
        student = {
            'name': name,
            'korean': korean,
            'english': english,
            'math': math
        }
        
        return student
        
    except ValueError:
        print("❌ 점수는 숫자로 입력해주세요.")
        return None

def display_student_grades(students_data):
    """학생 성적 출력"""
    if not students_data:
        print("📚 등록된 학생이 없습니다.")
        return
    
    print("\n📊 === 학생 성적표 ===")
    print(f"{'이름':^8} {'국어':^6} {'영어':^6} {'수학':^6} {'평균':^8} {'등급':^4}")
    print("-" * 50)
    
    for student in students_data:
        name = student['name']
        korean = student['korean']
        english = student['english']
        math = student['math']
        average = (korean + english + math) / 3
        
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
        
        print(f"{name:^8} {korean:^6} {english:^6} {math:^6} {average:^8.1f} {grade:^4}")

def backup_file(original_filename):
    """파일 백업 만들기"""
    import datetime
    
    # 현재 시간을 이용한 백업 파일명 생성
    now = datetime.datetime.now()
    timestamp = now.strftime("%Y%m%d_%H%M%S")
    backup_filename = f"backup_{timestamp}_{original_filename}"
    
    try:
        with open(original_filename, 'r', encoding='utf-8') as original:
            content = original.read()
        
        with open(backup_filename, 'w', encoding='utf-8') as backup:
            backup.write(content)
        
        print(f"💾 백업 파일 생성: {backup_filename}")
        return True
        
    except Exception as e:
        print(f"❌ 백업 생성 실패: {e}")
        return False
```

**2단계: 메인 프로그램**

```python
# grade_management_system.py - 메인 성적 관리 시스템

import file_manager

def display_menu():
    """메뉴 출력"""
    print("\n📚 === 학생 성적 관리 시스템 ===")
    print("1. 학생 성적 입력 ✏️")
    print("2. 성적표 보기 📊")
    print("3. 파일에 저장 💾")
    print("4. 파일에서 불러오기 📂")
    print("5. 파일 백업 🔄")
    print("6. 통계 보기 📈")
    print("0. 종료 🚪")

def show_statistics(students_data):
    """성적 통계 출력"""
    if not students_data:
        print("📚 등록된 학생이 없습니다.")
        return
    
    print("\n📈 === 성적 통계 ===")
    
    # 전체 평균 계산
    total_korean = sum(s['korean'] for s in students_data)
    total_english = sum(s['english'] for s in students_data)
    total_math = sum(s['math'] for s in students_data)
    
    student_count = len(students_data)
    
    avg_korean = total_korean / student_count
    avg_english = total_english / student_count
    avg_math = total_math / student_count
    overall_avg = (avg_korean + avg_english + avg_math) / 3
    
    print(f"👥 총 학생 수: {student_count}명")
    print(f"📊 과목별 평균:")
    print(f"   국어: {avg_korean:.1f}점")
    print(f"   영어: {avg_english:.1f}점")
    print(f"   수학: {avg_math:.1f}점")
    print(f"🎯 전체 평균: {overall_avg:.1f}점")
    
    # 최고점과 최저점
    all_averages = [(s['korean'] + s['english'] + s['math']) / 3 for s in students_data]
    max_avg = max(all_averages)
    min_avg = min(all_averages)
    
    max_student = students_data[all_averages.index(max_avg)]
    min_student = students_data[all_averages.index(min_avg)]
    
    print(f"🏆 최고 성적: {max_student['name']} ({max_avg:.1f}점)")
    print(f"📉 최저 성적: {min_student['name']} ({min_avg:.1f}점)")

def main():
    """메인 함수"""
    print("🎉 학생 성적 관리 시스템을 시작합니다! 🎉")
    
    students_data = []
    filename = "student_grades.csv"
    
    while True:
        display_menu()
        choice = input("\n메뉴를 선택하세요: ")
        
        if choice == "1":
            # 학생 성적 입력
            student = file_manager.get_student_input()
            if student:
                students_data.append(student)
                print(f"✅ {student['name']} 학생이 추가되었습니다.")
        
        elif choice == "2":
            # 성적표 보기
            file_manager.display_student_grades(students_data)
        
        elif choice == "3":
            # 파일에 저장
            if students_data:
                file_manager.save_student_grades(filename, students_data)
            else:
                print("❌ 저장할 학생 데이터가 없습니다.")
        
        elif choice == "4":
            # 파일에서 불러오기
            loaded_data = file_manager.load_student_grades(filename)
            if loaded_data:
                students_data = loaded_data
                print("✅ 데이터를 성공적으로 불러왔습니다.")
        
        elif choice == "5":
            # 파일 백업
            file_manager.backup_file(filename)
        
        elif choice == "6":
            # 통계 보기
            show_statistics(students_data)
        
        elif choice == "0":
            # 종료
            if students_data:
                save_choice = input("💾 종료 전에 저장하시겠습니까? (y/n): ")
                if save_choice.lower() == 'y':
                    file_manager.save_student_grades(filename, students_data)
            
            print("👋 성적 관리 시스템을 종료합니다. 수고하셨습니다!")
            break
        
        else:
            print("❌ 잘못된 선택입니다. 다시 선택해주세요.")

if __name__ == "__main__":
    main()
```

**🖥️ VSCode에서 파일 입출력 시스템 실행하기:**

1. **프로젝트 폴더 생성**:
   ```bash
   cd /workspace/week9_projects
   mkdir grade_management
   cd grade_management
   ```

2. **VSCode에서 파일 생성**:
   - `file_manager.py` (파일 관리 모듈)
   - `grade_management_system.py` (메인 프로그램)

3. **실행 및 테스트**:
   ```bash
   # 시스템 실행
   python grade_management_system.py
   ```

4. **파일 생성 확인**:
   ```bash
   # 프로그램 실행 후 생성된 파일들 확인
   ls -la
   
   # CSV 파일 내용 확인
   cat student_grades.csv
   
   # 백업 파일들 확인
   ls -la backup_*
   ```

**✅ 파일 처리 성공 확인:**
- 학생 데이터를 CSV 파일로 저장 가능
- 저장된 파일에서 데이터 로드 가능
- 백업 파일이 타임스탬프와 함께 생성됨
- 프로그램 재시작 후에도 데이터 유지됨

### 📌 핵심 개념 2: 예외 처리 - 안전한 프로그램 만들기 (15분)

#### 🛡️ **예외 처리의 중요성**

**예외가 발생할 수 있는 상황들:**
```python
# 😰 이런 상황들에서 프로그램이 멈출 수 있습니다!

# 1. 파일이 없는 경우
file = open("없는파일.txt", "r")  # FileNotFoundError

# 2. 잘못된 데이터 타입 변환
age = int("스무살")  # ValueError

# 3. 0으로 나누기
result = 10 / 0  # ZeroDivisionError

# 4. 리스트 인덱스 초과
numbers = [1, 2, 3]
print(numbers[10])  # IndexError

# 5. 딕셔너리에 없는 키 접근
data = {"name": "김철수"}
print(data["age"])  # KeyError
```

#### 🎯 **try-except 구문으로 안전하게 처리하기**

**기본 예외 처리 패턴:**

```python
# safe_calculator.py - 안전한 계산기

def safe_divide():
    """안전한 나눗셈 함수"""
    try:
        print("🔢 안전한 나눗셈 계산기")
        
        # 사용자 입력받기
        num1 = float(input("첫 번째 숫자를 입력하세요: "))
        num2 = float(input("두 번째 숫자를 입력하세요: "))
        
        # 나눗셈 실행
        result = num1 / num2
        print(f"📊 결과: {num1} ÷ {num2} = {result}")
        
        return result
        
    except ValueError:
        print("❌ 오류: 숫자만 입력해주세요!")
        return None
    except ZeroDivisionError:
        print("❌ 오류: 0으로 나눌 수 없습니다!")
        return None
    except Exception as e:
        print(f"❌ 예상치 못한 오류가 발생했습니다: {e}")
        return None
    finally:
        print("🔚 계산이 완료되었습니다.")

def safe_file_operations():
    """안전한 파일 처리 예제"""
    filename = input("파일명을 입력하세요: ")
    
    try:
        # 파일 읽기 시도
        with open(filename, 'r', encoding='utf-8') as file:
            content = file.read()
            print(f"📄 파일 내용:\n{content}")
            
    except FileNotFoundError:
        print(f"❌ 오류: '{filename}' 파일을 찾을 수 없습니다.")
        
        # 새 파일 생성 옵션 제공
        create_new = input("새 파일을 생성하시겠습니까? (y/n): ")
        if create_new.lower() == 'y':
            try:
                with open(filename, 'w', encoding='utf-8') as file:
                    file.write("# 새로 생성된 파일입니다.\n")
                print(f"✅ '{filename}' 파일이 생성되었습니다.")
            except Exception as e:
                print(f"❌ 파일 생성 실패: {e}")
                
    except PermissionError:
        print(f"❌ 오류: '{filename}' 파일에 접근 권한이 없습니다.")
    except UnicodeDecodeError:
        print(f"❌ 오류: '{filename}' 파일의 인코딩이 올바르지 않습니다.")
    except Exception as e:
        print(f"❌ 예상치 못한 오류: {e}")

def safe_user_input():
    """안전한 사용자 입력 처리"""
    max_attempts = 3
    
    for attempt in range(max_attempts):
        try:
            print(f"\n🎯 시도 {attempt + 1}/{max_attempts}")
            
            age = int(input("나이를 입력하세요 (1-150): "))
            
            # 범위 검증
            if not (1 <= age <= 150):
                raise ValueError("나이는 1-150 사이여야 합니다.")
            
            print(f"✅ 입력된 나이: {age}세")
            
            # 연령대 분류
            if age < 13:
                category = "어린이"
            elif age < 20:
                category = "청소년"
            elif age < 65:
                category = "성인"
            else:
                category = "시니어"
            
            print(f"👤 연령대: {category}")
            return age
            
        except ValueError as e:
            print(f"❌ 오류: {e}")
            if attempt == max_attempts - 1:
                print("😔 최대 시도 횟수를 초과했습니다.")
                return None
        except KeyboardInterrupt:
            print("\n👋 사용자가 입력을 취소했습니다.")
            return None

# 예외 처리 테스트 함수
def test_exception_handling():
    """예외 처리 기능 테스트"""
    print("🧪 === 예외 처리 테스트 ===")
    
    print("\n1. 안전한 나눗셈 테스트:")
    safe_divide()
    
    print("\n2. 안전한 파일 처리 테스트:")
    safe_file_operations()
    
    print("\n3. 안전한 사용자 입력 테스트:")
    safe_user_input()

if __name__ == "__main__":
    test_exception_handling()
```

---

## 🎯 실습과제 (60분)

### 📝 **과제 1: 개인 일기 관리 시스템 (30분)**

**모듈과 패키지 구조를 활용한 종합 시스템 구현**

**🖥️ VSCode에서 프로젝트 구조 만들기:**

```bash
# 터미널에서 프로젝트 기본 구조 생성
cd /workspace/week9_projects
mkdir -p diary_system/{diary,storage,utils}
cd diary_system

# __init__.py 파일들 생성
touch __init__.py
touch diary/__init__.py
touch storage/__init__.py
touch utils/__init__.py
```

**VSCode 파일 탐색기에서 완성할 구조:**
```
diary_system/
├── __init__.py
├── main_diary.py               ← 메인 실행 파일
├── diary/
│   ├── __init__.py
│   ├── diary_manager.py        ← 일기 생성/수정/삭제
│   └── search_engine.py        ← 일기 검색
├── storage/
│   ├── __init__.py
│   ├── file_handler.py         ← 파일 입출력
│   └── backup_manager.py       ← 백업 관리
└── utils/
    ├── __init__.py
    ├── date_helper.py          ← 날짜 처리 유틸
    └── text_formatter.py       ← 텍스트 포맷팅
```

**알고리즘 말투로 요구사항 표현:**

1. **패키지 구조 설계**: "일기 관리의 주요 기능들을 모듈별로 분리한다"
2. **파일 저장**: "일기 내용을 날짜별 파일로 저장하고 불러온다"
3. **검색 기능**: "키워드로 일기를 검색할 수 있게 한다"
4. **백업 시스템**: "일기 데이터를 안전하게 백업한다"
5. **예외 처리**: "모든 파일 처리에 안전장치를 적용한다"

**필수 구현 기능:**
- 날짜별 일기 작성 및 저장
- 일기 목록 보기 및 읽기
- 키워드 검색 (제목, 내용 모두 검색)
- 일기 수정 및 삭제
- 자동 백업 기능
- 모든 파일 처리에 예외 처리 적용
- 사용자 친화적인 메뉴 시스템

**🖥️ 실행 및 테스트:**
```bash
# 일기 시스템 실행
cd /workspace/week9_projects/diary_system
python main_diary.py

# 패키지 import 테스트
python -c "from diary import diary_manager; print('패키지 로드 성공!')"
```

### 📝 **과제 2: 미니 도서관 관리 시스템 (30분)**

**🖥️ VSCode에서 프로젝트 구조 만들기:**

```bash
# 터미널에서 프로젝트 생성
cd /workspace/week9_projects
mkdir library_system
cd library_system
```

**VSCode 파일 탐색기에서 생성할 파일들:**
```
library_system/
├── book_manager.py         ← 도서 등록/수정/삭제/조회
├── member_manager.py       ← 회원 등록/관리
├── loan_manager.py         ← 도서 대출/반납 관리
├── file_operations.py      ← CSV 파일 읽기/쓰기
├── statistics.py           ← 통계 생성 및 리포트
└── main_library.py         ← 메인 실행 프로그램
```

**알고리즘 말투로 요구사항 표현:**

1. **모듈 분리**: "도서 관리, 회원 관리, 대출 관리를 각각 다른 모듈로 분리한다"
2. **데이터 영속성**: "모든 데이터를 파일로 저장하여 프로그램 재시작 후에도 유지한다"
3. **CSV 형식 지원**: "도서 목록과 회원 정보를 CSV 파일로 관리한다"
4. **통계 기능**: "대출 현황과 인기 도서 통계를 제공한다"
5. **안전성 확보**: "모든 입력과 파일 처리에 예외 처리를 적용한다"

**필수 구현 기능:**
- 도서 등록 (ISBN, 제목, 저자, 출판사, 재고)
- 회원 등록 (회원번호, 이름, 연락처, 가입일)
- 도서 대출/반납 시스템
- 대출 가능 여부 확인
- 연체 관리 (대출일 기준 14일)
- 인기 도서 순위 (대출 횟수 기준)
- 회원별 대출 이력
- 모든 데이터의 CSV 파일 저장/로드
- 프로그램 종료 시 자동 저장

**🖥️ 실행 및 테스트:**
```bash
# 도서관 시스템 실행
cd /workspace/week9_projects/library_system
python main_library.py

# CSV 파일 생성 확인
ls -la *.csv

# CSV 파일 내용 확인
head books.csv
head members.csv
head loans.csv
```

**🖥️ 프로젝트 완성도 확인 체크리스트:**

```bash
# 1. 모든 파일이 정상적으로 생성되었는지 확인
find /workspace/week9_projects -name "*.py" | wc -l

# 2. 각 프로젝트의 메인 파일이 실행되는지 확인
cd /workspace/week9_projects/diary_system
python -c "import main_diary; print('일기 시스템 OK')"

cd /workspace/week9_projects/library_system
python -c "import main_library; print('도서관 시스템 OK')"

# 3. 패키지 구조가 올바른지 확인
cd /workspace/week9_projects/diary_system
python -c "from diary import diary_manager; print('패키지 구조 OK')"

# 4. 파일 입출력이 정상적으로 작동하는지 확인
ls -la *.csv *.json *.txt 2>/dev/null | wc -l
```

---

## 📚 실습과제 모범답안

### 🏆 **과제 1 모범답안: 개인 일기 관리 시스템**

**diary/diary_manager.py:**
```python
# diary/diary_manager.py
import datetime

class DiaryEntry:
    """일기 항목 클래스"""
    
    def __init__(self, date, title, content):
        self.date = date
        self.title = title
        self.content = content
        self.created_time = datetime.datetime.now()
    
    def __str__(self):
        return f"[{self.date}] {self.title}"

class DiaryManager:
    """일기 관리 클래스"""
    
    def __init__(self):
        self.entries = {}  # date를 키로 하는 일기 딕셔너리
    
    def create_diary_entry(self):
        """새 일기 작성"""
        print("\n📝 === 새 일기 작성 ===")
        
        # 날짜 입력 (기본값: 오늘)
        today = datetime.date.today().strftime("%Y-%m-%d")
        date_input = input(f"날짜 (YYYY-MM-DD, 기본값: {today}): ")
        date = date_input if date_input else today
        
        # 제목과 내용 입력
        title = input("제목: ")
        print("내용을 입력하세요 (빈 줄 입력시 종료):")
        
        content_lines = []
        while True:
            line = input()
            if line == "":
                break
            content_lines.append(line)
        
        content = "\n".join(content_lines)
        
        # 일기 생성
        entry = DiaryEntry(date, title, content)
        self.entries[date] = entry
        
        print(f"✅ {date}의 일기가 저장되었습니다!")
        return entry
    
    def list_diary_entries(self):
        """일기 목록 출력"""
        if not self.entries:
            print("📖 작성된 일기가 없습니다.")
            return
        
        print("\n📚 === 일기 목록 ===")
        sorted_dates = sorted(self.entries.keys(), reverse=True)
        
        for i, date in enumerate(sorted_dates, 1):
            entry = self.entries[date]
            print(f"{i:2d}. {entry}")
        
        return sorted_dates
    
    def read_diary_entry(self, date):
        """특정 날짜의 일기 읽기"""
        if date in self.entries:
            entry = self.entries[date]
            print(f"\n📖 === {date}의 일기 ===")
            print(f"제목: {entry.title}")
            print(f"작성시간: {entry.created_time.strftime('%Y-%m-%d %H:%M:%S')}")
            print(f"\n내용:\n{entry.content}")
        else:
            print(f"❌ {date}에 작성된 일기가 없습니다.")
    
    def delete_diary_entry(self, date):
        """일기 삭제"""
        if date in self.entries:
            title = self.entries[date].title
            del self.entries[date]
            print(f"🗑️ {date}의 일기 '{title}'가 삭제되었습니다.")
            return True
        else:
            print(f"❌ {date}에 작성된 일기가 없습니다.")
            return False
```

**storage/file_handler.py:**
```python
# storage/file_handler.py
import json
import os
from datetime import datetime

def save_diaries_to_file(diary_manager, filename="diaries.json"):
    """일기를 JSON 파일로 저장"""
    try:
        data = {}
        for date, entry in diary_manager.entries.items():
            data[date] = {
                "title": entry.title,
                "content": entry.content,
                "created_time": entry.created_time.isoformat()
            }
        
        with open(filename, 'w', encoding='utf-8') as file:
            json.dump(data, file, ensure_ascii=False, indent=2)
        
        print(f"💾 일기가 {filename}에 저장되었습니다.")
        return True
        
    except Exception as e:
        print(f"❌ 저장 실패: {e}")
        return False

def load_diaries_from_file(diary_manager, filename="diaries.json"):
    """JSON 파일에서 일기 불러오기"""
    try:
        if not os.path.exists(filename):
            print(f"📁 {filename} 파일이 존재하지 않습니다.")
            return False
        
        with open(filename, 'r', encoding='utf-8') as file:
            data = json.load(file)
        
        # DiaryManager의 entries 초기화
        diary_manager.entries = {}
        
        # 데이터 복원
        from diary.diary_manager import DiaryEntry
        for date, entry_data in data.items():
            entry = DiaryEntry(date, entry_data["title"], entry_data["content"])
            entry.created_time = datetime.fromisoformat(entry_data["created_time"])
            diary_manager.entries[date] = entry
        
        print(f"📂 {filename}에서 {len(data)}개의 일기를 불러왔습니다.")
        return True
        
    except Exception as e:
        print(f"❌ 불러오기 실패: {e}")
        return False
```

### 🏆 **과제 2 모범답안: 미니 도서관 관리 시스템**

**book_manager.py:**
```python
# book_manager.py
import csv

class Book:
    """도서 클래스"""
    
    def __init__(self, isbn, title, author, publisher, stock=1):
        self.isbn = isbn
        self.title = title
        self.author = author
        self.publisher = publisher
        self.stock = stock
        self.loan_count = 0  # 대출 횟수
    
    def __str__(self):
        return f"[{self.isbn}] {self.title} - {self.author}"

class BookManager:
    """도서 관리 클래스"""
    
    def __init__(self):
        self.books = {}  # ISBN을 키로 하는 도서 딕셔너리
    
    def add_book(self):
        """도서 추가"""
        print("\n📚 === 도서 등록 ===")
        
        isbn = input("ISBN: ")
        if isbn in self.books:
            print("❌ 이미 등록된 ISBN입니다.")
            return False
        
        title = input("제목: ")
        author = input("저자: ")
        publisher = input("출판사: ")
        
        try:
            stock = int(input("재고 수량: "))
            if stock < 1:
                print("❌ 재고는 1권 이상이어야 합니다.")
                return False
        except ValueError:
            print("❌ 재고는 숫자로 입력해주세요.")
            return False
        
        book = Book(isbn, title, author, publisher, stock)
        self.books[isbn] = book
        
        print(f"✅ 도서가 등록되었습니다: {book}")
        return True
    
    def search_books(self, keyword):
        """도서 검색"""
        found_books = []
        keyword_lower = keyword.lower()
        
        for book in self.books.values():
            if (keyword_lower in book.title.lower() or 
                keyword_lower in book.author.lower() or
                keyword_lower in book.publisher.lower()):
                found_books.append(book)
        
        return found_books
    
    def display_all_books(self):
        """전체 도서 목록 출력"""
        if not self.books:
            print("📚 등록된 도서가 없습니다.")
            return
        
        print("\n📚 === 전체 도서 목록 ===")
        print(f"{'ISBN':^15} {'제목':^20} {'저자':^15} {'재고':^5} {'대출횟수':^8}")
        print("-" * 70)
        
        for book in self.books.values():
            print(f"{book.isbn:^15} {book.title:^20} {book.author:^15} {book.stock:^5} {book.loan_count:^8}")
    
    def save_to_csv(self, filename="books.csv"):
        """도서 목록을 CSV로 저장"""
        try:
            with open(filename, 'w', newline='', encoding='utf-8') as csvfile:
                writer = csv.writer(csvfile)
                writer.writerow(['ISBN', '제목', '저자', '출판사', '재고', '대출횟수'])
                
                for book in self.books.values():
                    writer.writerow([book.isbn, book.title, book.author, 
                                   book.publisher, book.stock, book.loan_count])
            
            print(f"💾 도서 목록이 {filename}에 저장되었습니다.")
            return True
            
        except Exception as e:
            print(f"❌ 저장 실패: {e}")
            return False
    
    def load_from_csv(self, filename="books.csv"):
        """CSV에서 도서 목록 불러오기"""
        try:
            with open(filename, 'r', encoding='utf-8') as csvfile:
                reader = csv.DictReader(csvfile)
                
                self.books = {}
                for row in reader:
                    book = Book(row['ISBN'], row['제목'], row['저자'], 
                              row['출판사'], int(row['재고']))
                    book.loan_count = int(row['대출횟수'])
                    self.books[book.isbn] = book
            
            print(f"📂 {filename}에서 {len(self.books)}권의 도서를 불러왔습니다.")
            return True
            
        except FileNotFoundError:
            print(f"📁 {filename} 파일이 존재하지 않습니다.")
            return False
        except Exception as e:
            print(f"❌ 불러오기 실패: {e}")
            return False
```

---

## 📚 오늘 배운 내용 정리

### ✅ 핵심 포인트

1. **모듈과 패키지의 중요성**:
   - 코드 재사용성과 유지보수성 향상
   - 기능별 명확한 분리와 체계적 관리
   - 팀 협업과 대규모 프로젝트 개발 가능

2. **import문 활용법**:
   - 다양한 import 방식의 특징과 용도
   - PEP 8 가이드라인에 따른 import 순서
   - 별명(alias) 활용과 선택적 import

3. **패키지 구조 설계**:
   - __init__.py의 역할과 활용
   - 서브패키지를 통한 계층적 구조
   - 관련 기능들의 논리적 그룹핑

4. **파일 입출력 마스터**:
   - 텍스트 파일과 CSV 파일 처리
   - with문을 활용한 안전한 파일 처리
   - 데이터 영속성과 백업 시스템

5. **예외 처리의 완전 정복**:
   - try-except-finally 구문 활용
   - 다양한 예외 타입별 대응책
   - 사용자 친화적인 오류 메시지

6. **실제 프로젝트 구조**:
   - 모듈과 패키지를 활용한 시스템 설계
   - 파일 저장과 불러오기 구현
   - 안전하고 견고한 프로그램 작성

### 🏠 다음 주까지 해볼 과제

1. **Docker + VSCode 환경 마스터**:
   - 개인 컴퓨터에 Docker Desktop 설치하여 연습
   - 다양한 파이썬 프로젝트 구조를 VSCode에서 관리
   - Remote-SSH 연결 방법 완전 숙지

2. **모듈 분리 연습**:
   - 기존에 작성한 프로그램들을 기능별로 모듈 분리
   - 각 모듈에 적절한 문서화 추가
   - __init__.py 파일 활용한 패키지 구성

3. **실제 프로젝트 구조 연구**:
   - GitHub에서 오픈소스 파이썬 프로젝트 구조 분석
   - 대규모 프로젝트의 폴더 구조와 모듈 분리 방식 학습
   - 실무에서 사용하는 프로젝트 템플릿 연구

4. **파일 처리 시스템 구축**:
   - 다양한 형식(txt, csv, json, xml)의 파일 처리
   - 자동 백업 시스템 구현
   - 파일 암호화/복호화 기능 추가

5. **실습 과제 완성 및 확장**:
   - 개인 일기 관리 시스템에 이미지 첨부 기능 추가
   - 도서관 시스템에 대출 연체료 계산 기능 구현
   - 웹 인터페이스나 GUI 추가 연구

6. **예외 처리 강화**:
   - 모든 사용자 입력에 대한 검증 추가
   - 네트워크 연결, 데이터베이스 접근 등의 예외 처리
   - 로그 시스템 구현하여 오류 추적

7. **협업 환경 구축**:
   - Git을 활용한 버전 관리 시스템 구축
   - 팀 프로젝트를 위한 폴더 구조 설계
   - 코드 리뷰와 품질 관리 프로세스 학습

### 🔮 다음 주 예고

**10주차: 데이터 시각화와 코드 문서화**
- matplotlib와 pandas를 활용한 데이터 시각화
- 차트와 그래프로 데이터 표현하기
- 프로젝트 문서화와 코드 품질 관리
- 사용자 인터페이스 개선 방법

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
8주차: "객체지향으로 현실 세계를 프로그램으로 만들 수 있다!" (OOP) ✅
9주차: "모듈과 패키지로 대규모 시스템을 체계적으로 관리할 수 있다!" ✅
```

**오늘 여러분이 할 수 있게 된 것들:**
- 🐳 **Docker + VSCode 환경**: 실제 개발 현장과 동일한 환경에서 프로젝트 관리하기
- 🏗️ **시스템 설계**: 복잡한 프로그램을 모듈과 패키지로 체계적 구성하기
- 📁 **파일 관리**: 다양한 형식의 파일을 안전하게 읽고 쓰기
- 🔄 **데이터 영속성**: 프로그램 종료 후에도 데이터 유지하기
- 🛡️ **예외 처리**: 모든 상황에 대비한 안전한 프로그램 작성하기
- 📚 **코드 재사용**: 한 번 작성한 모듈을 여러 프로젝트에서 활용하기
- 🎯 **프로젝트 관리**: 실제 개발 현장과 같은 파일 구조 설계하기
- 💾 **백업 시스템**: 중요한 데이터의 안전한 보관과 복구
- 🔍 **디버깅**: 오류 상황을 예측하고 적절히 대응하기
- 🖥️ **통합 개발환경**: VSCode와 터미널을 활용한 효율적인 개발 워크플로

**개발환경 마스터의 진정한 가치:**
오늘 배운 Docker + VSCode 환경은 단순한 도구가 아닌, **실제 개발 현장의 표준 워크플로**입니다. 대부분의 기업에서 사용하는 개발 환경과 동일하므로, 여러분은 이미 현업 개발자와 같은 수준의 환경을 다룰 수 있게 되었습니다.

**모듈과 패키지의 진정한 가치:**
오늘 배운 모듈과 패키지 시스템은 단순한 기술이 아닌, **대규모 소프트웨어 개발의 핵심 원리**입니다. 이를 통해 Netflix, 카카오톡, 게임 같은 복잡한 시스템이 어떻게 구성되는지 이해할 수 있게 되었습니다.

**실무에서의 중요성:**
```python
# 실제 기업 시스템은 이런 구조를 가집니다
enterprise_system/
├── user_management/      # 사용자 관리
├── product_catalog/      # 상품 관리  
├── order_processing/     # 주문 처리
├── payment_gateway/      # 결제 시스템
├── notification_service/ # 알림 서비스
├── analytics/           # 데이터 분석
├── security/            # 보안 시스템
├── database/            # 데이터베이스
├── api/                 # API 서버
└── utils/               # 공통 유틸리티

# 각 패키지는 수십 개의 모듈을 포함하며,
# 수백 명의 개발자가 Docker + VSCode 환경에서 협업하여 개발합니다!
```

**개발 환경의 현실적 중요성:**
```bash
# 실제 개발팀에서는 이런 환경을 사용합니다
- Docker: 모든 개발자가 동일한 환경에서 작업
- VSCode + Remote-SSH: 클라우드 서버에서 원격 개발
- Git: 코드 버전 관리 및 팀 협업
- CI/CD: 자동 테스트 및 배포 파이프라인
- 모듈화된 코드: 팀원별 독립적인 개발 가능
```

**마지막 격려:**
모듈과 패키지를 마스터한 여러분은 이제 **진정한 소프트웨어 엔지니어**의 길에 들어섰습니다! 단순히 코드를 작성하는 것을 넘어서, 체계적이고 확장 가능한 시스템을 설계할 수 있는 능력을 갖추었어요.

**Docker + VSCode 환경**으로 실제 개발 현장과 동일한 경험을 쌓았고, **예외 처리와 파일 관리**를 통해 견고하고 신뢰할 수 있는 프로그램을 만들 수 있으며, **모듈과 패키지**를 통해 거대한 시스템도 체계적으로 관리할 수 있습니다.

이제 여러분은 **개발 환경 구축부터 대규모 시스템 설계까지** 모든 것을 다룰 수 있는 완전한 개발자가 되었습니다! 🌟

다음 주에는 이런 멋진 시스템들의 데이터를 시각적으로 표현하는 방법을 배워봅시다! 💪

---

**🎯 9주차 학습 완료! 수고하셨습니다! 🎉**