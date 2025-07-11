# 10주차: 데이터 시각화와 코드 문서화
**총 강의시간: 3시간 20분 (200분)**
- 강의: 120분 (3부로 구성)
- 휴식: 20분 (10분씩 2회)
- 실습: 60분

---

## 🎯 1부: 데이터 시각화의 필요성과 matplotlib 기초 (40분)

### 📌 핵심 개념 1: 지금까지의 여정과 새로운 도전 (8분)

#### 🔄 **우리가 정복한 프로그래밍의 세계**

**1-9주차 완주! 완전한 프로그래머로 성장** ✅
```
1주차: "프로그래밍이 뭔지 알았다!" (기본 구조) ✅
2주차: "어디서든 코딩할 수 있게 되었다!" (개발환경) ✅
3주차: "변수로 복잡한 문제를 해결할 수 있다!" (자료형) ✅
4주차: "조건문으로 똑똑한 프로그램을 만들 수 있다!" (선택구조) ✅
5주차: "반복문으로 효율적인 프로그램을 만들 수 있다!" (반복구조) ✅
6주차: "자료구조로 체계적인 데이터 관리를 할 수 있다!" (컬렉션) ✅
7주차: "함수로 재사용 가능한 코드를 만들 수 있다!" (모듈화) ✅
8주차: "객체지향으로 현실 세계를 프로그램으로 만들 수 있다!" (OOP) ✅
9주차: "모듈과 패키지로 대규모 시스템을 체계적으로 관리할 수 있다!" (구조화) ✅
```

**오늘 해결할 문제**: 
복잡한 데이터를 어떻게 한눈에 알아볼 수 있게 시각적으로 표현할 수 있을까? 내가 작성한 코드를 다른 사람들이 쉽게 이해할 수 있도록 문서화하려면 어떻게 해야 할까?

#### 📊 **데이터의 힘 vs 시각화의 마법**

**예시: 학급별 성적 데이터 분석**

```python
# 😰 숫자만 봐서는... (이해하기 어렵다!)
class_scores = {
    "1반": [85, 92, 78, 96, 88, 84, 91, 87, 93, 89],
    "2반": [89, 76, 93, 81, 87, 90, 85, 88, 79, 92],
    "3반": [82, 95, 77, 90, 84, 86, 89, 83, 94, 91],
    "4반": [78, 88, 85, 79, 91, 87, 82, 90, 86, 93],
    "5반": [94, 89, 96, 85, 92, 88, 91, 87, 90, 84]
}

# 평균 계산
for class_name, scores in class_scores.items():
    average = sum(scores) / len(scores)
    print(f"{class_name} 평균: {average:.1f}점")

# 출력:
# 1반 평균: 88.3점
# 2반 평균: 86.0점
# 3반 평균: 87.1점
# 4반 평균: 85.9점
# 5반 평균: 89.6점

# 🤔 어느 반이 가장 잘했는지? 성적 분포는 어떤지? 한눈에 알기 어렵다!
```

#### 🎨 **시각화의 마법 - 한 그래프가 천 마디 말보다 강하다**

```python
# ✅ 시각화로 표현하면 한눈에!
import matplotlib.pyplot as plt

# 데이터 준비
classes = list(class_scores.keys())
averages = [sum(scores)/len(scores) for scores in class_scores.values()]

# 막대그래프로 시각화
plt.figure(figsize=(10, 6))
bars = plt.bar(classes, averages, color=['#FF6B6B', '#4ECDC4', '#45B7D1', '#96CEB4', '#FECA57'])

# 그래프 꾸미기
plt.title('학급별 평균 성적 비교', fontsize=16, fontweight='bold')
plt.xlabel('학급', fontsize=12)
plt.ylabel('평균 점수', fontsize=12)
plt.ylim(80, 95)

# 각 막대 위에 수치 표시
for bar, avg in zip(bars, averages):
    plt.text(bar.get_x() + bar.get_width()/2, bar.get_height() + 0.5, 
             f'{avg:.1f}', ha='center', va='bottom', fontweight='bold')

plt.grid(axis='y', alpha=0.3)
plt.tight_layout()
plt.show()

# 🎉 이제 한눈에! 5반이 1등, 4반이 꼴찌, 전체적으로 고른 분포!
```

### 📌 핵심 개념 2: 시각화 환경 비교 - Docker vs Colab (15분)

#### 🐳 **Docker 환경에서의 시각화**

**Docker 환경의 특징:**
```bash
# Docker 컨테이너에서 matplotlib 설치 및 설정
FROM python:3.9

# 필요한 패키지 설치
RUN pip install matplotlib pandas numpy jupyter

# GUI 백엔드 설정 (X11 forwarding 필요)
ENV DISPLAY=:0

# 한글 폰트 설치 (Linux 환경)
RUN apt-get update && apt-get install -y fonts-noto-cjk

# Jupyter 실행
CMD ["jupyter", "notebook", "--ip=0.0.0.0", "--allow-root"]
```

**Docker 환경의 장점:**
- ✅ **완전한 개발 환경**: 실제 서버 환경과 동일
- ✅ **버전 일치**: 모든 개발자가 동일한 환경
- ✅ **패키지 충돌 없음**: 격리된 환경에서 안전한 개발
- ✅ **배포 용이**: 개발 환경 그대로 배포 가능

**Docker 환경의 단점:**
- ❌ **복잡한 설정**: 초기 환경 구축이 어려움
- ❌ **GUI 제약**: 그래프 출력을 위한 추가 설정 필요
- ❌ **자원 사용**: 시스템 리소스를 많이 사용
- ❌ **학습 곡선**: Docker 자체를 배워야 함

#### ☁️ **Google Colab 환경에서의 시각화**

**Colab 환경의 특징:**
```python
# Colab에서는 바로 실행 가능!
import matplotlib.pyplot as plt
import pandas as pd
import numpy as np

# 한글 폰트 설정 (Colab 전용)
!apt-get update -qq
!apt-get install fonts-noto-cjk -qq
import matplotlib.font_manager as fm
fontpath = '/usr/share/fonts/truetype/noto/NotoSansCJK-Regular.ttc'
font = fm.FontProperties(fname=fontpath, size=10)
plt.rcParams['font.family'] = font.get_name()

# 즉시 그래프 출력!
plt.plot([1, 2, 3, 4], [1, 4, 2, 3])
plt.title('테스트 그래프')
plt.show()
```

**Colab 환경의 장점:**
- ✅ **즉시 시작**: 브라우저만 있으면 바로 시작
- ✅ **무료 GPU**: 고성능 컴퓨팅 자원 무료 제공
- ✅ **쉬운 공유**: 링크 하나로 코드 공유
- ✅ **자동 저장**: Google Drive에 자동 백업

**Colab 환경의 단점:**
- ❌ **세션 제한**: 12시간 후 자동 종료
- ❌ **네트워크 의존**: 인터넷 연결 필수
- ❌ **제한된 커스터마이징**: 환경 설정에 제약
- ❌ **데이터 접근 제약**: 로컬 파일 접근 어려움

#### 🎯 **환경별 추천 사용 시나리오**

**Docker 환경 추천:**
```python
# 이런 경우에는 Docker가 좋습니다!
scenarios_for_docker = [
    "대규모 프로젝트 개발",
    "팀 협업이 중요한 프로젝트",
    "실제 서비스 배포 예정",
    "고도의 커스터마이징 필요",
    "보안이 중요한 기업 환경"
]
```

**Colab 환경 추천:**
```python
# 이런 경우에는 Colab이 좋습니다!
scenarios_for_colab = [
    "빠른 프로토타이핑",
    "교육 및 학습 목적",
    "데이터 분석 및 시각화",
    "머신러닝 실험",
    "간단한 개인 프로젝트"
]
```

### 📌 핵심 개념 3: matplotlib 기초와 코딩 규칙 (17분)

#### 📈 **matplotlib의 기본 구조 이해**

**알고리즘 말투로 그래프 그리기 과정 표현:**
1. "필요한 라이브러리를 불러온다"
2. "데이터를 준비한다"
3. "그래프의 크기와 스타일을 설정한다"
4. "데이터를 그래프로 그린다"
5. "제목, 축 레이블, 범례 등을 추가한다"
6. "그래프를 화면에 출력한다"

#### 🎯 **흥미로운 실습: 나의 일주일 생활 패턴 시각화**

**문제**: 사용자로부터 일주일간의 생활 데이터를 입력받아 다양한 그래프로 시각화하기

**1단계: 데이터 수집 및 준비**

```python
import matplotlib.pyplot as plt
import numpy as np

# 한글 폰트 설정 (Windows 환경 기준)
plt.rcParams['font.family'] = 'Malgun Gothic'
plt.rcParams['axes.unicode_minus'] = False

def collect_weekly_data():
    """
    사용자로부터 일주일간의 생활 데이터를 입력받는 함수
    
    알고리즘:
    1. 요일별로 반복하며 데이터 입력받기
    2. 각 요일마다 수면시간, 공부시간, 운동시간 입력
    3. 입력받은 데이터를 딕셔너리로 구조화
    4. 검증된 데이터 반환
    """
    days = ['월요일', '화요일', '수요일', '목요일', '금요일', '토요일', '일요일']
    
    # 데이터 저장할 딕셔너리 초기화
    weekly_data = {
        'days': days,
        'sleep_hours': [],
        'study_hours': [],
        'exercise_minutes': []
    }
    
    print("🗓️ 일주일간의 생활 패턴을 입력해주세요!")
    print("=" * 50)
    
    for day in days:
        print(f"\n📅 {day} 데이터 입력:")
        
        # 수면시간 입력 (검증 포함)
        while True:
            try:
                sleep = float(input(f"  🛏️  수면시간 (시간): "))
                if 0 <= sleep <= 24:
                    weekly_data['sleep_hours'].append(sleep)
                    break
                else:
                    print("     ❌ 0-24 시간 사이로 입력해주세요.")
            except ValueError:
                print("     ❌ 숫자로 입력해주세요.")
        
        # 공부시간 입력 (검증 포함)
        while True:
            try:
                study = float(input(f"  📚 공부시간 (시간): "))
                if 0 <= study <= 24:
                    weekly_data['study_hours'].append(study)
                    break
                else:
                    print("     ❌ 0-24 시간 사이로 입력해주세요.")
            except ValueError:
                print("     ❌ 숫자로 입력해주세요.")
        
        # 운동시간 입력 (검증 포함)
        while True:
            try:
                exercise = int(input(f"  🏃 운동시간 (분): "))
                if 0 <= exercise <= 1440:  # 24시간 = 1440분
                    weekly_data['exercise_minutes'].append(exercise)
                    break
                else:
                    print("     ❌ 0-1440 분 사이로 입력해주세요.")
            except ValueError:
                print("     ❌ 숫자로 입력해주세요.")
    
    return weekly_data

# 데이터 수집
user_data = collect_weekly_data()
```

**2단계: 다양한 그래프로 시각화**

