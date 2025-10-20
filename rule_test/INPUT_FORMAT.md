# 📝 표준 사용자 입력 포맷

## 기본 구조

```python
user = {
    # ========== 필수 필드 (기본 정보) ==========
    "age": 29.0,                                    # float - 나이
    "gender": "여성",                                # str - "남성" 또는 "여성"
    "weight": 60.0,                                 # float - 체중 (kg)
    
    # ========== 필수 필드 (운동 관련) ==========
    "training_experience": "초보",                   # str - "초보", "중급", "숙련자"
    "training_duration": "60-90",                   # str - "60-90", "<60", "90+"
    "training_time": "저녁",                         # str - "오전", "오후", "저녁", "밤"
    
    # ========== 필수 필드 (다이어트/목표) ==========
    "diet_phase": "체지방 감소",                      # str ㄴ- "체지방 감소", "유지", "벌크업"
    "user_goal": {"체지방 감소", "회복 지원"},        # set - 목표 집합
    
    # ========== 필수 필드 (건강/제약) ==========
    "health_conditions": {"유당 불내증", "수면장애"},  # set - 건강 상태
    "allergy": set(),                               # set - 알러지 (없으면 빈 set)
    "current_stack": set(),                         # set - 현재 복용 성분
    "is_dehydrated": False,                         # bool - 탈수 여부
    
    # ========== 선택적 필드 ==========
    "lean_mass": None,                              # Optional[float] - 제지방량 kg
    "training_intensity": None,                     # Optional[str] - "고", "중", "저"
    "diet_type": "일반식",                           # Optional[str] - "일반식", "채식 위주"
    "oral_hygiene": "해당 없음",                     # Optional[str]
    "workout_type": None,                           # Optional[str] - "유산소", "무산소"
    "environment_heat_humid": None,                 # Optional[str] - "실내", "고온", "고온다습"
}
```

## 실제 사용 예시

### 예시 1: 초보 여성 다이어터 (복잡한 제약)
```python
user = {
    "age": 29.0,
    "gender": "여성",
    "weight": 60.0,
    "lean_mass": None,
    "training_experience": "초보",
    "training_duration": "60-90",
    "training_time": "저녁",
    "diet_phase": "체지방 감소",
    "user_goal": {"체지방 감소", "회복 지원"},
    "health_conditions": {"유당 불내증", "수면장애"},
    "allergy": set(),
    "current_stack": set(),
    "is_dehydrated": False,
    "diet_type": "일반식",
    "oral_hygiene": "해당 없음"
}
```

### 예시 2: 숙련 남성 벌크업 (건강)
```python
user = {
    "age": 30.0,
    "gender": "남성",
    "weight": 85.0,
    "lean_mass": 70.0,
    "training_experience": "숙련자",
    "training_duration": "90+",
    "training_time": "오전",
    "diet_phase": "벌크업",
    "user_goal": {"근성장", "퍼포먼스"},
    "health_conditions": set(),
    "allergy": set(),
    "current_stack": set(),
    "is_dehydrated": False,
}
```

### 예시 3: 최소 필수 필드만 사용
```python
user = {
    "age": 25.0,
    "gender": "남성",
    "weight": 75.0,
    "training_experience": "중급",
    "training_duration": "60-90",
    "training_time": "저녁",
    "diet_phase": "유지",
    "user_goal": {"퍼포먼스"},
    "health_conditions": set(),
    "allergy": set(),
    "current_stack": set(),
    "is_dehydrated": False,
}
```

## 필드별 가능한 값

### gender (성별)
- "남성" 또는 "여성"

### training_experience (운동 경험)
- "초보", "중급", "숙련자"

### training_duration (운동 시간)
- "<60" (60분 미만)
- "60-90" (60-90분)
- "90+" (90분 이상)

### training_time (운동 시간대)
- "오전", "오후", "저녁", "밤"

### diet_phase (다이어트 단계)
- "체지방 감소", "유지", "벌크업"

### user_goal (목표) - **set 타입**
- "체지방 감소"
- "회복" 또는 "회복 지원" (부분 매칭)
- "근성장"
- "퍼포먼스"
- "집중력"

### health_conditions (건강 상태) - **set 타입**
- "수면장애"
- "유당 불내증"
- "신장 질환"
- "저혈압"
- "고혈압"
- "불안장애"
- set() (없으면 빈 set)

## 중요 참고사항

1. **Set 타입 사용**: user_goal, health_conditions, allergy, current_stack
2. **빈 값은 set()**: []가 아님
3. **부분 매칭 지원**: "회복"과 "회복 지원" 모두 인식
4. **대소문자 정확히**: "여성" (O), "Female" (X)
5. **lean_mass가 None**: 자동으로 weight 기반 계산

## 변경사항 (2025-10-20)

- `disease_flag` → `health_conditions` (CSV와 일치)

