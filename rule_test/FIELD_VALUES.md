# 📋 필드별 가능한 값 리스트 (CSV 룰베이스 기반)

## 🔹 user_goal (목표) - **set 타입**

### 룰베이스에서 추출한 값:
- `"회복"` 또는 `"회복 지원"` (부분 매칭 지원)
- `"퍼포먼스"`
- `"근성장"`
- `"체지방 감소"`
- `"집중력"`
- `"고온환경"`
- `"근력_향상"` (Glutamine에서 금지)
- `"근성장_촉진"` (Glutamine에서 금지)
- `"펌핑감"` (Betaine에서 금지)

### 권장 사용 값:
```python
user_goal = {"회복", "퍼포먼스", "근성장", "체지방 감소", "집중력"}
```

---

## 🔹 health_conditions (건강 상태) - **set 타입**

### 룰베이스에서 추출한 값:
- `"신장 질환"` (Creatine, Glutamine 금지)
- `"수면장애"` (Caffeine 금지)
- `"고혈압"` (Caffeine 금지)
- `"불안장애"` (Caffeine 금지)
- `"저혈압"` (Arginine 금지)
- `"MELAS"` (Arginine 금지)
- `"유당 불내증"` (Whey Protein/Casein → WPI/WPH 권장)

### 사용 예시:
```python
health_conditions = {"유당 불내증", "수면장애"}
# 또는 건강 문제 없으면
health_conditions = set()
```

---

## 🔹 allergy (알러지) - **set 타입**

### 제품 메타데이터에서 추출한 알러젠:
- `"우유"`
- `"대두"`
- `"계란"`
- `"생선"`
- `"조개류"`
- `"견과류"`
- `"땅콩"`
- `"밀"`
- `"참깨"`

### 추가 가능한 알러지 관련:
- `"카페인 민감성"` (custom, Caffeine 관련)
- `"글루텐 불내증"` (밀 관련)

### 사용 예시:
```python
allergy = {"우유", "대두"}
# 또는 알러지 없으면
allergy = set()
```

---

## 🔹 diet_type (식단 타입)

### 룰베이스에서 추출한 값:
- `"채식 위주"` (Creatine 추가 권장)
- `"일반식"`

---

## 🔹 workout_time / training_time (운동 시간대)

### 룰베이스에서 추출한 값:
- `"저녁"` (Caffeine 용량 감소, Casein 용량 증가)
- `"밤"` (Casein 용량 증가)
- `"오전"`
- `"오후"`

---

## 🔹 workout_environment / environment_heat_humid (운동 환경)

### 룰베이스에서 추출한 값:
- `"고온다습"` (Glycerol 증가, Nitrate 금지)
- `"고온"` (Taurine 권장, Betaine 경고, Glutamine 권장)
- `"실내"`

---

## 🔹 workout_type (운동 유형)

### 룰베이스에서 추출한 값:
- `"유산소"` (Casein 금지)
- `"무산소"`

---

## 🔹 oral_hygiene (구강 위생)

### 룰베이스에서 추출한 값:
- `"구강청결제 사용"` (Nitrate에 경고)
- `"해당 없음"`

---

## 🔹 exercise_type (운동 종류)

### 룰베이스에서 추출한 값:
- `"장시간_고강도_지구력"` (Glutamine 권장)

---

## 🔹 training_intensity (운동 강도)

### 룰베이스에서 추출한 값:
- `"고"` (L-Carnitine 2g)
- `"중"`
- `"저"`

---

## 🔹 current_stack (현재 복용 중인 성분) - **set 타입**

### 룰베이스에서 추출한 값:
- `"caffeine"` (L-theanine 시너지, Taurine 금지)

### 사용 예시:
```python
current_stack = {"caffeine", "creatine"}
# 또는 아무것도 복용 중이지 않으면
current_stack = set()
```

---

## 🔹 intake_period (섭취 기간)

### 룰베이스에서 추출한 값:
- `"만성"` (L-Carnitine 경고)

---

## 🔹 cvd_risk (심혈관 위험)

### 룰베이스에서 추출한 값:
- `True` 또는 `"예"` (L-Carnitine 경고)
- `False`

---

## 🔹 is_dehydrated (탈수 여부)

### 룰베이스에서 추출한 값:
- `True` (Creatine 금지)
- `False`

---

## 📊 전체 예시 (모든 필드 포함)

```python
user = {
    # 기본 정보
    "age": 29.0,
    "gender": "여성",
    "weight": 60.0,
    "lean_mass": None,
    
    # 운동 정보
    "training_experience": "초보",
    "training_duration": "60-90",
    "training_time": "저녁",
    "training_intensity": "고",
    
    # 다이어트/목표
    "diet_phase": "체지방 감소",
    "diet_type": "일반식",
    "user_goal": {"체지방 감소", "회복"},
    
    # 건강/제약 (set 타입)
    "health_conditions": {"유당 불내증", "수면장애"},
    "allergy": {"우유", "대두"},
    "current_stack": {"creatine"},
    "is_dehydrated": False,
    "cvd_risk": False,
    
    # 운동 환경/타입
    "workout_type": "무산소",
    "workout_environment": "실내",
    "exercise_type": None,
    
    # 기타
    "oral_hygiene": "해당 없음",
    "intake_period": None,
}
```

---

## 💡 주요 참고사항

1. **Set 타입 필드**: `user_goal`, `health_conditions`, `allergy`, `current_stack`
   - 중괄호 `{}` 사용
   - 빈 값은 `set()` (리스트 `[]` 아님!)

2. **부분 매칭**: 
   - "회복"과 "회복 지원" 모두 인식됨
   - "퍼포먼스"의 다양한 표현 가능

3. **대소문자**: 정확히 입력 (예: "여성" O, "Female" X)

4. **룰베이스 확장**: 
   - `rulebased.csv` 파일에 새로운 조건 추가 시 이 값들도 확장 가능