```python
def create_comprehensive_visualization(data):
    """
    수집된 데이터를 다양한 그래프로 시각화하는 함수
    
    알고리즘:
    1. 전체 화면을 2×2 격자로 나누어 4개 그래프 배치
    2. 각 그래프마다 다른 시각화 방법 적용
    3. 색상과 스타일을 통일성 있게 설정
    4. 데이터의 특성에 맞는 그래프 타입 선택
    """
    
    # 전체 화면 설정
    fig, ((ax1, ax2), (ax3, ax4)) = plt.subplots(2, 2, figsize=(15, 12))
    fig.suptitle('🗓️ 나의 일주일 생활 패턴 분석', fontsize=20, fontweight='bold')
    
    days = data['days']
    sleep_hours = data['sleep_hours']
    study_hours = data['study_hours']
    exercise_minutes = data['exercise_minutes']
    
    # 색상 팔레트 설정
    colors = ['#FF6B6B', '#4ECDC4', '#45B7D1', '#96CEB4', '#FECA57', '#FF9F43', '#A55EEA']
    
    # 그래프 1: 수면시간 막대그래프
    bars1 = ax1.bar(days, sleep_hours, color=colors, alpha=0.8)
    ax1.set_title('😴 일별 수면시간', fontsize=14, fontweight='bold')
    ax1.set_ylabel('시간 (hour)', fontsize=12)
    ax1.set_ylim(0, max(sleep_hours) + 2)
    
    # 평균선 추가
    avg_sleep = np.mean(sleep_hours)
    ax1.axhline(y=avg_sleep, color='red', linestyle='--', alpha=0.7, 
                label=f'평균: {avg_sleep:.1f}시간')
    ax1.legend()
    
    # 막대 위에 수치 표시
    for bar, hour in zip(bars1, sleep_hours):
        ax1.text(bar.get_x() + bar.get_width()/2, bar.get_height() + 0.1,
                f'{hour:.1f}h', ha='center', va='bottom', fontweight='bold')
    
    # 그래프 2: 공부시간 꺾은선그래프
    ax2.plot(days, study_hours, marker='o', linewidth=3, markersize=8, 
             color='#45B7D1', markerfacecolor='white', markeredgewidth=2)
    ax2.fill_between(days, study_hours, alpha=0.3, color='#45B7D1')
    ax2.set_title('📚 일별 공부시간 추이', fontsize=14, fontweight='bold')
    ax2.set_ylabel('시간 (hour)', fontsize=12)
    ax2.grid(True, alpha=0.3)
    ax2.set_ylim(0, max(study_hours) + 1)
    
    # 그래프 3: 운동시간 원그래프
    total_exercise = sum(exercise_minutes)
    exercise_percentages = [minutes/total_exercise*100 for minutes in exercise_minutes]
    
    # 0인 데이터는 제외하고 그래프 그리기
    non_zero_days = []
    non_zero_percentages = []
    non_zero_colors = []
    
    for i, (day, percentage) in enumerate(zip(days, exercise_percentages)):
        if exercise_minutes[i] > 0:
            non_zero_days.append(f"{day}\n({exercise_minutes[i]}분)")
            non_zero_percentages.append(percentage)
            non_zero_colors.append(colors[i])
    
    if non_zero_percentages:  # 운동한 날이 있는 경우에만
        wedges, texts, autotexts = ax3.pie(non_zero_percentages, labels=non_zero_days, 
                                          colors=non_zero_colors, autopct='%1.1f%%',
                                          startangle=90, textprops={'fontsize': 10})
        ax3.set_title('🏃 주간 운동시간 분포', fontsize=14, fontweight='bold')
    else:
        ax3.text(0.5, 0.5, '이번 주는\n운동을 안 했네요! 😅', 
                ha='center', va='center', transform=ax3.transAxes,
                fontsize=16, bbox=dict(boxstyle="round,pad=0.3", facecolor="lightgray"))
        ax3.set_title('🏃 주간 운동시간 분포', fontsize=14, fontweight='bold')
    
    # 그래프 4: 종합 분석 - 생활 패턴 레이더 차트
    # 각 요일별 생활 건강도 점수 계산
    health_scores = []
    for i in range(7):
        # 수면: 7-9시간이 최적 (최대 30점)
        sleep_score = 30 - abs(sleep_hours[i] - 8) * 5
        sleep_score = max(0, min(30, sleep_score))
        
        # 공부: 많을수록 좋음 (최대 35점, 8시간 기준)
        study_score = min(35, study_hours[i] * 4.375)
        
        # 운동: 30분 이상이 최적 (최대 35점)
        exercise_score = min(35, exercise_minutes[i] / 30 * 35)
        
        total_score = sleep_score + study_score + exercise_score
        health_scores.append(total_score)
    
    bars4 = ax4.bar(days, health_scores, color=colors, alpha=0.8)
    ax4.set_title('🌟 일별 생활 건강도 점수', fontsize=14, fontweight='bold')
    ax4.set_ylabel('점수 (0-100)', fontsize=12)
    ax4.set_ylim(0, 100)
    
    # 점수별 등급 표시
    for bar, score in zip(bars4, health_scores):
        if score >= 80:
            grade = "A+"
            color = "green"
        elif score >= 70:
            grade = "A"
            color = "blue"
        elif score >= 60:
            grade = "B"
            color = "orange"
        else:
            grade = "C"
            color = "red"
        
        ax4.text(bar.get_x() + bar.get_width()/2, bar.get_height() + 1,
                f'{score:.0f}\n({grade})', ha='center', va='bottom', 
                fontweight='bold', color=color)
    
    # 그래프 간격 조정
    plt.tight_layout()
    
    # 전체 통계 출력
    print(f"\n📊 일주일 생활 패턴 분석 결과:")
    print(f"=" * 50)
    print(f"🛏️  평균 수면시간: {np.mean(sleep_hours):.1f}시간")
    print(f"📚 평균 공부시간: {np.mean(study_hours):.1f}시간")
    print(f"🏃 총 운동시간: {sum(exercise_minutes)}분")
    print(f"🌟 평균 건강도 점수: {np.mean(health_scores):.1f}점")
    
    # 개선 제안
    avg_health = np.mean(health_scores)
    if avg_health >= 80:
        print(f"🎉 훌륭한 생활 패턴입니다! 계속 유지하세요!")
    elif avg_health >= 70:
        print(f"👍 좋은 생활 패턴이네요! 조금만 더 노력하면 완벽!")
    elif avg_health >= 60:
        print(f"💪 보통 수준입니다. 수면과 운동을 늘려보세요!")
    else:
        print(f"😅 생활 패턴 개선이 필요해요. 규칙적인 생활을 시작해봅시다!")
    
    plt.show()

# 시각화 실행
create_comprehensive_visualization(user_data)
```

---

## ☕ 휴식 시간 (10분)

---

## 🎯 2부: pandas를 활용한 데이터 분석과 시각화 (40분)

### 📌 핵심 개념 1: pandas 기초와 데이터 구조 (15분)

#### 📋 **pandas의 핵심 개념**

**pandas = Python Data Analysis Library**
- 구조화된 데이터를 쉽게 처리할 수 있는 도구
- Excel과 비슷하지만 프로그래밍으로 조작 가능
- 대용량 데이터도 빠르게 처리

**알고리즘 말투로 pandas 데이터 처리 과정 표현:**
1. "데이터를 DataFrame(표) 형태로 불러온다"
2. "데이터의 구조와 내용을 파악한다"
3. "필요한 데이터만 선택하거나 조건으로 필터링한다"
4. "데이터를 그룹화하고 집계한다"
5. "결과를 그래프로 시각화한다"

#### 🎯 **흥미로운 실습: 우리 반 학생들의 취미 통계**

```python
import pandas as pd
import matplotlib.pyplot as plt

def create_hobby_survey():
    """
    사용자로부터 학생들의 취미 데이터를 입력받아 DataFrame 생성
    
    알고리즘:
    1. 학생 수 입력받기
    2. 각 학생별로 이름, 나이, 취미, 주간 활동시간 입력
    3. 입력된 데이터를 DataFrame으로 구조화
    4. 기본 통계 정보 출력
    """
    
    print("🎭 우리 반 취미 조사를 시작합니다!")
    print("=" * 50)
    
    # 학생 수 입력
    while True:
        try:
            num_students = int(input("조사할 학생 수를 입력하세요 (3-20명): "))
            if 3 <= num_students <= 20:
                break
            else:
                print("3명 이상 20명 이하로 입력해주세요.")
        except ValueError:
            print("숫자로 입력해주세요.")
    
    # 데이터 수집
    students_data = []
    
    # 미리 정의된 취미 목록 (선택의 일관성을 위해)
    hobby_options = [
        "독서", "영화감상", "음악듣기", "게임", "운동", 
        "요리", "그림그리기", "사진촬영", "여행", "춤추기",
        "악기연주", "영어공부", "코딩", "블로그쓰기", "쇼핑"
    ]
    
    print(f"\n📝 {num_students}명의 학생 정보를 입력해주세요:")
    print("취미 선택지:", ", ".join(hobby_options))
    print()
    
    for i in range(num_students):
        print(f"\n👤 {i+1}번째 학생 정보:")
        
        # 이름 입력
        name = input("  이름: ").strip()
        
        # 나이 입력
        while True:
            try:
                age = int(input("  나이: "))
                if 10 <= age <= 30:
                    break
                else:
                    print("     10-30세 사이로 입력해주세요.")
            except ValueError:
                print("     숫자로 입력해주세요.")
        
        # 취미 입력
        while True:
            hobby = input("  주요 취미: ").strip()
            if hobby in hobby_options:
                break
            else:
                print(f"     위 선택지에서 정확히 입력해주세요: {', '.join(hobby_options)}")
        
        # 주간 활동시간 입력
        while True:
            try:
                hours_per_week = float(input("  주간 활동시간 (시간): "))
                if 0 <= hours_per_week <= 50:
                    break
                else:
                    print("     0-50시간 사이로 입력해주세요.")
            except ValueError:
                print("     숫자로 입력해주세요.")
        
        # 데이터 저장
        students_data.append({
            '이름': name,
            '나이': age,
            '취미': hobby,
            '주간_활동시간': hours_per_week
        })
    
    # DataFrame 생성
    df = pd.DataFrame(students_data)
    
    return df

def analyze_hobby_data(df):
    """
    취미 데이터를 분석하고 시각화하는 함수
    
    알고리즘:
    1. 기본 통계 정보 출력
    2. 취미별 인기도 분석
    3. 나이대별 취미 분포 분석
    4. 활동시간별 분석
    5. 종합 시각화
    """
    
    print("\n📊 취미 데이터 분석 결과")
    print("=" * 50)
    
    # 1. 기본 정보
    print(f"📋 전체 학생 수: {len(df)}명")
    print(f"📋 평균 나이: {df['나이'].mean():.1f}세")
    print(f"📋 평균 활동시간: {df['주간_활동시간'].mean():.1f}시간/주")
    
    # 2. 취미별 인기도
    hobby_counts = df['취미'].value_counts()
    print(f"\n🏆 인기 취미 TOP 3:")
    for i, (hobby, count) in enumerate(hobby_counts.head(3).items(), 1):
        print(f"  {i}위: {hobby} ({count}명)")
    
    # 3. 시각화
    fig, ((ax1, ax2), (ax3, ax4)) = plt.subplots(2, 2, figsize=(16, 12))
    fig.suptitle('🎭 우리 반 취미 분석 대시보드', fontsize=20, fontweight='bold')
    
    # 그래프 1: 취미별 인기도
    colors = plt.cm.Set3(range(len(hobby_counts)))
    bars1 = ax1.bar(hobby_counts.index, hobby_counts.values, color=colors)
    ax1.set_title('📊 취미별 인기도', fontsize=14, fontweight='bold')
    ax1.set_xlabel('취미', fontsize=12)
    ax1.set_ylabel('학생 수 (명)', fontsize=12)
    ax1.tick_params(axis='x', rotation=45)
    
    # 막대 위에 숫자 표시
    for bar, count in zip(bars1, hobby_counts.values):
        ax1.text(bar.get_x() + bar.get_width()/2, bar.get_height() + 0.05,
                str(count), ha='center', va='bottom', fontweight='bold')
    
    # 그래프 2: 나이별 분포
    age_bins = [10, 15, 18, 22, 30]
    age_labels = ['10-14세', '15-17세', '18-21세', '22-30세']
    df['나이대'] = pd.cut(df['나이'], bins=age_bins, labels=age_labels, include_lowest=True)
    age_counts = df['나이대'].value_counts().sort_index()
    
    wedges, texts, autotexts = ax2.pie(age_counts.values, labels=age_counts.index, 
                                      autopct='%1.1f%%', startangle=90, 
                                      colors=plt.cm.Pastel1(range(len(age_counts))))
    ax2.set_title('👥 나이대별 분포', fontsize=14, fontweight='bold')
    
    # 그래프 3: 활동시간 분포
    ax3.hist(df['주간_활동시간'], bins=8, color='skyblue', alpha=0.7, edgecolor='black')
    ax3.axvline(df['주간_활동시간'].mean(), color='red', linestyle='--', 
                label=f'평균: {df["주간_활동시간"].mean():.1f}시간')
    ax3.set_title('⏰ 주간 활동시간 분포', fontsize=14, fontweight='bold')
    ax3.set_xlabel('활동시간 (시간/주)', fontsize=12)
    ax3.set_ylabel('학생 수 (명)', fontsize=12)
    ax3.legend()
    ax3.grid(True, alpha=0.3)
    
    # 그래프 4: 취미별 평균 활동시간
    hobby_time = df.groupby('취미')['주간_활동시간'].mean().sort_values(ascending=False)
    bars4 = ax4.bar(hobby_time.index, hobby_time.values, 
                    color=plt.cm.viridis(range(len(hobby_time))))
    ax4.set_title('🕒 취미별 평균 활동시간', fontsize=14, fontweight='bold')
    ax4.set_xlabel('취미', fontsize=12)
    ax4.set_ylabel('평균 활동시간 (시간/주)', fontsize=12)
    ax4.tick_params(axis='x', rotation=45)
    
    # 막대 위에 숫자 표시
    for bar, time in zip(bars4, hobby_time.values):
        ax4.text(bar.get_x() + bar.get_width()/2, bar.get_height() + 0.2,
                f'{time:.1f}h', ha='center', va='bottom', fontweight='bold')
    
    plt.tight_layout()
    plt.show()
    
    # 상세 분석 결과
    print(f"\n🔍 상세 분석 결과:")
    print(f"=" * 30)
    print(f"🎯 가장 인기있는 취미: {hobby_counts.index[0]} ({hobby_counts.iloc[0]}명)")
    print(f"⏰ 가장 많은 시간을 투자하는 취미: {hobby_time.index[0]} ({hobby_time.iloc[0]:.1f}시간/주)")
    print(f"👥 가장 많은 나이대: {age_counts.index[age_counts.argmax()]}")
    
    # DataFrame 정보 출력
    print(f"\n📋 상세 데이터:")
    print(df.to_string(index=False))

# 실행
hobby_df = create_hobby_survey()
analyze_hobby_data(hobby_df)
```

