# 2주차: 개발 환경 실습 (Docker & Colab)
**총 강의시간: 3시간 20분 (200분)**
- 강의: 120분 (3부로 구성)
- 휴식: 20분 (10분씩 2회)
- 실습: 60분

---

## 🎯 1부: 코딩은 했는데... 어떤 컴퓨터에서 실행할까? (40분)

### 📌 핵심 개념 1: 지난 주 복습 - 우리가 해결한 문제 (10분)

#### 🔄 **1주차에서 우리가 알아낸 것들**

**문제 상황:**
1. 🤔 **사람**: 컴퓨터의 강력한 힘을 쓰고 싶다 (백만 번 계산을 5초에!)
2. 😅 **컴퓨터**: 사람의 말을 이해하지 못한다 (0과 1만 이해)
3. 💡 **해결책**: 사람이 컴퓨터 언어(파이썬)를 배워서 소통하자!

**우리가 배운 "알고리즘 스타일 말투":**
- **순차 스타일**: "이것 하고, 저것 하고, 그 다음 요것 해"
- **선택 스타일**: "만약 이러면 이것 하고, 아니면 저것 해"
- **반복 스타일**: "조건 만족할 때까지 계속해"

**우리가 만든 첫 번째 파이썬 코드들:**
```python
# 자기소개 프로그램 (순차 구조)
name = "김학생"
age = 20
print(f"안녕하세요! 제 이름은 {name}이고, 나이는 {age}살입니다.")

# 성적 판별 프로그램 (선택 구조)
score = 85
if score >= 90:
    print("A학점입니다!")
else:
    print("더 열심히 해봅시다!")

# 콜라츠 수열 (반복 구조)
number = 7
while number != 1:
    if number % 2 == 0:
        number = number // 2
    else:
        number = number * 3 + 1
    print(number)
```

**그런데 문제 발생!** 🤨

### 📌 핵심 개념 2: 새로운 문제 - 코드는 만들었는데 어디서 실행하지? (15분)

#### 💻 **코드를 실행할 컴퓨터가 필요하다!**

**현재 상황 분석:**
```
👤 우리: 파이썬 코드를 열심히 작성함 ✅
💾 코드: print("Hello Python!") ✅
❓ 실행환경: ??? 어디서 실행하지?
```

**다양한 선택지들과 문제점:**

**1. 내 개인 노트북/데스크탑**
- ✅ 장점: 내 컴퓨터니까 자유롭게 사용
- ❌ 단점: 
  - 파이썬 설치해야 함 (복잡!)
  - 운영체제마다 다름 (Windows/Mac/Linux)
  - 컴퓨터 고장나면 모든 코드 날아감
  - 다른 곳에서 작업하기 어려움

**2. 학교 컴퓨터실**
- ✅ 장점: 이미 설치되어 있을 수 있음
- ❌ 단점:
  - 언제나 사용할 수 없음
  - 내 파일 저장하기 어려움
  - 집에서 작업 불가능

#### 🌍 **현대적 해결 방법들**

**넷플릭스를 보는 방법 비교:**
```
예전 방식 (DVD):
1. 비디오 대여점 가기
2. DVD 빌리기  
3. 집에 가서 DVD 플레이어에 넣기
→ 번거롭고 제한적

현재 방식 (스트리밍):
1. 인터넷 연결
2. 넷플릭스 접속
3. 바로 시청
→ 편리하고 자유로움
```

**코딩 환경도 마찬가지:**
```
예전 방식 (로컬 설치):
1. 파이썬 다운로드
2. 설치 프로그램 실행
3. 환경 설정
→ 복잡하고 오류 많음

현재 방식 (클라우드):
1. 인터넷 연결
2. 웹사이트 접속
3. 바로 코딩
→ 간단하고 편리함
```

### 📌 핵심 개념 3: 두 가지 최적의 해결책 (15분)

#### ☁️ **해결책 1: Google Colab - "넷플릭스 같은 코딩 환경"**

**Google Colab이란?**
- 구글에서 만든 무료 온라인 파이썬 실행 환경
- 웹브라우저만 있으면 어디서든 사용 가능
- 구글 드라이브에 자동 저장

