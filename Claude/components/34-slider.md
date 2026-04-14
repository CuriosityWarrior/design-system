# 컴포넌트: 슬라이더 (Slider)

## 개요
사용자가 연속적인 범위 내에서 값을 선택할 수 있는 드래그 컨트롤. 볼륨, 밝기, 가격 범위 등에 사용.

---

## 디자인 토큰

| 토큰 | 값 |
|---|---|
| 트랙 배경 | `color/surface/3` |
| 트랙 활성 | `color/primary/default` |
| 썸 배경 | `color/common/white` (#FFFFFF) |
| 썸 보더 | 2px solid `color/primary/default` |
| 썸 그림자 | 0 1px 3px rgba(0,0,0,0.15) |
| 트랙 높이 | 4px |
| 썸 크기 | 20 × 20px |
| 보더 반경 (트랙/썸) | `radius/FULL` (9999px — pill 형태) |
| 포커스 링 | `shadow/focus` (썸에 적용) |
| 모션 | 100ms ease-out |

---

## 변형 (Variant)

### Single (기본)
- 하나의 썸, 단일 값 선택
- 예: 볼륨, 밝기

### Range
- 두 개의 썸, 시작-종료 범위 선택
- 두 썸 사이 트랙 구간은 활성 색상으로 채움
- 예: 가격 범위 필터

### With Ticks
- 트랙 하단에 눈금 표시 (옵션)
- 눈금 간격: 토큰 값

### With Value Label
- 썸 위에 현재 값 툴팁 표시 (드래그 중 또는 상시)
- 툴팁 스타일: Tooltip 컴포넌트 재사용

---

## 구성 요소
- **Track**: 전체 범위 표시용 회색 막대
- **Active Track**: 현재 값까지 채워진 오렌지 막대
- **Thumb**: 드래그 가능한 원형 핸들
- **Tick Marks** (옵션): 스텝 위치 표시 점
- **Value Label** (옵션): 썸 상단 값 표시

---

## 크기 (Size)

| 크기 | 트랙 높이 | 썸 크기 |
|---|---|---|
| Medium (기본) | 4px | 20 × 20px |
| Small | 2px | 16 × 16px |

---

### Size/Spacing 토큰 바인딩

| 속성 | 토큰 | 값 |
|---|---|---|
| 트랙 높이 (Medium) | `size/4` | 4px |
| 트랙 높이 (Small) | `size/2` | 2px |
| 썸 크기 (Medium) | `size/20` | 20px |
| 썸 크기 (Small) | `size/XS` | 16px |
| 썸 보더 두께 | 2px |

> Figma에서 해당 속성에 Variables를 직접 바인딩한다. 임의 px 고정값 사용 금지.

---

## 상태 (State)

| 상태 | 트랙 활성 | 썸 |
|---|---|---|
| 기본 | `color/primary/default` | 흰색 + 오렌지 보더 |
| 호버 | `color/primary/default` | 썸 scale(1.1) |
| 드래그 / Active | `color/primary/active` | 썸 `shadow/focus` |
| 포커스 | `color/primary/default` | 썸 `shadow/focus` |
| 비활성 | `color/border/strong` | 회색 보더, opacity 0.4 |

---

## 사이즈 동작

| 속성 | 값 |
|---|---|
| layoutSizingHorizontal | `FILL` (부모 너비) |
| layoutSizingVertical | `FIXED` (썸 크기 기준) |

> 트랙은 부모 너비에 맞춰 늘어나고, 높이는 썸 영역 기준 고정. 임의 값 입력 금지.

---

## 접근성
- `role="slider"`
- `aria-valuemin`, `aria-valuemax`, `aria-valuenow` 필수
- `aria-label` 또는 `aria-labelledby`
- 키보드: ← → 1 step, PageUp/Down 큰 step, Home/End 끝값
- Range 변형: 두 썸 각각에 위 속성 적용

---

## 아이콘 사용 규칙

> 컴포넌트 내 아이콘은 반드시 `01 — Icons` 페이지의 아이콘 컴포넌트 인스턴스를 사용한다.
> 텍스트 특수 문자(✓, ✕, →, ⋯ 등), 이모지, 직접 그린 벡터 도형으로 아이콘을 대체하는 것을 금지한다.
> 필요한 아이콘이 없는 경우, 먼저 `01 — Icons` 페이지에 추가한 후 인스턴스를 참조한다.

---

### Variants 구성
- 모든 변형은 Figma의 **Combine as Variants** 기능을 사용하여 하나의 Component Set으로 통합한다.

---

## Figma Make 프롬프트

```
다음 스펙으로 슬라이더(Slider) 컴포넌트를 만들어줘:

변형: Single, Range, With Ticks, With Value Label
크기: Medium (트랙 4px, 썸 20px), Small (트랙 2px, 썸 16px)

Track:
- 높이 4px, 보더 반경 9999px (필 형태)
- 배경: 회색 (color/surface/3)
- Active Track: 오렌지 (color/primary/default)

Thumb:
- 20×20 원형
- 배경 흰색, 2px 오렌지 보더
- 그림자: 0 1px 3px rgba(0,0,0,0.15)
- 호버: scale(1.1)
- 포커스/드래그: 3px 오렌지 글로우 링

Range 변형: 두 개 썸, 사이 트랙은 오렌지
Value Label: 썸 위 Tooltip 인스턴스 재사용

너비는 부모에 Fill, 높이는 썸 기준 고정

네이밍: Slider / {Single|Range} / {크기} / {상태}
```