### 📌 핵심 개념 2: 실무 데이터 처리 패턴 (25분)

#### 🔄 **CSV 파일 처리와 실제 데이터 분석**

**알고리즘 말투로 실무 데이터 분석 과정 표현:**
1. "외부 데이터 파일을 안전하게 불러온다"
2. "데이터의 품질을 확인하고 결측치를 처리한다"
3. "비즈니스 목적에 맞게 데이터를 변환한다"
4. "의미 있는 인사이트를 도출한다"
5. "결과를 이해하기 쉬운 시각화로 표현한다"

#### 🎯 **실무 시뮬레이션: 온라인 쇼핑몰 매출 분석**

```python
import pandas as pd
import matplotlib.pyplot as plt
import numpy as np
from datetime import datetime, timedelta

def create_sample_sales_data():
    """
    가상의 온라인 쇼핑몰 매출 데이터 생성
    실제 업무에서는 데이터베이스나 CSV 파일에서 불러옴
    """
    
    # 알고리즘: 현실적인 샘플 데이터 생성
    np.random.seed(42)  # 재현 가능한 결과를 위해
    
    # 날짜 범위 (최근 3개월)
    end_date = datetime.now()
    start_date = end_date - timedelta(days=90)
    date_range = pd.date_range(start=start_date, end=end_date, freq='D')
    
    # 상품 카테고리
    categories = ['전자제품', '의류', '도서', '화장품', '식품', '생활용품', '스포츠용품']
    
    # 실제 비즈니스 패턴을 반영한 데이터 생성
    sales_data = []
    
    for date in date_range:
        # 요일별 패턴 (주말에 더 많은 매출)
        weekday_factor = 1.5 if date.weekday() >= 5 else 1.0
        
        # 월별 패턴 (월말에 더 많은 매출)
        month_factor = 1.3 if date.day >= 25 else 1.0
        
        # 각 카테고리별로 데이터 생성
        for category in categories:
            # 카테고리별 기본 매출량
            base_sales = {
                '전자제품': 50, '의류': 80, '도서': 30, '화장품': 60,
                '식품': 100, '생활용품': 70, '스포츠용품': 40
            }
            
            # 카테고리별 평균 단가
            avg_price = {
                '전자제품': 150000, '의류': 50000, '도서': 15000, '화장품': 30000,
                '식품': 10000, '생활용품': 25000, '스포츠용품': 80000
            }
            
            # 무작위 변동 추가
            daily_sales = int(base_sales[category] * weekday_factor * month_factor * 
                            np.random.uniform(0.7, 1.3))
            
            # 매출액 계산
            revenue = daily_sales * avg_price[category] * np.random.uniform(0.8, 1.2)
            
            sales_data.append({
                '날짜': date,
                '카테고리': category,
                '판매량': daily_sales,
                '매출액': int(revenue),
                '요일': date.strftime('%A'),
                '월': date.month,
                '주차': date.isocalendar()[1]
            })
    
    return pd.DataFrame(sales_data)

def analyze_sales_performance(df):
    """
    매출 데이터를 다각도로 분석하는 함수
    
    알고리즘:
    1. 전체 매출 현황 파악
    2. 카테고리별 성과 분석
    3. 시간대별 트렌드 분석
    4. 실무진에게 유용한 인사이트 도출
    """
    
    print("💼 온라인 쇼핑몰 매출 분석 리포트")
    print("=" * 60)
    
    # 1. 전체 현황
    total_revenue = df['매출액'].sum()
    total_sales = df['판매량'].sum()
    avg_daily_revenue = df.groupby('날짜')['매출액'].sum().mean()
    
    print(f"📈 전체 매출액: {total_revenue:,}원")
    print(f"📦 총 판매량: {total_sales:,}개")
    print(f"💰 일평균 매출: {avg_daily_revenue:,.0f}원")
    
    # 2. 카테고리별 분석
    category_analysis = df.groupby('카테고리').agg({
        '매출액': ['sum', 'mean'],
        '판매량': ['sum', 'mean']
    }).round(0)
    
    print(f"\n🏆 카테고리별 성과:")
    category_revenue = df.groupby('카테고리')['매출액'].sum().sort_values(ascending=False)
    for i, (category, revenue) in enumerate(category_revenue.items(), 1):
        percentage = revenue / total_revenue * 100
        print(f"  {i}위: {category} - {revenue:,}원 ({percentage:.1f}%)")
    
    # 3. 시각화
    fig = plt.figure(figsize=(20, 15))
    
    # 그래프 1: 일별 매출 트렌드 (2x3 레이아웃)
    ax1 = plt.subplot(2, 3, 1)
    daily_revenue = df.groupby('날짜')['매출액'].sum()
    ax1.plot(daily_revenue.index, daily_revenue.values, linewidth=2, color='#2E86AB')
    ax1.fill_between(daily_revenue.index, daily_revenue.values, alpha=0.3, color='#2E86AB')
    ax1.set_title('📈 일별 매출 트렌드', fontsize=14, fontweight='bold')
    ax1.set_ylabel('매출액 (원)', fontsize=12)
    ax1.tick_params(axis='x', rotation=45)
    ax1.grid(True, alpha=0.3)
    
    # 이동평균선 추가
    rolling_mean = daily_revenue.rolling(window=7).mean()
    ax1.plot(rolling_mean.index, rolling_mean.values, '--', color='red', 
             label='7일 이동평균', linewidth=2)
    ax1.legend()
    
    # 그래프 2: 카테고리별 매출 파이차트
    ax2 = plt.subplot(2, 3, 2)
    colors = plt.cm.Set3(range(len(category_revenue)))
    wedges, texts, autotexts = ax2.pie(category_revenue.values, labels=category_revenue.index,
                                      autopct='%1.1f%%', colors=colors, startangle=90)
    ax2.set_title('🥧 카테고리별 매출 비중', fontsize=14, fontweight='bold')
    
    # 그래프 3: 요일별 매출 패턴
    ax3 = plt.subplot(2, 3, 3)
    weekday_order = ['Monday', 'Tuesday', 'Wednesday', 'Thursday', 'Friday', 'Saturday', 'Sunday']
    weekday_korean = ['월', '화', '수', '목', '금', '토', '일']
    weekday_revenue = df.groupby('요일')['매출액'].mean().reindex(weekday_order)
    
    bars3 = ax3.bar(weekday_korean, weekday_revenue.values, 
                    color=['#FF6B6B', '#4ECDC4', '#45B7D1', '#96CEB4', '#FECA57', '#FF9F43', '#A55EEA'])
    ax3.set_title('📅 요일별 평균 매출', fontsize=14, fontweight='bold')
    ax3.set_ylabel('평균 매출액 (원)', fontsize=12)
    
    # 막대 위에 수치 표시
    for bar, revenue in zip(bars3, weekday_revenue.values):
        ax3.text(bar.get_x() + bar.get_width()/2, bar.get_height() + 100000,
                f'{revenue/1000000:.1f}M', ha='center', va='bottom', fontweight='bold')
    
    # 그래프 4: 카테고리별 상세 분석 (판매량 vs 매출액)
    ax4 = plt.subplot(2, 3, 4)
    category_summary = df.groupby('카테고리').agg({
        '판매량': 'sum',
        '매출액': 'sum'
    })
    
    # 버블 차트 (크기 = 매출액, 위치 = 판매량)
    scatter = ax4.scatter(category_summary['판매량'], 
                         category_summary.index,
                         s=category_summary['매출액']/1000000,  # 크기를 백만원 단위로
                         alpha=0.6, c=range(len(category_summary)), cmap='viridis')
    
    ax4.set_title('🎯 카테고리별 판매량 vs 매출액', fontsize=14, fontweight='bold')
    ax4.set_xlabel('총 판매량 (개)', fontsize=12)
    
    # 각 점에 라벨 추가
    for i, (category, row) in enumerate(category_summary.iterrows()):
        ax4.annotate(f'{row["매출액"]/100000000:.1f}억', 
                    (row['판매량'], i), xytext=(10, 0), 
                    textcoords='offset points', va='center')
    
    # 그래프 5: 월별 성장률
    ax5 = plt.subplot(2, 3, 5)
    monthly_revenue = df.groupby('월')['매출액'].sum()
    monthly_growth = monthly_revenue.pct_change() * 100
    
    colors = ['red' if x < 0 else 'green' for x in monthly_growth.values[1:]]
    bars5 = ax5.bar(monthly_growth.index[1:], monthly_growth.values[1:], color=colors, alpha=0.7)
    ax5.set_title('📊 월별 매출 성장률', fontsize=14, fontweight='bold')
    ax5.set_ylabel('성장률 (%)', fontsize=12)
    ax5.axhline(y=0, color='black', linestyle='-', alpha=0.3)
    ax5.set_xlabel('월', fontsize=12)
    
    # 그래프 6: TOP 5 매출일
    ax6 = plt.subplot(2, 3, 6)
    top_days = daily_revenue.nlargest(5)
    bars6 = ax6.bar(range(len(top_days)), top_days.values, 
                    color=plt.cm.Reds(np.linspace(0.4, 0.8, len(top_days))))
    ax6.set_title('🏆 TOP 5 매출 기록일', fontsize=14, fontweight='bold')
    ax6.set_ylabel('매출액 (원)', fontsize=12)
    ax6.set_xticks(range(len(top_days)))
    ax6.set_xticklabels([date.strftime('%m/%d') for date in top_days.index], rotation=45)
    
    # 막대 위에 수치 표시
    for bar, revenue in zip(bars6, top_days.values):
        ax6.text(bar.get_x() + bar.get_width()/2, bar.get_height() + 1000000,
                f'{revenue/1000000:.1f}M', ha='center', va='bottom', fontweight='bold')
    
    plt.tight_layout()
    plt.show()
    
    # 4. 비즈니스 인사이트
    print(f"\n💡 핵심 인사이트:")
    print(f"=" * 30)
    
    # 최고 매출 요일
    best_weekday = weekday_revenue.idxmax()
    best_weekday_kr = weekday_korean[weekday_order.index(best_weekday)]
    print(f"🎯 매출이 가장 좋은 요일: {best_weekday_kr}요일")
    
    # 성장률 분석
    if len(monthly_growth) > 1:
        latest_growth = monthly_growth.iloc[-1]
        if latest_growth > 0:
            print(f"📈 최근 매출 트렌드: 전월 대비 {latest_growth:.1f}% 성장")
        else:
            print(f"📉 최근 매출 트렌드: 전월 대비 {abs(latest_growth):.1f}% 감소")
    
    # 카테고리 추천
    top_category = category_revenue.index[0]
    print(f"🏆 핵심 카테고리: {top_category} (전체 매출의 {category_revenue.iloc[0]/total_revenue*100:.1f}%)")
    
    return df

# 실행
print("🏪 온라인 쇼핑몰 매출 데이터 분석을 시작합니다...")
sales_df = create_sample_sales_data()
analyzed_df = analyze_sales_performance(sales_df)
```