**장점들:**
```
✅ 설치 필요 없음: 브라우저만 있으면 OK
✅ 무료 사용: 구글 계정만 있으면 평생 무료
✅ 자동 저장: 구글 드라이브에 알아서 저장
✅ 어디서든 접속: 집, 학교, 카페 어디서든
```

#### 🐳 **해결책 2: Docker - "내 컴퓨터 안의 가상 컴퓨터"**

**아파트와 비슷한 개념:**
```
🏢 내 컴퓨터 = 아파트 건물
🏠 Docker 컨테이너 = 각각의 방
👤 파이썬 프로그램 = 방에 사는 사람

특징:
- 각 방은 독립적 (301호에서 일어나는 일이 501호에 영향 없음)
- 같은 건물이지만 각자 다른 환경
- 필요에 따라 방을 늘리거나 줄일 수 있음
```

**Docker 장점들:**
```
✅ 환경 통일: 모든 사람이 동일한 개발 환경 사용
✅ 격리성: 프로젝트별로 독립적인 환경
✅ 어디서든 동일: 어떤 컴퓨터에서든 동일하게 동작
```

---

## ☕ 휴식 시간 (10분)

---

## 🎯 2부: Google Colab으로 쉬운 파이썬 요리하기 (40분)

### 📌 Google Colab 시작하기 (15분)

#### 🚀 **Colab 접속하기 - 따라하기 단계**

**1단계: 구글 계정으로 로그인**
```
1. 웹브라우저 열기 (크롬, 사파리, 엣지 등)
2. https://colab.research.google.com 접속
3. 구글 계정으로 로그인
```

**2단계: 새 노트북 만들기**
```
1. "새 노트북" 클릭
2. 제목 변경: "파이썬 첫 실습.ipynb"
3. 자동으로 구글 드라이브에 저장됨
```

**3단계: 첫 번째 코드 실행해보기**
```python
# 첫 번째 셀에 입력할 코드
print("🎉 Google Colab에서 안녕하세요!")
print("파이썬이 제대로 동작하는지 확인해볼까요?")

# 간단한 계산
result = 5 + 3
print(f"5 + 3 = {result}")
```

**실행 방법:**
```
- Shift + Enter: 현재 셀 실행하고 다음 셀로 이동
- Ctrl + Enter: 현재 셀만 실행
- 왼쪽 재생 버튼 클릭
```

### 📌 Colab에서 1주차 복습하기 (25분)

#### 💻 **순차 구조 - 간단한 자기소개**

```python
# ===================================
# 🎯 나만의 자기소개 프로그램
# ===================================

print("🌟" * 15)
print("   자기소개 시간   ")
print("🌟" * 15)

# 기본 정보 (순차 구조)
name = "김파이썬"
age = 20
school = "한국대학교"
major = "컴퓨터공학과"

print(f"👤 이름: {name}")
print(f"🎂 나이: {age}살")
print(f"🏫 학교: {school}")
print(f"📚 전공: {major}")

# 간단한 계산
birth_year = 2024 - age
print(f"🗓️ 태어난 년도: {birth_year}년")

print("\n" + "🌟" * 15)
print("Google Colab에서 실행 성공! ✅")
print("🌟" * 15)
```

#### 🎯 **선택 구조 - 성적 판별하기**

```python
# ===================================
# 📊 성적 판별 프로그램
# ===================================

print("📚 성적 판별 시스템")
print("=" * 30)

# 과목별 점수
korean = 88
english = 92
math = 85

print(f"국어: {korean}점")
print(f"영어: {english}점")
print(f"수학: {math}점")

# 평균 계산
total = korean + english + math
average = total / 3

print(f"\n총점: {total}점")
print(f"평균: {average:.1f}점")

# 등급 판정 (선택 구조)
print(f"\n📋 등급 판정:")
if average >= 90:
    print("🏆 A학점 - 최우수!")
elif average >= 80:
    print("🎉 B학점 - 우수!")
elif average >= 70:
    print("👍 C학점 - 보통!")
else:
    print("💪 더 열심히 해봅시다!")

# 개별 과목 판정
print(f"\n📝 과목별 판정:")
if korean >= 90:
    print("국어: 잘했어요! 🎯")
else:
    print("국어: 조금 더 노력해요! 📚")

if english >= 90:
    print("영어: 잘했어요! 🎯")
else:
    print("영어: 조금 더 노력해요! 📚")

if math >= 90:
    print("수학: 잘했어요! 🎯")
else:
    print("수학: 조금 더 노력해요! 📚")
```