---

## ☕ 휴식 시간 (10분)

---

## 🎯 3부: 코드 문서화와 프로젝트 관리 (40분)

### 📌 핵심 개념 1: 코드 문서화의 중요성 (15분)

#### 📝 **왜 문서화가 필요한가?**

**문서화 = 미래의 나와 다른 개발자들을 위한 배려**

**실제 개발 현장에서의 문제:**
```python
# 😰 문서화가 안 된 코드 (6개월 후 내가 봐도 모르겠다!)
def calc(a, b, c):
    if a > 18:
        x = b * 0.15 + c * 0.05
        if b > 100000:
            x *= 1.2
        return x
    else:
        return 0

# 🤔 이 함수가 뭘 하는 거지? a, b, c는 뭘 의미하지?
result = calc(25, 120000, 50000)  # 뭔지 모르겠다...
```

**문서화가 잘 된 코드:**
```python
# ✅ 문서화가 잘 된 코드 (1년 후에도 바로 이해!)
def calculate_tax_amount(age: int, income: int, deduction: int) -> float:
    """
    나이와 소득에 따른 세금을 계산하는 함수
    
    Args:
        age (int): 납세자의 나이
        income (int): 연간 소득 (원)
        deduction (int): 공제 금액 (원)
    
    Returns:
        float: 계산된 세금 (원)
        
    Examples:
        >>> calculate_tax_amount(25, 120000, 50000)
        19500.0
        
        >>> calculate_tax_amount(17, 50000, 10000)
        0
    
    Note:
        - 18세 미만은 세금 면제
        - 기본 세율: 소득 15%, 공제 5%
        - 고소득자(10만원 초과) 추가 20% 할증
    """
    # 미성년자는 세금 면제
    if age < 18:
        return 0
    
    # 기본 세율 적용
    basic_tax = income * 0.15 + deduction * 0.05
    
    # 고소득자 할증 적용
    if income > 100000:
        basic_tax *= 1.2  # 20% 할증
    
    return basic_tax

# 이제 함수의 용도가 명확하다!
my_tax = calculate_tax_amount(age=25, income=120000, deduction=50000)
print(f"내 세금: {my_tax:,}원")
```

#### 📚 **Python Docstring 작성 규칙**

**Google Style Docstring (가장 널리 사용됨):**

```python
def process_student_grades(grades_dict, passing_score=60):
    """
    학생들의 성적을 처리하고 통계를 계산하는 함수
    
    이 함수는 학생별 성적 딕셔너리를 받아서 합격/불합격을 판정하고,
    전체 통계 정보를 계산하여 반환합니다.
    
    Args:
        grades_dict (dict): 학생 이름을 키로, 점수 리스트를 값으로 하는 딕셔너리
            예: {"김철수": [85, 90, 78], "이영희": [92, 88, 95]}
        passing_score (int, optional): 합격 기준 점수. 기본값은 60점.
    
    Returns:
        dict: 처리 결과를 담은 딕셔너리
            - 'summary': 전체 통계 정보 (dict)
                - 'total_students': 전체 학생 수 (int)
                - 'passed_students': 합격 학생 수 (int)
                - 'average_score': 전체 평균 점수 (float)
            - 'individual_results': 개별 학생 결과 (dict)
                - 학생 이름: {'average': 평균점수, 'status': '합격'/'불합격'}
    
    Raises:
        ValueError: grades_dict가 비어있거나 잘못된 형식일 때
        TypeError: 점수가 숫자가 아닐 때
    
    Examples:
        >>> grades = {"김철수": [85, 90, 78], "이영희": [45, 50, 48]}
        >>> result = process_student_grades(grades, passing_score=70)
        >>> print(result['summary']['passed_students'])
        1
        
        >>> result['individual_results']['김철수']['status']
        '합격'
    
    Note:
        - 각 학생의 평균이 passing_score 이상이면 합격
        - 빈 점수 리스트가 있으면 해당 학생은 불합격 처리
        - 소수점 둘째 자리까지 반올림하여 계산
    
    Version:
        1.2.0 (2024-10-15): 통계 계산 로직 개선
    
    Author:
        개발팀 교육파트 (education@company.com)
    """
    
    # 입력 검증
    if not grades_dict:
        raise ValueError("성적 데이터가 비어있습니다.")
    
    summary = {
        'total_students': len(grades_dict),
        'passed_students': 0,
        'average_score': 0.0
    }
    
    individual_results = {}
    all_scores = []
    
    # 각 학생별 처리
    for student_name, scores in grades_dict.items():
        if not scores:  # 빈 리스트 처리
            individual_results[student_name] = {
                'average': 0.0,
                'status': '불합격'
            }
            continue
        
        # 점수 유효성 검사
        try:
            numeric_scores = [float(score) for score in scores]
        except (ValueError, TypeError):
            raise TypeError(f"{student_name}의 점수에 숫자가 아닌 값이 포함되어 있습니다.")
        
        # 평균 계산
        student_average = round(sum(numeric_scores) / len(numeric_scores), 2)
        all_scores.extend(numeric_scores)
        
        # 합격/불합격 판정
        status = '합격' if student_average >= passing_score else '불합격'
        if status == '합격':
            summary['passed_students'] += 1
        
        individual_results[student_name] = {
            'average': student_average,
            'status': status
        }
    
    # 전체 평균 계산
    if all_scores:
        summary['average_score'] = round(sum(all_scores) / len(all_scores), 2)
    
    return {
        'summary': summary,
        'individual_results': individual_results
    }


# 사용 예시
if __name__ == "__main__":
    # 테스트 데이터
    test_grades = {
        "김철수": [85, 90, 78],
        "이영희": [92, 88, 95],
        "박민수": [45, 50, 48],
        "최지원": [70, 75, 65]
    }
    
    # 함수 실행
    result = process_student_grades(test_grades, passing_score=70)
    
    # 결과 출력
    print("📊 성적 처리 결과")
    print(f"전체 학생: {result['summary']['total_students']}명")
    print(f"합격 학생: {result['summary']['passed_students']}명")
    print(f"전체 평균: {result['summary']['average_score']}점")
    
    print("\n📋 개별 결과:")
    for name, info in result['individual_results'].items():
        print(f"  {name}: {info['average']}점 ({info['status']})")
```

### 📌 핵심 개념 2: 프로젝트 문서화 패턴 (25분)

#### 📁 **실제 프로젝트 구조와 문서화**

**알고리즘 말투로 프로젝트 문서화 과정 표현:**
1. "프로젝트의 목적과 기능을 명확히 정의한다"
2. "설치 및 실행 방법을 단계별로 설명한다"
3. "코드의 구조와 주요 모듈을 설명한다"
4. "사용 예시와 API 문서를 제공한다"
5. "개발자를 위한 가이드라인을 작성한다"

#### 🎯 **종합 실습: 개인 가계부 관리 시스템**

```python
# personal_finance_manager/
# ├── README.md
# ├── main.py
# ├── modules/
# │   ├── __init__.py
# │   ├── expense_tracker.py
# │   ├── data_processor.py
# │   └── visualizer.py
# ├── data/
# │   └── sample_data.csv
# ├── docs/
# │   ├── user_guide.md
# │   └── developer_guide.md
# └── requirements.txt

"""
personal_finance_manager/main.py

개인 가계부 관리 시스템 메인 실행 파일

이 프로그램은 개인의 수입과 지출을 관리하고 분석할 수 있는 
완전한 가계부 시스템입니다.

Author: 교육팀
Version: 1.0.0
Created: 2024-10-15
Last Modified: 2024-10-15

Dependencies:
    - pandas >= 1.3.0
    - matplotlib >= 3.4.0
    - numpy >= 1.21.0

Usage:
    python main.py
    
Example:
    $ python main.py
    📊 개인 가계부 관리 시스템에 오신 것을 환영합니다!
    
License:
    MIT License
"""

import sys
import os
from datetime import datetime, timedelta
import pandas as pd
import matplotlib.pyplot as plt

# 로컬 모듈 import (실제로는 별도 파일에 있음)
class ExpenseTracker:
    """
    지출 내역을 관리하는 클래스
    
    이 클래스는 사용자의 수입과 지출을 기록하고 관리하는 
    핵심 기능을 제공합니다.
    
    Attributes:
        transactions (list): 거래 내역을 저장하는 리스트
        categories (set): 등록된 카테고리 집합
        
    Example:
        >>> tracker = ExpenseTracker()
        >>> tracker.add_transaction("income", 3000000, "급여", "2024-10-01")
        >>> tracker.add_transaction("expense", 500000, "식비", "2024-10-02")
        >>> print(tracker.get_balance())
        2500000
    """
    
    def __init__(self):
        """ExpenseTracker 인스턴스를 초기화합니다."""
        self.transactions = []
        self.categories = {
            # 수입 카테고리
            '급여', '용돈', '투자수익', '부업', '기타수입',
            # 지출 카테고리  
            '식비', '교통비', '쇼핑', '문화생활', '의료비', 
            '교육비', '통신비', '주거비', '기타지출'
        }
        
    def add_transaction(self, transaction_type: str, amount: int, 
                       category: str, date: str, description: str = "") -> bool:
        """
        새로운 거래 내역을 추가합니다.
        
        Args:
            transaction_type (str): 거래 유형 ('income' 또는 'expense')
            amount (int): 거래 금액 (양수)
            category (str): 거래 카테고리
            date (str): 거래 날짜 (YYYY-MM-DD 형식)
            description (str, optional): 거래 설명
            
        Returns:
            bool: 성공적으로 추가되면 True, 실패하면 False
            
        Raises:
            ValueError: 잘못된 거래 유형이나 금액일 때
            
        Example:
            >>> tracker.add_transaction("expense", 50000, "식비", "2024-10-15", "점심 식사")
            True
        """
        try:
            # 입력 검증
            if transaction_type not in ['income', 'expense']:
                raise ValueError("거래 유형은 'income' 또는 'expense'여야 합니다.")
            
            if amount <= 0:
                raise ValueError("거래 금액은 양수여야 합니다.")
            
            if category not in self.categories:
                print(f"⚠️  새로운 카테고리 '{category}'가 추가됩니다.")
                self.categories.add(category)
            
            # 날짜 형식 검증
            datetime.strptime(date, '%Y-%m-%d')
            
            # 거래 내역 추가
            transaction = {
                'type': transaction_type,
                'amount': amount,
                'category': category,
                'date': date,
                'description': description,
                'timestamp': datetime.now().isoformat()
            }
            
            self.transactions.append(transaction)
            return True
            
        except ValueError as e:
            print(f"❌ 거래 추가 실패: {e}")
            return False
    
    def get_balance(self) -> int:
        """
        현재 잔액을 계산합니다.
        
        Returns:
            int: 총 수입에서 총 지출을 뺀 잔액
            
        Example:
            >>> tracker.get_balance()
            2500000
        """
        total_income = sum(t['amount'] for t in self.transactions if t['type'] == 'income')
        total_expense = sum(t['amount'] for t in self.transactions if t['type'] == 'expense')
        return total_income - total_expense
    
    def get_monthly_summary(self, year: int, month: int) -> dict:
        """
        특정 월의 수입/지출 요약을 반환합니다.
        
        Args:
            year (int): 연도
            month (int): 월 (1-12)
            
        Returns:
            dict: 월별 요약 정보
                - 'income': 총 수입
                - 'expense': 총 지출  
                - 'balance': 잔액
                - 'categories': 카테고리별 지출
                
        Example:
            >>> summary = tracker.get_monthly_summary(2024, 10)
            >>> print(summary['income'])
            3000000
        """
        monthly_transactions = [
            t for t in self.transactions 
            if datetime.strptime(t['date'], '%Y-%m-%d').year == year
            and datetime.strptime(t['date'], '%Y-%m-%d').month == month
        ]
        
        income_total = sum(t['amount'] for t in monthly_transactions if t['type'] == 'income')
        expense_total = sum(t['amount'] for t in monthly_transactions if t['type'] == 'expense')
        
        # 카테고리별 지출 분석
        expense_by_category = {}
        for transaction in monthly_transactions:
            if transaction['type'] == 'expense':
                category = transaction['category']
                expense_by_category[category] = expense_by_category.get(category, 0) + transaction['amount']
        
        return {
            'income': income_total,
            'expense': expense_total,
            'balance': income_total - expense_total,
            'categories': expense_by_category,
            'transaction_count': len(monthly_transactions)
        }


class FinanceVisualizer:
    """
    가계부 데이터를 시각화하는 클래스
    
    ExpenseTracker의 데이터를 받아서 다양한 그래프와 
    차트로 시각화하는 기능을 제공합니다.
    
    Attributes:
        tracker (ExpenseTracker): 데이터 소스인 ExpenseTracker 인스턴스
        
    Example:
        >>> visualizer = FinanceVisualizer(tracker)
        >>> visualizer.plot_monthly_trend(2024)
    """
    
    def __init__(self, tracker: ExpenseTracker):
        """
        FinanceVisualizer를 초기화합니다.
        
        Args:
            tracker (ExpenseTracker): 데이터 소스
        """
        self.tracker = tracker
        # 한글 폰트 설정
        plt.rcParams['font.family'] = 'Malgun Gothic'
        plt.rcParams['axes.unicode_minus'] = False
    
    def plot_monthly_trend(self, year: int) -> None:
        """
        연간 월별 수입/지출 추이를 그래프로 표시합니다.
        
        Args:
            year (int): 표시할 연도
            
        Example:
            >>> visualizer.plot_monthly_trend(2024)
        """
        months = range(1, 13)
        monthly_incomes = []
        monthly_expenses = []
        
        for month in months:
            summary = self.tracker.get_monthly_summary(year, month)
            monthly_incomes.append(summary['income'])
            monthly_expenses.append(summary['expense'])
        
        fig, ax = plt.subplots(figsize=(12, 6))
        
        # 수입/지출 그래프
        ax.plot(months, monthly_incomes, marker='o', linewidth=3, 
                label='수입', color='#2E86AB', markersize=8)
        ax.plot(months, monthly_expenses, marker='s', linewidth=3, 
                label='지출', color='#F24236', markersize=8)
        
        # 그래프 꾸미기
        ax.set_title(f'{year}년 월별 수입/지출 추이', fontsize=16, fontweight='bold')
        ax.set_xlabel('월', fontsize=12)
        ax.set_ylabel('금액 (원)', fontsize=12)
        ax.legend(fontsize=12)
        ax.grid(True, alpha=0.3)
        ax.set_xticks(months)
        
        # y축 포맷팅 (백만원 단위)
        ax.yaxis.set_major_formatter(plt.FuncFormatter(lambda x, p: f'{x/1000000:.1f}M'))
        
        plt.tight_layout()
        plt.show()


def main():
    """
    메인 프로그램 실행 함수
    
    사용자 인터페이스를 제공하고 전체 프로그램 흐름을 관리합니다.
    
    이 함수는 다음과 같은 기능을 제공합니다:
    1. 거래 내역 추가
    2. 월별 요약 보기
    3. 그래프 시각화
    4. 데이터 내보내기
    
    Usage:
        이 함수는 직접 호출하지 말고 스크립트 실행으로 사용하세요.
        $ python main.py
    
    Note:
        프로그램 종료는 메뉴에서 '5'를 선택하거나 Ctrl+C를 누르세요.
    """
    
    print("=" * 60)
    print("📊 개인 가계부 관리 시스템 v1.0.0")
    print("=" * 60)
    print("이 프로그램으로 수입과 지출을 체계적으로 관리해보세요!")
    print()
    
    # ExpenseTracker 인스턴스 생성
    tracker = ExpenseTracker()
    visualizer = FinanceVisualizer(tracker)
    
    # 샘플 데이터 추가 (시연용)
    sample_data = [
        ("income", 3000000, "급여", "2024-10-01", "10월 급여"),
        ("expense", 500000, "식비", "2024-10-02", "월 식비"),
        ("expense", 800000, "주거비", "2024-10-03", "월 임대료"),
        ("expense", 200000, "교통비", "2024-10-04", "교통카드 충전"),
        ("income", 500000, "부업", "2024-10-05", "프리랜서 수입"),
        ("expense", 300000, "쇼핑", "2024-10-06", "의류 구매"),
    ]
    
    print("📝 샘플 데이터를 추가하는 중...")
    for data in sample_data:
        tracker.add_transaction(*data)
    print(f"✅ {len(sample_data)}개의 샘플 거래가 추가되었습니다.")
    print()
    
    while True:
        try:
            # 메인 메뉴
            print("🏠 메인 메뉴")
            print("-" * 30)
            print("1. 💰 거래 추가")
            print("2. 📊 월별 요약 보기")
            print("3. 📈 그래프 보기")
            print("4. 💳 현재 잔액 확인")
            print("5. 🚪 프로그램 종료")
            print()
            
            choice = input("선택하세요 (1-5): ").strip()
            
            if choice == "1":
                # 거래 추가
                print("\n💰 새 거래 추가")
                print("-" * 20)
                
                # 거래 유형 선택
                while True:
                    trans_type = input("거래 유형 (1: 수입, 2: 지출): ").strip()
                    if trans_type == "1":
                        trans_type = "income"
                        break
                    elif trans_type == "2":
                        trans_type = "expense"
                        break
                    else:
                        print("1 또는 2를 입력하세요.")
                
                # 금액 입력
                while True:
                    try:
                        amount = int(input("금액 (원): "))
                        if amount > 0:
                            break
                        else:
                            print("양수를 입력하세요.")
                    except ValueError:
                        print("숫자를 입력하세요.")
                
                # 카테고리 선택
                print(f"\n사용 가능한 카테고리: {', '.join(sorted(tracker.categories))}")
                category = input("카테고리: ").strip()
                
                # 날짜 입력
                while True:
                    date_input = input("날짜 (YYYY-MM-DD, 엔터키: 오늘): ").strip()
                    if not date_input:
                        date_input = datetime.now().strftime('%Y-%m-%d')
                    
                    try:
                        datetime.strptime(date_input, '%Y-%m-%d')
                        break
                    except ValueError:
                        print("올바른 날짜 형식을 입력하세요 (YYYY-MM-DD).")
                
                # 설명 입력
                description = input("설명 (선택사항): ").strip()
                
                # 거래 추가
                if tracker.add_transaction(trans_type, amount, category, date_input, description):
                    type_kr = "수입" if trans_type == "income" else "지출"
                    print(f"✅ {type_kr} {amount:,}원이 추가되었습니다.")
                
            elif choice == "2":
                # 월별 요약
                print("\n📊 월별 요약")
                print("-" * 20)
                
                try:
                    year = int(input("연도 (YYYY): "))
                    month = int(input("월 (1-12): "))
                    
                    if 1 <= month <= 12:
                        summary = tracker.get_monthly_summary(year, month)
                        
                        print(f"\n📅 {year}년 {month}월 요약")
                        print("=" * 30)
                        print(f"💰 총 수입: {summary['income']:,}원")
                        print(f"💸 총 지출: {summary['expense']:,}원")
                        print(f"💳 잔액: {summary['balance']:,}원")
                        print(f"📝 거래 건수: {summary['transaction_count']}건")
                        
                        if summary['categories']:
                            print(f"\n📊 카테고리별 지출:")
                            for cat, amount in sorted(summary['categories'].items(), 
                                                    key=lambda x: x[1], reverse=True):
                                percentage = amount / summary['expense'] * 100 if summary['expense'] > 0 else 0
                                print(f"  • {cat}: {amount:,}원 ({percentage:.1f}%)")
                    else:
                        print("올바른 월을 입력하세요 (1-12).")
                        
                except ValueError:
                    print("숫자를 입력하세요.")
            
            elif choice == "3":
                # 그래프 보기
                print("\n📈 그래프 시각화")
                print("-" * 20)
                
                try:
                    year = int(input("연도 (YYYY): "))
                    print("그래프를 생성하는 중...")
                    visualizer.plot_monthly_trend(year)
                except ValueError:
                    print("올바른 연도를 입력하세요.")
            
            elif choice == "4":
                # 잔액 확인
                balance = tracker.get_balance()
                print(f"\n💳 현재 잔액: {balance:,}원")
                
                if balance > 0:
                    print("💰 수입이 지출보다 많습니다!")
                elif balance < 0:
                    print("⚠️  지출이 수입을 초과했습니다.")
                else:
                    print("⚖️  수입과 지출이 동일합니다.")
            
            elif choice == "5":
                print("\n👋 프로그램을 종료합니다.")
                print("가계부 관리를 통해 건전한 소비습관을 만들어보세요!")
                break
            
            else:
                print("❌ 올바른 번호를 선택하세요 (1-5).")
            
            print()  # 빈 줄 추가
            
        except KeyboardInterrupt:
            print("\n\n👋 프로그램이 중단되었습니다.")
            break
        except Exception as e:
            print(f"\n❌ 오류가 발생했습니다: {e}")
            print("다시 시도해주세요.")


if __name__ == "__main__":
    """
    스크립트가 직접 실행될 때만 main() 함수를 호출합니다.
    
    이 방식은 Python 모듈의 표준 패턴으로, 다른 파일에서 
    이 모듈을 import할 때 main() 함수가 자동으로 실행되지 
    않도록 방지합니다.
    
    Usage:
        $ python main.py
    """
    main()
```