#### 🔄 **반복 구조 - 콜라츠 수열 만들기**

```python
# ===================================
# 🔢 콜라츠 수열 프로그램
# ===================================

print("🔢 콜라츠 수열 만들기")
print("=" * 30)

# 시작 숫자 설정
start_number = 7
number = start_number
step = 0

print(f"시작 숫자: {number}")
print(f"과정:")

# 콜라츠 수열 계산 (반복 구조)
while number != 1:
    step = step + 1
    
    if number % 2 == 0:  # 짝수인 경우
        number = number // 2
        print(f"{step}단계: {number} (짝수이므로 ÷2)")
    else:  # 홀수인 경우
        number = number * 3 + 1
        print(f"{step}단계: {number} (홀수이므로 ×3+1)")

print(f"\n🎯 완료!")
print(f"숫자 {start_number}에서 1까지 {step}단계 걸렸습니다!")

# 다른 숫자들도 테스트
print(f"\n🎮 다른 숫자들 테스트:")
test_numbers = [3, 5, 6, 9, 10]

for test_num in test_numbers:
    temp_number = test_num
    temp_steps = 0
    
    while temp_number != 1:
        temp_steps = temp_steps + 1
        if temp_number % 2 == 0:
            temp_number = temp_number // 2
        else:
            temp_number = temp_number * 3 + 1
    
    print(f"숫자 {test_num}: {temp_steps}단계")
```

#### 📊 **콜라츠 수열 간단한 시각화**

```python
# ===================================
# 📈 콜라츠 수열 시각화 (텍스트 버전)
# ===================================

print("📈 콜라츠 수열 시각화")
print("=" * 40)

# 시작 숫자
start_number = 13
number = start_number
sequence = [number]  # 수열을 저장할 리스트

print(f"시작 숫자: {number}")

# 콜라츠 수열 계산하면서 저장
while number != 1:
    if number % 2 == 0:
        number = number // 2
    else:
        number = number * 3 + 1
    sequence.append(number)

print(f"수열: {sequence}")
print(f"총 단계: {len(sequence) - 1}단계")

# 텍스트로 간단한 그래프 만들기
print(f"\n📊 텍스트 그래프:")
for i, num in enumerate(sequence):
    # 숫자의 크기에 따라 ★ 개수 조절
    stars = "★" * (num // 10 + 1)  # 10으로 나누어서 크기 조절
    print(f"{i:2d}단계: {num:3d} {stars}")

# 최대값과 최소값 찾기
max_value = max(sequence)
min_value = min(sequence)
max_position = sequence.index(max_value)

print(f"\n📊 통계:")
print(f"최대값: {max_value} ({max_position}단계에서)")
print(f"최소값: {min_value} (마지막)")
print(f"시작값의 {max_value / start_number:.1f}배까지 올라갔네요!")
```

#### 🎨 **Colab의 기본 시각화 기능**