---

## 🎯 실습과제 (60분)

### 📝 **과제 1: 개인 운동 기록 관리 시스템 (30분)**

**알고리즘 말투로 요구사항 표현:**

1. **데이터 수집**: "사용자로부터 운동 기록 데이터를 입력받는다"
2. **데이터 저장**: "입력받은 데이터를 체계적으로 저장하고 관리한다"
3. **분석 처리**: "운동 패턴과 성과를 분석한다"
4. **시각화**: "분석 결과를 다양한 그래프로 표현한다"
5. **문서화**: "모든 함수와 클래스에 완전한 docstring을 작성한다"

**구현해야 할 기능:**
- 운동 기록 추가 (날짜, 운동종류, 시간, 칼로리, 강도)
- 주별/월별 운동 통계 분석
- 운동 종류별 성과 비교
- 목표 설정 및 달성률 계산
- 종합 대시보드 시각화

**필수 구현 사항:**
- 사용자 입력 검증 및 예외 처리
- Google Style Docstring 적용
- matplotlib를 활용한 최소 4가지 그래프
- 데이터 저장/불러오기 기능

### 📝 **과제 2: 독서 기록 및 리뷰 시스템 (30분)**

**알고리즘 말투로 요구사항 표현:**

1. **도서 관리**: "읽은 책들의 정보를 체계적으로 관리한다"
2. **독서 패턴 분석**: "독서 습관과 선호도를 분석한다"
3. **통계 생성**: "월별, 장르별, 평점별 통계를 생성한다"
4. **추천 시스템**: "읽은 책 패턴을 바탕으로 추천을 제공한다"
5. **리포트 생성**: "연간 독서 리포트를 자동 생성한다"

**구현해야 할 기능:**
- 도서 정보 등록 (제목, 저자, 장르, 페이지수, 읽은날짜, 평점, 한줄평)
- 독서 목표 설정 및 진행률 추적
- 장르별/저자별 선호도 분석
- 월별 독서량 추이 그래프
- 평점 분포 및 추천 도서 시스템

**필수 구현 사항:**
- pandas를 활용한 데이터 분석
- 상세한 함수 문서화 (Args, Returns, Examples 포함)
- 사용자 친화적인 메뉴 시스템
- 에러 처리 및 입력 검증

---

## 📚 모범답안

### 💡 **과제 1 모범답안: 개인 운동 기록 관리 시스템**

```python
"""
운동 기록 관리 시스템 - 모범답안

이 시스템은 개인의 운동 기록을 체계적으로 관리하고 
분석할 수 있는 완전한 솔루션을 제공합니다.

Author: 교육팀
Version: 1.0.0
"""

import pandas as pd
import matplotlib.pyplot as plt
import numpy as np
from datetime import datetime, timedelta
from typing import Dict, List, Optional, Tuple

class WorkoutTracker:
    """
    개인 운동 기록을 관리하는 클래스
    
    이 클래스는 운동 기록 추가, 분석, 목표 관리 등의 
    핵심 기능을 제공합니다.
    
    Attributes:
        workouts (List[Dict]): 운동 기록 리스트
        goals (Dict): 사용자 목표 설정
        workout_types (set): 등록된 운동 종류들
        
    Examples:
        >>> tracker = WorkoutTracker()
        >>> tracker.add_workout("러닝", 30, 300, "중강도", "2024-10-15")
        True
        >>> tracker.get_weekly_stats("2024-10-15")
        {'total_time': 30, 'total_calories': 300, 'workout_count': 1}
    """
    
    def __init__(self):
        """WorkoutTracker 인스턴스를 초기화합니다."""
        self.workouts = []
        self.goals = {
            'weekly_time': 300,  # 주간 목표 시간 (분)
            'weekly_calories': 2000,  # 주간 목표 칼로리
            'weekly_count': 5  # 주간 목표 운동 횟수
        }
        self.workout_types = {
            '러닝', '걷기', '수영', '자전거', '웨이트 트레이닝', 
            '요가', '필라테스', '등산', '농구', '축구', '테니스'
        }
    
    def add_workout(self, workout_type: str, duration: int, calories: int, 
                   intensity: str, date: str, notes: str = "") -> bool:
        """
        새로운 운동 기록을 추가합니다.
        
        Args:
            workout_type (str): 운동 종류
            duration (int): 운동 시간 (분)
            calories (int): 소모 칼로리
            intensity (str): 운동 강도 ('저강도', '중강도', '고강도')
            date (str): 운동 날짜 (YYYY-MM-DD)
            notes (str, optional): 운동 메모
            
        Returns:
            bool: 성공시 True, 실패시 False
            
        Raises:
            ValueError: 잘못된 입력값일 때
            
        Examples:
            >>> tracker.add_workout("러닝", 30, 300, "중강도", "2024-10-15")
            True
            >>> tracker.add_workout("수영", -10, 200, "중강도", "2024-10-15")
            False
        """
        try:
            # 입력 검증
            if duration <= 0:
                raise ValueError("운동 시간은 양수여야 합니다.")
            
            if calories < 0:
                raise ValueError("칼로리는 0 이상이어야 합니다.")
            
            if intensity not in ['저강도', '중강도', '고강도']:
                raise ValueError("강도는 '저강도', '중강도', '고강도' 중 하나여야 합니다.")
            
            # 날짜 형식 검증
            datetime.strptime(date, '%Y-%m-%d')
            
            # 새로운 운동 종류 추가
            if workout_type not in self.workout_types:
                self.workout_types.add(workout_type)
            
            # 운동 기록 추가
            workout = {
                'type': workout_type,
                'duration': duration,
                'calories': calories,
                'intensity': intensity,
                'date': date,
                'notes': notes,
                'timestamp': datetime.now().isoformat()
            }
            
            self.workouts.append(workout)
            return True
            
        except ValueError as e:
            print(f"❌ 운동 기록 추가 실패: {e}")
            return False
    
    def get_weekly_stats(self, date: str) -> Dict:
        """
        특정 날짜가 포함된 주의 운동 통계를 반환합니다.
        
        Args:
            date (str): 기준 날짜 (YYYY-MM-DD)
            
        Returns:
            Dict: 주간 운동 통계
                - 'total_time': 총 운동 시간 (분)
                - 'total_calories': 총 소모 칼로리
                - 'workout_count': 운동 횟수
                - 'goal_achievement': 목표 달성률 (%)
                
        Examples:
            >>> stats = tracker.get_weekly_stats("2024-10-15")
            >>> print(stats['total_time'])
            150
        """
        target_date = datetime.strptime(date, '%Y-%m-%d')
        week_start = target_date - timedelta(days=target_date.weekday())
        week_end = week_start + timedelta(days=6)
        
        # 해당 주의 운동 기록 필터링
        weekly_workouts = [
            w for w in self.workouts
            if week_start <= datetime.strptime(w['date'], '%Y-%m-%d') <= week_end
        ]
        
        total_time = sum(w['duration'] for w in weekly_workouts)
        total_calories = sum(w['calories'] for w in weekly_workouts)
        workout_count = len(weekly_workouts)
        
        # 목표 달성률 계산
        time_achievement = (total_time / self.goals['weekly_time']) * 100
        calorie_achievement = (total_calories / self.goals['weekly_calories']) * 100
        count_achievement = (workout_count / self.goals['weekly_count']) * 100
        
        return {
            'total_time': total_time,
            'total_calories': total_calories,
            'workout_count': workout_count,
            'goal_achievement': {
                'time': min(100, time_achievement),
                'calories': min(100, calorie_achievement),
                'count': min(100, count_achievement)
            }
        }


class WorkoutVisualizer:
    """
    운동 데이터 시각화 클래스
    
    WorkoutTracker의 데이터를 다양한 그래프와 차트로 
    시각화하는 기능을 제공합니다.
    """
    
    def __init__(self, tracker: WorkoutTracker):
        """
        WorkoutVisualizer를 초기화합니다.
        
        Args:
            tracker (WorkoutTracker): 데이터 소스
        """
        self.tracker = tracker
        plt.rcParams['font.family'] = 'Malgun Gothic'
        plt.rcParams['axes.unicode_minus'] = False
    
    def create_dashboard(self, weeks: int = 4) -> None:
        """
        운동 대시보드를 생성합니다.
        
        Args:
            weeks (int): 표시할 주간 수 (기본 4주)
            
        Examples:
            >>> visualizer.create_dashboard(4)
        """
        if not self.tracker.workouts:
            print("📊 표시할 운동 데이터가 없습니다.")
            return
        
        fig, ((ax1, ax2), (ax3, ax4)) = plt.subplots(2, 2, figsize=(16, 12))
        fig.suptitle('🏃‍♂️ 개인 운동 기록 대시보드', fontsize=20, fontweight='bold')
        
        # 데이터 준비
        df = pd.DataFrame(self.tracker.workouts)
        df['date'] = pd.to_datetime(df['date'])
        df = df.sort_values('date')
        
        # 그래프 1: 주간 운동 시간 추이
        df['week'] = df['date'].dt.isocalendar().week
        weekly_time = df.groupby('week')['duration'].sum().tail(weeks)
        
        ax1.plot(range(len(weekly_time)), weekly_time.values, 
                marker='o', linewidth=3, markersize=8, color='#2E86AB')
        ax1.axhline(y=self.tracker.goals['weekly_time'], color='red', 
                   linestyle='--', label=f"목표: {self.tracker.goals['weekly_time']}분")
        ax1.set_title('📈 주간 운동 시간 추이', fontsize=14, fontweight='bold')
        ax1.set_ylabel('시간 (분)', fontsize=12)
        ax1.set_xlabel('주차', fontsize=12)
        ax1.legend()
        ax1.grid(True, alpha=0.3)
        
        # 그래프 2: 운동 종류별 분포
        type_counts = df['type'].value_counts()
        colors = plt.cm.Set3(range(len(type_counts)))
        ax2.pie(type_counts.values, labels=type_counts.index, autopct='%1.1f%%',
               colors=colors, startangle=90)
        ax2.set_title('🥧 운동 종류별 분포', fontsize=14, fontweight='bold')
        
        # 그래프 3: 강도별 칼로리 소모
        intensity_calories = df.groupby('intensity')['calories'].sum()
        bars3 = ax3.bar(intensity_calories.index, intensity_calories.values,
                       color=['#96CEB4', '#FECA57', '#FF6B6B'])
        ax3.set_title('🔥 강도별 총 칼로리 소모', fontsize=14, fontweight='bold')
        ax3.set_ylabel('칼로리', fontsize=12)
        
        # 막대 위에 수치 표시
        for bar, calories in zip(bars3, intensity_calories.values):
            ax3.text(bar.get_x() + bar.get_width()/2, bar.get_height() + 50,
                    f'{calories:,}', ha='center', va='bottom', fontweight='bold')
        
        # 그래프 4: 월별 성과 비교
        df['month'] = df['date'].dt.month
        monthly_stats = df.groupby('month').agg({
            'duration': 'sum',
            'calories': 'sum',
            'type': 'count'
        }).rename(columns={'type': 'count'})
        
        if len(monthly_stats) > 0:
            x = range(len(monthly_stats))
            width = 0.25
            
            ax4.bar([i - width for i in x], monthly_stats['duration'], 
                   width, label='운동시간(분)', color='#45B7D1', alpha=0.8)
            ax4.bar(x, monthly_stats['calories']/10, width, 
                   label='칼로리(/10)', color='#FF9F43', alpha=0.8)
            ax4.bar([i + width for i in x], monthly_stats['count']*50, 
                   width, label='횟수(×50)', color='#A55EEA', alpha=0.8)
            
            ax4.set_title('📊 월별 운동 성과', fontsize=14, fontweight='bold')
            ax4.set_xlabel('월', fontsize=12)
            ax4.set_xticks(x)
            ax4.set_xticklabels([f'{int(m)}월' for m in monthly_stats.index])
            ax4.legend()
        
        plt.tight_layout()
        plt.show()


def main_workout_system():
    """운동 관리 시스템 메인 함수"""
    print("🏃‍♂️ 개인 운동 기록 관리 시스템")
    print("=" * 50)
    
    tracker = WorkoutTracker()
    visualizer = WorkoutVisualizer(tracker)
    
    # 샘플 데이터 추가
    sample_workouts = [
        ("러닝", 30, 300, "중강도", "2024-10-01"),
        ("웨이트 트레이닝", 45, 400, "고강도", "2024-10-02"),
        ("요가", 60, 200, "저강도", "2024-10-03"),
        ("수영", 40, 450, "고강도", "2024-10-05"),
        ("걷기", 25, 150, "저강도", "2024-10-07"),
    ]
    
    for workout in sample_workouts:
        tracker.add_workout(*workout)
    
    while True:
        print("\n🏠 메인 메뉴")
        print("1. 운동 기록 추가")
        print("2. 주간 통계 보기")
        print("3. 대시보드 보기")
        print("4. 목표 설정")
        print("5. 종료")
        
        choice = input("\n선택하세요: ").strip()
        
        if choice == "1":
            # 운동 기록 추가 로직
            print("운동 기록을 추가하겠습니다...")
            
        elif choice == "2":
            # 주간 통계 보기
            date = input("날짜 입력 (YYYY-MM-DD): ").strip()
            try:
                stats = tracker.get_weekly_stats(date)
                print(f"\n📊 주간 운동 통계:")
                print(f"총 운동시간: {stats['total_time']}분")
                print(f"총 칼로리: {stats['total_calories']}kcal")
                print(f"운동 횟수: {stats['workout_count']}회")
            except ValueError:
                print("올바른 날짜 형식을 입력하세요.")
                
        elif choice == "3":
            visualizer.create_dashboard()
            
        elif choice == "4":
            print("목표 설정 기능...")
            
        elif choice == "5":
            print("👋 프로그램을 종료합니다.")
            break


if __name__ == "__main__":
    main_workout_system()
```

### 💡 **과제 2 모범답안: 독서 기록 및 리뷰 시스템**

```python
"""
독서 기록 및 리뷰 시스템 - 모범답안

개인의 독서 기록을 체계적으로 관리하고 분석하는 시스템입니다.

Author: 교육팀  
Version: 1.0.0
"""

import pandas as pd
import matplotlib.pyplot as plt
import numpy as np
from datetime import datetime, timedelta
from typing import Dict, List, Optional, Tuple
import random

class BookTracker:
    """
    독서 기록을 관리하는 클래스
    
    도서 정보 등록, 독서 통계 분석, 추천 시스템 등의
    핵심 기능을 제공합니다.
    
    Attributes:
        books (List[Dict]): 독서 기록 리스트
        goals (Dict): 독서 목표 설정
        genres (set): 등록된 장르들
        
    Examples:
        >>> tracker = BookTracker()
        >>> tracker.add_book("파이썬 입문", "김개발", "IT", 300, "2024-10-15", 5)
        True
        >>> tracker.get_monthly_stats(2024, 10)
        {'books_read': 1, 'total_pages': 300, 'avg_rating': 5.0}
    """
    
    def __init__(self):
        """BookTracker 인스턴스를 초기화합니다."""
        self.books = []
        self.goals = {
            'yearly_books': 24,  # 연간 목표 도서 수
            'yearly_pages': 7200,  # 연간 목표 페이지 수
            'monthly_books': 2  # 월간 목표 도서 수
        }
        self.genres = {
            '소설', '에세이', '시', '자기계발', 'IT', '경제경영', 
            '역사', '과학', '철학', '종교', '예술', '여행', '요리', '건강'
        }
    
    def add_book(self, title: str, author: str, genre: str, pages: int,
                finish_date: str, rating: int, review: str = "") -> bool:
        """
        새로운 독서 기록을 추가합니다.
        
        Args:
            title (str): 도서 제목
            author (str): 저자명
            genre (str): 장르
            pages (int): 페이지 수
            finish_date (str): 완독 날짜 (YYYY-MM-DD)
            rating (int): 평점 (1-5)
            review (str, optional): 한줄평
            
        Returns:
            bool: 성공시 True, 실패시 False
            
        Raises:
            ValueError: 잘못된 입력값일 때
            
        Examples:
            >>> tracker.add_book("파이썬 입문", "김개발", "IT", 300, "2024-10-15", 5)
            True
        """
        try:
            # 입력 검증
            if not title.strip() or not author.strip():
                raise ValueError("제목과 저자명은 필수입니다.")
            
            if pages <= 0:
                raise ValueError("페이지 수는 양수여야 합니다.")
            
            if not (1 <= rating <= 5):
                raise ValueError("평점은 1-5 사이여야 합니다.")
            
            # 날짜 형식 검증
            datetime.strptime(finish_date, '%Y-%m-%d')
            
            # 새로운 장르 추가
            if genre not in self.genres:
                self.genres.add(genre)
            
            # 도서 기록 추가
            book = {
                'title': title.strip(),
                'author': author.strip(),
                'genre': genre,
                'pages': pages,
                'finish_date': finish_date,
                'rating': rating,
                'review': review.strip(),
                'added_date': datetime.now().isoformat()
            }
            
            self.books.append(book)
            return True
            
        except ValueError as e:
            print(f"❌ 도서 추가 실패: {e}")
            return False
    
    def get_monthly_stats(self, year: int, month: int) -> Dict:
        """
        특정 월의 독서 통계를 반환합니다.
        
        Args:
            year (int): 연도
            month (int): 월 (1-12)
            
        Returns:
            Dict: 월별 독서 통계
                - 'books_read': 읽은 도서 수
                - 'total_pages': 총 페이지 수  
                - 'avg_rating': 평균 평점
                - 'favorite_genre': 가장 많이 읽은 장르
                
        Examples:
            >>> stats = tracker.get_monthly_stats(2024, 10)
            >>> print(stats['books_read'])
            5
        """
        monthly_books = [
            book for book in self.books
            if datetime.strptime(book['finish_date'], '%Y-%m-%d').year == year
            and datetime.strptime(book['finish_date'], '%Y-%m-%d').month == month
        ]
        
        if not monthly_books:
            return {
                'books_read': 0,
                'total_pages': 0,
                'avg_rating': 0,
                'favorite_genre': None
            }
        
        # 장르별 통계
        genre_counts = {}
        for book in monthly_books:
            genre_counts[book['genre']] = genre_counts.get(book['genre'], 0) + 1
        
        favorite_genre = max(genre_counts, key=genre_counts.get) if genre_counts else None
        
        return {
            'books_read': len(monthly_books),
            'total_pages': sum(book['pages'] for book in monthly_books),
            'avg_rating': round(sum(book['rating'] for book in monthly_books) / len(monthly_books), 2),
            'favorite_genre': favorite_genre
        }
    
    def get_recommendations(self, count: int = 3) -> List[str]:
        """
        읽은 책 패턴을 바탕으로 추천을 제공합니다.
        
        Args:
            count (int): 추천할 도서 수
            
        Returns:
            List[str]: 추천 도서 리스트
            
        Examples:
            >>> recommendations = tracker.get_recommendations(3)
            >>> print(recommendations)
            ['파이썬 완벽 가이드', 'AI 프로그래밍', '데이터 과학 입문']
        """
        if not self.books:
            return ["독서 기록을 먼저 추가해주세요!"]
        
        # 선호 장르 분석
        genre_ratings = {}
        for book in self.books:
            genre = book['genre']
            if genre not in genre_ratings:
                genre_ratings[genre] = []
            genre_ratings[genre].append(book['rating'])
        
        # 평균 평점이 높은 장르 찾기
        avg_ratings = {
            genre: sum(ratings) / len(ratings)
            for genre, ratings in genre_ratings.items()
        }
        
        top_genres = sorted(avg_ratings.keys(), key=lambda x: avg_ratings[x], reverse=True)[:2]
        
        # 가상의 추천 도서 데이터베이스
        recommendations_db = {
            'IT': ['파이썬 완벽 가이드', 'AI 프로그래밍', '데이터 과학 입문', '클린 코드'],
            '자기계발': ['아침형 인간', '습관의 힘', '부의 추월차선', '미라클 모닝'],
            '소설': ['미움받을 용기', '연금술사', '데미안', '어린 왕자'],
            '경제경영': ['부자 아빠 가난한 아빠', '투자의 정석', '경제학 콘서트', '넛지'],
            '과학': ['코스모스', '사피엔스', '총 균 쇠', '이기적 유전자']
        }
        
        # 선호 장르에서 추천
        recommendations = []
        for genre in top_genres:
            if genre in recommendations_db:
                available_books = recommendations_db[genre]
                # 이미 읽은 책 제외
                read_titles = [book['title'] for book in self.books]
                new_books = [book for book in available_books if book not in read_titles]
                recommendations.extend(new_books[:count//2])
        
        # 부족한 경우 다른 장르에서 보충
        if len(recommendations) < count:
            all_recommendations = []
            for books in recommendations_db.values():
                all_recommendations.extend(books)
            
            read_titles = [book['title'] for book in self.books]
            remaining = [book for book in all_recommendations 
                        if book not in read_titles and book not in recommendations]
            recommendations.extend(remaining[:count - len(recommendations)])
        
        return recommendations[:count]


class ReadingVisualizer:
    """
    독서 데이터 시각화 클래스
    """
    
    def __init__(self, tracker: BookTracker):
        """ReadingVisualizer를 초기화합니다."""
        self.tracker = tracker
        plt.rcParams['font.family'] = 'Malgun Gothic'
        plt.rcParams['axes.unicode_minus'] = False
    
    def create_annual_report(self, year: int) -> None:
        """
        연간 독서 리포트를 생성합니다.
        
        Args:
            year (int): 리포트 생성할 연도
            
        Examples:
            >>> visualizer.create_annual_report(2024)
        """
        if not self.tracker.books:
            print("📚 표시할 독서 데이터가 없습니다.")
            return
        
        # 해당 연도 데이터 필터링
        yearly_books = [
            book for book in self.tracker.books
            if datetime.strptime(book['finish_date'], '%Y-%m-%d').year == year
        ]
        
        if not yearly_books:
            print(f"📚 {year}년 독서 기록이 없습니다.")
            return
        
        fig, ((ax1, ax2), (ax3, ax4)) = plt.subplots(2, 2, figsize=(16, 12))
        fig.suptitle(f'📚 {year}년 독서 연간 리포트', fontsize=20, fontweight='bold')
        
        # 데이터 준비
        df = pd.DataFrame(yearly_books)
        df['finish_date'] = pd.to_datetime(df['finish_date'])
        df['month'] = df['finish_date'].dt.month
        
        # 그래프 1: 월별 독서량
        monthly_books = df.groupby('month').size()
        monthly_pages = df.groupby('month')['pages'].sum()
        
        ax1_twin = ax1.twinx()
        bars1 = ax1.bar(monthly_books.index, monthly_books.values, 
                       alpha=0.7, color='#4ECDC4', label='도서 수')
        line1 = ax1_twin.plot(monthly_pages.index, monthly_pages.values, 
                            'ro-', linewidth=2, markersize=6, color='#FF6B6B', label='페이지 수')
        
        ax1.set_title('📈 월별 독서량', fontsize=14, fontweight='bold')
        ax1.set_xlabel('월', fontsize=12)
        ax1.set_ylabel('도서 수', fontsize=12)
        ax1_twin.set_ylabel('페이지 수', fontsize=12)
        ax1.legend(loc='upper left')
        ax1_twin.legend(loc='upper right')
        
        # 그래프 2: 장르별 분포
        genre_counts = df['genre'].value_counts()
        colors = plt.cm.Set3(range(len(genre_counts)))
        wedges, texts, autotexts = ax2.pie(genre_counts.values, labels=genre_counts.index,
                                          autopct='%1.1f%%', colors=colors, startangle=90)
        ax2.set_title('🥧 장르별 독서 분포', fontsize=14, fontweight='bold')
        
        # 그래프 3: 평점 분포
        rating_counts = df['rating'].value_counts().sort_index()
        bars3 = ax3.bar(rating_counts.index, rating_counts.values,
                       color=['#FF6B6B', '#FF9F43', '#FECA57', '#96CEB4', '#4ECDC4'])
        ax3.set_title('⭐ 평점 분포', fontsize=14, fontweight='bold')
        ax3.set_xlabel('평점', fontsize=12)
        ax3.set_ylabel('도서 수', fontsize=12)
        ax3.set_xticks(range(1, 6))
        
        # 막대 위에 수치 표시
        for bar, count in zip(bars3, rating_counts.values):
            ax3.text(bar.get_x() + bar.get_width()/2, bar.get_height() + 0.1,
                    str(count), ha='center', va='bottom', fontweight='bold')
        
        # 그래프 4: 페이지 수 분포
        ax4.hist(df['pages'], bins=10, alpha=0.7, color='#A55EEA', edgecolor='black')
        ax4.axvline(df['pages'].mean(), color='red', linestyle='--', 
                   label=f'평균: {df["pages"].mean():.0f}페이지')
        ax4.set_title('📄 페이지 수 분포', fontsize=14, fontweight='bold')
        ax4.set_xlabel('페이지 수', fontsize=12)
        ax4.set_ylabel('도서 수', fontsize=12)
        ax4.legend()
        
        plt.tight_layout()
        plt.show()
        
        # 연간 통계 출력
        total_books = len(yearly_books)
        total_pages = df['pages'].sum()
        avg_rating = df['rating'].mean()
        favorite_genre = genre_counts.index[0]
        
        print(f"\n📊 {year}년 독서 통계")
        print("=" * 40)
        print(f"📚 총 읽은 책: {total_books}권")
        print(f"📄 총 페이지: {total_pages:,}페이지")
        print(f"⭐ 평균 평점: {avg_rating:.1f}점")
        print(f"❤️  가장 좋아하는 장르: {favorite_genre}")
        print(f"🎯 목표 달성률: {(total_books/self.tracker.goals['yearly_books'])*100:.1f}%")


def main_reading_system():
    """독서 관리 시스템 메인 함수"""
    print("📚 개인 독서 기록 및 리뷰 시스템")
    print("=" * 50)
    
    tracker = BookTracker()
    visualizer = ReadingVisualizer(tracker)
    
    # 샘플 데이터 추가
    sample_books = [
        ("파이썬 입문", "김개발", "IT", 300, "2024-09-15", 5, "프로그래밍 기초를 잘 설명한 책"),
        ("습관의 힘", "찰스 두히그", "자기계발", 350, "2024-09-20", 4, "습관 형성에 대한 과학적 접근"),
        ("코스모스", "칼 세이건", "과학", 450, "2024-10-01", 5, "우주에 대한 경이로운 이야기"),
        ("미움받을 용기", "기시미 이치로", "자기계발", 380, "2024-10-10", 4, "아들러 심리학의 핵심"),
        ("클린 코드", "로버트 마틴", "IT", 400, "2024-10-15", 5, "깨끗한 코드 작성법")
    ]
    
    for book in sample_books:
        tracker.add_book(*book)
    
    while True:
        print("\n🏠 메인 메뉴")
        print("1. 📖 도서 추가")
        print("2. 📊 월별 통계")
        print("3. 📈 연간 리포트")
        print("4. 💡 추천 도서")
        print("5. 🎯 목표 설정")
        print("6. 🚪 종료")
        
        choice = input("\n선택하세요 (1-6): ").strip()
        
        if choice == "1":
            print("\n📖 새 도서 추가")
            print("-" * 20)
            # 도서 추가 로직 구현
            
        elif choice == "2":
            try:
                year = int(input("연도 입력: "))
                month = int(input("월 입력 (1-12): "))
                stats = tracker.get_monthly_stats(year, month)
                
                print(f"\n📊 {year}년 {month}월 독서 통계:")
                print(f"읽은 책: {stats['books_read']}권")
                print(f"총 페이지: {stats['total_pages']:,}페이지")
                print(f"평균 평점: {stats['avg_rating']}점")
                if stats['favorite_genre']:
                    print(f"선호 장르: {stats['favorite_genre']}")
            except ValueError:
                print("올바른 숫자를 입력하세요.")
                
        elif choice == "3":
            try:
                year = int(input("리포트 생성할 연도: "))
                visualizer.create_annual_report(year)
            except ValueError:
                print("올바른 연도를 입력하세요.")
                
        elif choice == "4":
            recommendations = tracker.get_recommendations(5)
            print("\n💡 추천 도서:")
            for i, book in enumerate(recommendations, 1):
                print(f"  {i}. {book}")
                
        elif choice == "5":
            print("\n🎯 목표 설정")
            print(f"현재 연간 목표: {tracker.goals['yearly_books']}권")
            # 목표 설정 로직
            
        elif choice == "6":
            print("\n👋 프로그램을 종료합니다.")
            print("📚 독서를 통해 더 넓은 세상을 만나세요!")
            break
        else:
            print("❌ 올바른 번호를 선택하세요 (1-6).")


if __name__ == "__main__":
    main_reading_system()
```