```python
# ===================================
# 🎨 콜라츠 수열 그래프 그리기
# ===================================

# Colab에서 제공하는 기본 그래프 라이브러리 사용
import matplotlib.pyplot as plt

# 콜라츠 수열 데이터 (위에서 계산한 것)
start_number = 13
number = start_number
sequence = [number]

while number != 1:
    if number % 2 == 0:
        number = number // 2
    else:
        number = number * 3 + 1
    sequence.append(number)

# 단계별 번호 (x축)
steps = list(range(len(sequence)))

# 그래프 그리기
plt.figure(figsize=(10, 6))  # 그래프 크기 설정
plt.plot(steps, sequence, 'bo-', linewidth=2, markersize=6)
plt.title(f'콜라츠 수열 (시작: {start_number})', fontsize=16)
plt.xlabel('단계')
plt.ylabel('숫자 값')
plt.grid(True, alpha=0.3)  # 격자 표시

# 시작점과 끝점 강조
plt.plot(0, sequence[0], 'ro', markersize=10, label='시작')
plt.plot(len(sequence)-1, 1, 'go', markersize=10, label='끝')
plt.legend()

plt.show()

print(f"🎨 콜라츠 수열 그래프 완성!")
print(f"시작 숫자 {start_number}이 {len(sequence)-1}단계를 거쳐 1에 도달했습니다!")
```

---

## ☕ 휴식 시간 (10분)

---

## 🎯 3부: Docker로 나만의 파이썬 서버 만들기 (40분)

### 📌 Docker Desktop 설치하기 (10분)

#### 💻 **Docker Desktop이란?**

**Docker Desktop**: 윈도우, 맥, 리눅스에서 Docker를 쉽게 사용할 수 있게 해주는 프로그램
- 마치 "한글 워드"나 "포토샵" 같은 일반 프로그램처럼 설치
- 복잡한 명령어 없이 그래픽 인터페이스로 Docker 관리
- 무료로 사용 가능 (개인 용도)

#### 🪟 **Windows에서 Docker Desktop 설치하기**

**1단계: 시스템 요구사항 확인**
```
✅ Windows 10/11 (64bit)
✅ WSL 2 활성화 (Windows Subsystem for Linux)
✅ 하드웨어 가상화 지원 (대부분의 최신 컴퓨터에서 지원)
✅ 최소 4GB RAM (8GB 권장)
```

**2단계: Docker Desktop 다운로드**
```
1. 웹브라우저에서 https://www.docker.com/products/docker-desktop 접속
2. "Download for Windows" 버튼 클릭
3. "Docker Desktop Installer.exe" 파일 다운로드 (약 500MB)
```

**3단계: 설치 실행**
```
1. 다운로드한 "Docker Desktop Installer.exe" 파일 실행
2. 관리자 권한으로 실행 허용
3. "Use WSL 2 instead of Hyper-V" 옵션 체크 ✅
4. "Add shortcut to desktop" 옵션 체크 ✅  
5. "Install" 버튼 클릭
6. 설치 완료 후 재부팅 (필요시)
```

**4단계: Docker Desktop 실행 및 확인**
```
1. 바탕화면의 Docker Desktop 아이콘 더블클릭
2. 첫 실행 시 약간의 시간 소요 (Docker Engine 시작)
3. 시스템 트레이에 Docker 고래 아이콘 🐳 표시되면 성공!
4. 터미널(명령 프롬프트)에서 확인:
   docker --version
   → Docker version 24.0.x 같은 버전 정보가 나오면 설치 완료!
```

#### 🍎 **다른 운영체제에서 설치**

**Mac (macOS):**
```
1. https://www.docker.com/products/docker-desktop 접속
2. "Download for Mac" 선택
3. Intel Mac / Apple Silicon Mac 구분해서 다운로드
4. .dmg 파일 실행 후 Applications 폴더로 드래그
```

**Linux (Ubuntu 등):**
```
1. Docker Engine 설치 (명령어 방식)
2. 또는 Docker Desktop for Linux 설치
3. 배포판별로 설치 방법이 조금씩 다름
4. 공식 문서 참조: https://docs.docker.com/engine/install/
```

#### ⚠️ **설치 시 주의사항**

**Windows 사용자 주의점:**
```
❗ WSL 2가 설치되어 있지 않다면:
1. Windows 기능 켜기/끄기에서 "Linux용 Windows 하위 시스템" 활성화
2. Microsoft Store에서 "Windows Subsystem for Linux" 설치
3. 재부팅 후 Docker Desktop 재설치

❗ 가상화가 비활성화되어 있다면:
1. BIOS/UEFI 설정에서 Virtualization Technology 활성화
2. 컴퓨터마다 방법이 다르므로 "컴퓨터 모델 + 가상화 활성화" 검색

❗ 방화벽/백신 프로그램:
1. Docker Desktop을 신뢰할 수 있는 프로그램으로 설정
2. 필요시 일시적으로 방화벽 해제 후 설치
```

**설치 확인 명령어:**
```bash
# 터미널(CMD)에서 실행
docker --version          # Docker 버전 확인
docker run hello-world     # 테스트 컨테이너 실행

# 성공 시 출력:
# Hello from Docker!
# This message shows that your installation appears to be working correctly.
```

### 📌 Docker로 파이썬 환경 만들기 (15분)

#### 🐳 **Docker 기본 설정 - 복사 & 붙여넣기 가이드**

**1단계: Ubuntu 기반 컨테이너 생성**
```bash
# Ubuntu 최신 버전으로 컨테이너 생성 및 실행
docker run -it --name python-dev -p 22:22 -p 8888:8888 ubuntu:latest /bin/bash
```

**2단계: 기본 시스템 업데이트 및 필수 도구 설치**
```bash
# 패키지 목록 업데이트
apt update && apt upgrade -y

# 필수 도구들 설치
apt install -y wget curl vim nano sudo openssh-server python3 python3-pip git
```

**3단계: 개발용 사용자 계정 생성**
```bash
# 새 사용자 'pydev' 생성
useradd -m -s /bin/bash pydev

# 사용자에게 sudo 권한 부여
usermod -aG sudo pydev

# 비밀번호 설정 (예: python123)
echo 'pydev:python123' | chpasswd

# 사용자 홈 디렉토리로 이동
su - pydev
cd /home/pydev
```

**4단계: SSH 서버 설정**
```bash
# SSH 설정 파일 수정 (root로 전환)
exit  # pydev에서 root로 돌아가기

# SSH 설정 파일 편집
cat >> /etc/ssh/sshd_config << 'EOF'
Port 22
PermitRootLogin yes
PasswordAuthentication yes
PubkeyAuthentication yes
EOF

# SSH 서비스 시작
service ssh start
```

### 📌 Python 개발환경 구성 (15분)

#### 🐍 **Anaconda 설치 및 설정**

**1단계: Anaconda 다운로드 및 설치**
```bash
# pydev 사용자로 전환
su - pydev
cd /home/pydev

# Anaconda 다운로드
wget https://repo.anaconda.com/archive/Anaconda3-2024.02-1-Linux-x86_64.sh

# 설치 권한 부여 및 설치
chmod +x Anaconda3-2024.02-1-Linux-x86_64.sh
./Anaconda3-2024.02-1-Linux-x86_64.sh -b

# PATH 환경변수 설정
echo 'export PATH="/home/pydev/anaconda3/bin:$PATH"' >> ~/.bashrc
source ~/.bashrc
```

**2단계: Jupyter Notebook 설정**
```bash
# Jupyter 설정 디렉토리 생성
/home/pydev/anaconda3/bin/jupyter notebook --generate-config

# 간단한 Jupyter 설정
cat > /home/pydev/.jupyter/jupyter_notebook_config.py << 'EOF'
c.NotebookApp.ip = '0.0.0.0'
c.NotebookApp.port = 8888
c.NotebookApp.open_browser = False
c.NotebookApp.token = 'python123'
c.NotebookApp.notebook_dir = '/home/pydev/notebooks'
EOF

# 노트북 저장용 디렉토리 생성
mkdir -p /home/pydev/notebooks
```

**3단계: 간단한 테스트 스크립트 생성**
```bash
# 테스트용 Python 스크립트 생성
cat > /home/pydev/test_python.py << 'EOF'
print("🐍 Docker에서 파이썬 테스트")
print("=" * 30)

# 간단한 계산
numbers = [1, 2, 3, 4, 5]
total = sum(numbers)
average = total / len(numbers)

print(f"숫자들: {numbers}")
print(f"합계: {total}")
print(f"평균: {average}")

# 콜라츠 수열 테스트
print(f"\n🔢 콜라츠 수열 테스트 (시작: 7)")
number = 7
steps = 0
while number != 1:
    steps += 1
    if number % 2 == 0:
        number = number // 2
    else:
        number = number * 3 + 1
    print(f"{steps}단계: {number}")

print(f"\n✅ Docker 환경에서 파이썬 실행 성공!")
EOF

# 스크립트 실행 권한 부여 및 테스트
chmod +x /home/pydev/test_python.py
python3 /home/pydev/test_python.py
```