---

## 📚 오늘 배운 내용 정리

### ✅ 핵심 포인트

**1. 데이터 시각화의 힘:**
- 📊 **숫자 → 그래프**: 복잡한 데이터를 한눈에 이해할 수 있는 시각적 표현
- 📈 **matplotlib 활용**: 막대그래프, 꺾은선그래프, 원그래프, 히스토그램 등 다양한 그래프
- 📋 **pandas 연동**: 데이터 분석과 시각화의 완벽한 조합
- 🎨 **사용자 친화적 디자인**: 색상, 레이블, 범례를 통한 가독성 향상

**2. 개발 환경 비교:**
- 🐳 **Docker**: 실무 환경에 최적화, 완전한 제어 가능, 팀 협업에 유리
- ☁️ **Colab**: 학습과 프로토타이핑에 최적화, 즉시 시작 가능, 무료 GPU 제공
- ⚖️ **선택 기준**: 프로젝트 규모, 협업 필요성, 배포 계획에 따른 환경 선택

**3. 코드 문서화 마스터:**
- 📝 **Google Style Docstring**: Args, Returns, Examples, Raises 섹션 활용
- 💡 **실용적 문서화**: 코드의 '무엇'보다 '왜'와 '어떻게'에 집중
- 🔍 **타입 힌트**: 함수 매개변수와 반환값에 타입 정보 명시
- 📚 **프로젝트 문서화**: README, 사용자 가이드, 개발자 가이드 작성

**4. 종합 프로젝트 설계:**
- 🏗️ **클래스 설계**: 단일 책임 원칙에 따른 기능별 클래스 분리
- 🔄 **데이터 흐름**: 입력 → 검증 → 저장 → 분석 → 시각화의 체계적 처리
- 🛡️ **견고한 시스템**: 예외 처리와 입력 검증을 통한 안정성 확보
- 🎯 **사용자 경험**: 직관적인 메뉴와 명확한 피드백 제공

### 🏠 다음 주까지 해볼 과제

1. **시각화 실습**:
   - 본인의 실제 데이터로 다양한 그래프 만들기
   - matplotlib 고급 기능 탐구 (애니메이션, 3D 그래프 등)

2. **문서화 연습**:
   - 이전에 작성한 코드들에 완전한 docstring 추가
   - 프로젝트 README 파일 작성해보기

3. **실습과제 완성**:
   - 운동 기록 관리 시스템 완전 구현
   - 독서 기록 시스템 완전 구현
   - 추가 기능 개발 (데이터 내보내기, 백업 등)

4. **심화 학습**:
   - seaborn 라이브러리로 더 고급 시각화
   - plotly를 활용한 인터랙티브 그래프

### 🔮 다음 주 예고

**11주차: AI 라이브러리 활용 I - YOLO 객체 탐지**
- 인공지능과 컴퓨터 비전의 기초 개념
- YOLO 라이브러리를 활용한 실시간 객체 탐지
- 이미지 처리와 결과 시각화
- 객체 탐지 결과를 활용한 애플리케이션 개발

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
9주차: "모듈과 패키지로 대규모 시스템을 체계적으로 관리할 수 있다!" (구조화) ✅
10주차: "데이터를 의미 있는 시각화로 표현할 수 있다!" (시각화) ✅
```

**오늘 여러분이 할 수 있게 된 것들:**
- 📊 **데이터 스토리텔링**: 복잡한 데이터를 직관적인 그래프로 전달하기
- 🎨 **시각적 커뮤니케이션**: 한 장의 그래프로 천 마디 말 대신하기
- 📝 **전문적 문서화**: 다른 개발자들과 원활한 소통을 위한 코드 문서화
- 🏗️ **시스템 아키텍처**: 복잡한 요구사항을 체계적인 클래스 구조로 설계하기
- 🔄 **데이터 파이프라인**: 데이터 수집부터 시각화까지 전체 흐름 구축하기
- 🐳 **개발 환경 선택**: 프로젝트 특성에 맞는 최적의 개발 환경 판단하기

**데이터 시각화의 진정한 가치:**
오늘 배운 시각화는 단순한 그래프 그리기가 아닌, **데이터를 통한 인사이트 발견과 의사결정 지원**의 핵심 도구입니다. 이제 여러분은 복잡한 비즈니스 데이터를 분석하고, 이해관계자들에게 명확한 시각적 보고서를 제공할 수 있습니다.

**전문적 개발자로의 성장:**
코드 문서화와 프로젝트 구조화를 마스터한 여러분은 이제 **개인 개발자에서 팀 개발자로**, **취미 프로그래머에서 전문 소프트웨어 엔지니어로** 성장했습니다.

**실무 역량 완성:**
- 📈 **데이터 분석가**: pandas와 matplotlib로 비즈니스 인텔리전스 구현
- 🎨 **프론트엔드 개발자**: 사용자 친화적인 인터페이스 설계 능력
- 🏗️ **백엔드 개발자**: 견고하고 확장 가능한 시스템 아키텍처 설계
- 📚 **기술 문서 작성자**: 복잡한 시스템을 명확하게 설명하는 커뮤니케이션 능력

**마지막 격려:**
10주차를 완주하신 여러분은 이제 진정한 **데이터 드리븐 개발자**가 되었습니다! 데이터를 수집하고, 분석하고, 시각화하여 의미있는 인사이트를 도출할 수 있으며, 이를 체계적으로 문서화하여 다른 사람들과 공유할 수 있습니다.

앞으로 2주간은 최신 AI 기술을 다룰 예정입니다. 여러분이 쌓아온 탄탄한 기초 위에 인공지능이라는 날개를 달아보세요! 🚀

---

**🎯 10주차 학습 완료! 수고하셨습니다! 🎉**