**4단계: 자동 시작 스크립트 생성**
```bash
# root 사용자로 전환
exit

# 컨테이너 시작 시 자동 실행 스크립트 생성
cat > /start-services.sh << 'EOF'
#!/bin/bash
echo "🚀 Python 개발 서버 시작 중..."

# SSH 서비스 시작
service ssh start
echo "✅ SSH 서버 시작 완료 (포트 22)"

# Jupyter Notebook 시작
su - pydev -c "cd /home/pydev/notebooks && /home/pydev/anaconda3/bin/jupyter notebook --config=/home/pydev/.jupyter/jupyter_notebook_config.py" &
echo "✅ Jupyter Notebook 시작 완료 (포트 8888)"

echo "🎉 모든 서비스 시작 완료!"
echo "📡 SSH 접속: ssh pydev@localhost -p 22"
echo "🌐 Jupyter 접속: http://localhost:8888"

# 컨테이너가 종료되지 않도록 대기
tail -f /dev/null
EOF

chmod +x /start-services.sh
```

**5단계: 컨테이너를 이미지로 저장하기**
```bash
# 현재 컨테이너에서 나가기
exit

# 컨테이너 정지
docker stop python-dev

# 컨테이너를 이미지로 저장
docker commit python-dev python-dev-env:v1.0

# 저장된 이미지로 새 컨테이너 실행
docker run -d --name python-server -p 22:22 -p 8888:8888 python-dev-env:v1.0 /start-services.sh
```

---

## 🎯 실습 시간 (60분)

### 🎯 실습 과제 1: Google Colab에서 1주차 복습하기 (20분)

**목표**: Colab에서 1주차 내용을 더 재미있게 만들어보기

**과제: 나만의 계산기 만들기**

```python
# ===============================================
# 🧮 나만의 계산기 프로그램
# ===============================================

print("🧮 나만의 계산기")
print("=" * 30)

# 기본 계산 (순차 구조)
num1 = 15
num2 = 7

print(f"첫 번째 숫자: {num1}")
print(f"두 번째 숫자: {num2}")
print()

# 사칙연산 결과
plus_result = num1 + num2
minus_result = num1 - num2
multiply_result = num1 * num2
divide_result = num1 / num2

print(f"덧셈: {num1} + {num2} = {plus_result}")
print(f"뺄셈: {num1} - {num2} = {minus_result}")
print(f"곱셈: {num1} × {num2} = {multiply_result}")
print(f"나눗셈: {num1} ÷ {num2} = {divide_result:.2f}")

# 결과 판정 (선택 구조)
print(f"\n📊 결과 분석:")
if plus_result > 20:
    print("덧셈 결과가 20보다 크네요! 🎯")
else:
    print("덧셈 결과가 20 이하입니다.")

if multiply_result > 100:
    print("곱셈 결과가 100보다 크네요! 🚀")
else:
    print("곱셈 결과가 100 이하입니다.")

# 구구단 만들기 (반복 구조)
print(f"\n📚 {num2}단 구구단:")
for i in range(1, 10):
    result = num2 * i
    print(f"{num2} × {i} = {result}")

print(f"\n🎉 계산기 프로그램 완료!")
```

**응용 과제: 여러 숫자로 실험하기**
```python
# 다양한 숫자들로 테스트
print("🎮 여러 숫자 테스트")
print("=" * 25)

test_numbers = [3, 8, 12, 25]

for number in test_numbers:
    print(f"\n숫자 {number}:")
    print(f"  2배: {number * 2}")
    print(f"  제곱: {number * number}")
    
    # 짝수/홀수 판별
    if number % 2 == 0:
        print(f"  {number}는 짝수입니다! 🎯")
    else:
        print(f"  {number}는 홀수입니다! ⚡")
```

### 🎯 실습 과제 2: Docker에서 간단한 파이썬 프로그래밍 (20분)

**목표**: Docker 컨테이너에서 SSH로 접속하여 파이썬 코딩하기

**SSH 접속 후 실행할 프로그램:**

```python
#!/usr/bin/env python3
"""
간단한 Docker 파이썬 실습
"""

print("🐳 Docker 컨테이너에서 파이썬 실습")
print("=" * 40)

# 1. 기본 정보 출력
import os
import datetime

print(f"👤 현재 사용자: {os.getenv('USER')}")
print(f"📅 현재 시간: {datetime.datetime.now()}")
print(f"📂 현재 경로: {os.getcwd()}")

# 2. 간단한 게임 - 숫자 맞추기
print(f"\n🎮 숫자 맞추기 게임")
print("-" * 25)

secret_number = 7  # 비밀 숫자
print("1부터 10 사이의 숫자를 하나 생각했어요!")

# 몇 가지 숫자로 테스트
guesses = [3, 7, 9]

for guess in guesses:
    print(f"\n추측: {guess}")
    
    if guess == secret_number:
        print("🎉 정답입니다! 축하해요!")
        break
    elif guess < secret_number:
        print("📈 더 큰 숫자입니다!")
    else:
        print("📉 더 작은 숫자입니다!")

# 3. 콜라츠 수열 한 번 더
print(f"\n🔢 콜라츠 수열 (시작: 5)")
number = 5
step = 0

while number != 1:
    step += 1
    if number % 2 == 0:
        number = number // 2
        print(f"{step}단계: {number} (÷2)")
    else:
        number = number * 3 + 1
        print(f"{step}단계: {number} (×3+1)")

print(f"\n✅ {step}단계 만에 완료!")

# 4. 파일 만들어보기
filename = "docker_memo.txt"
memo_content = f"""Docker 실습 메모
작성 시간: {datetime.datetime.now()}
작성 장소: Docker 컨테이너

오늘 배운 것:
1. Google Colab 사용법
2. Docker 컨테이너 만들기
3. SSH로 원격 접속하기
4. 파이썬으로 파일 만들기

다음에 해볼 것:
- 더 복잡한 프로그램 만들기
- Jupyter Notebook 활용하기
"""

with open(filename, 'w', encoding='utf-8') as f:
    f.write(memo_content)

print(f"\n📝 파일 '{filename}' 생성 완료!")
print("파일 내용을 확인해보세요:")
print(f"cat {filename}")

print(f"\n🎉 Docker 실습 완료!")
```

### 🎯 실습 과제 3: Jupyter Notebook에서 시각화하기 (20분)

**목표**: Docker의 Jupyter Notebook에서 콜라츠 수열 시각화하기

브라우저에서 `http://localhost:8888` 접속 (토큰: python123)

**첫 번째 셀: 기본 설정**
```python
print("📊 Jupyter Notebook에서 콜라츠 수열 시각화")
print("Docker 컨테이너 + Jupyter = 완벽한 조합! 🎉")

import matplotlib.pyplot as plt
```

**두 번째 셀: 콜라츠 수열 계산**
```python
# 콜라츠 수열 계산 함수
def calculate_collatz(start_num):
    sequence = [start_num]
    number = start_num
    
    while number != 1:
        if number % 2 == 0:
            number = number // 2
        else:
            number = number * 3 + 1
        sequence.append(number)
    
    return sequence

# 여러 숫자로 테스트
test_numbers = [3, 5, 7, 9, 11]
print("🔢 각 숫자의 콜라츠 수열 길이:")

for num in test_numbers:
    seq = calculate_collatz(num)
    print(f"숫자 {num}: {len(seq)-1}단계")
```

**세 번째 셀: 시각화**
```python
# 콜라츠 수열 시각화
start_num = 13
sequence = calculate_collatz(start_num)
steps = list(range(len(sequence)))

# 그래프 그리기
plt.figure(figsize=(12, 6))

# 첫 번째 그래프: 수열 변화
plt.subplot(1, 2, 1)
plt.plot(steps, sequence, 'bo-', linewidth=2, markersize=4)
plt.title(f'콜라츠 수열 변화 (시작: {start_num})')
plt.xlabel('단계')
plt.ylabel('숫자 값')
plt.grid(True, alpha=0.3)

# 두 번째 그래프: 단계 수 비교
plt.subplot(1, 2, 2)
numbers = [3, 5, 7, 9, 11, 13]
step_counts = []

for num in numbers:
    seq = calculate_collatz(num)
    step_counts.append(len(seq) - 1)

plt.bar(numbers, step_counts, color='skyblue', alpha=0.7)
plt.title('시작 숫자별 단계 수')
plt.xlabel('시작 숫자')
plt.ylabel('단계 수')

# 막대 위에 숫자 표시
for i, count in enumerate(step_counts):
    plt.text(numbers[i], count + 0.5, str(count), ha='center')

plt.tight_layout()
plt.show()

print(f"🎨 콜라츠 수열 시각화 완성!")
print(f"Docker + Jupyter + 파이썬 = 완벽한 개발환경! 🚀")
```

---

## 📚 오늘 배운 내용 정리

### ✅ 핵심 포인트

1. **개발환경의 중요성**: 
   - 코드를 작성했지만 실행할 컴퓨터가 필요함
   - 설치와 설정의 복잡성 해결

2. **Google Colab 활용**: 
   - ☁️ 무료 클라우드 파이썬 환경
   - 브라우저만으로 즉시 코딩 가능
   - 1주차 내용을 더 쉽고 재미있게 복습

3. **Docker 컨테이너 구축**: 
   - 🐳 가상화 기술로 독립적인 개발 환경
   - SSH 원격 접속으로 전문적인 개발 경험
   - Jupyter Notebook으로 시각화까지

4. **1주차 내용 심화**:
   - 순차, 선택, 반복 구조를 실제 환경에서 활용
   - 콜라츠 수열의 간단한 시각화
   - 텍스트 기반 그래프와 실제 그래프 비교

### 🏠 다음 주까지 해볼 과제

1. **Colab 연습**:
   - 자기소개 프로그램에 더 많은 정보 추가하기
   - 다양한 숫자로 콜라츠 수열 실험하기
   - 간단한 계산기 기능 더 추가하기

2. **Docker 활용**:
   - SSH로 매일 접속해서 간단한 코딩 연습
   - 새로운 파이썬 파일 만들어보기
   - Jupyter Notebook으로 학습 노트 작성

3. **두 환경 비교**:
   - 같은 프로그램을 두 환경에서 실행해보기
   - 어떤 상황에서 어떤 환경이 더 좋은지 생각해보기

### 🔮 다음 주 예고

**3주차: 변수와 자료형 심화 및 연산자 활용 규칙**
- 변수 이름 잘 짓는 방법 (네이밍 컨벤션)
- 다양한 자료형의 특징과 활용
- 문자열 다루기의 모든 것
- 코드를 아름답게 만드는 PEP 8 스타일

### 💡 마지막 정리

오늘 여러분은 정말 큰 발전을 이뤘습니다! 🎉

**발전 과정:**
```
1주차: "프로그래밍이 뭔지 알았다!"
2주차: "어디서든 코딩할 수 있게 되었다!"
```

이제 여러분은:
- ☁️ Google Colab에서 언제든 코딩할 수 있고
- 🐳 Docker로 전문적인 개발환경을 만들 수 있습니다

**실제로 할 수 있게 된 것들:**
- 집에서 Colab으로 즉석 코딩 ✨
- 카페에서 노트북으로 Docker 개발 💻  
- 친구들과 코드 공유하기 📤
- SSH로 원격 서버 접속하기 🔐

가장 중요한 것은 **매일 조금씩이라도 코딩하는 것**입니다.
Colab이나 Docker에서 간단한 프로그램이라도 만들어보세요.

다음 주에는 더 예쁘고 읽기 쉬운 코드를 작성하는 방법을 배워보겠습니다! 🚀