# 컴포넌트: 날짜 & 시간 선택기 (Date & Time Picker)

## 개요
사용자가 특정 날짜, 날짜 범위, 또는 시간을 선택할 수 있는 폼 컴포넌트. Input 트리거와 팝오버 Picker로 구성.

---

## 디자인 토큰

| 토큰 | 값 |
|---|---|
| 트리거 배경 | `color/surface/1` |
| 트리거 보더 | 1px solid `color/border/default` |
| 트리거 보더 반경 | `radius/input` = 8px |
| 팝오버 배경 | `color/surface/1` |
| 팝오버 보더 반경 | `radius/dropdown` = 10px |
| 팝오버 그림자 | `shadow/dropdown` |
| 팝오버 패딩 | `spacing/16` (16px) |
| 폰트 | 13px / Regular 400 |
| 셀 크기 | `size/XL` (36px) × `size/XL` (36px) |
| 셀 보더 반경 | `radius/M` (8px) |
| 포커스 링 | `shadow/focus` |

---

## 구성 요소

### Date Picker Trigger
- Input 스타일 트리거 + 우측 `calendar_today` 아이콘 (Icons 페이지 인스턴스)
- Height: Input과 동일 Size 토큰 (`size/input/*`)

### Date Picker Popover
- **Header**: 월/년 레이블 + 이전/다음 버튼 (`chevron_left`, `chevron_right` 아이콘 인스턴스)
- **Weekday Row**: 월~일 2자 약어, `color/text/tertiary`
- **Day Grid**: 6행 × 7열, 각 셀 36×36
- **Footer**: (옵션) Today / Clear 액션 버튼

### Time Picker Popover
- 시/분/(초) 컬럼 스크롤러 또는 숫자 Input + 증감 버튼
- 12h/24h 전환 지원

### Date & Time Picker (결합)
- 좌측 Date Grid + 우측 Time Column

### Date Range Picker
- 두 개 월 그리드 나란히 표시
- 시작일 → 종료일 선택, 사이 구간 하이라이트

---

## 셀 상태

| 상태 | 배경 | 텍스트 |
|---|---|---|
| 기본 | transparent | `color/text/primary` |
| 호버 | `color/surface/2` | `color/text/primary` |
| 선택 | `color/primary/default` | `color/primary/on-primary` |
| 범위 내(시작·종료 사이) | `color/primary/subtle` | `color/primary/default` |
| 오늘 | transparent | `color/primary/default` + 밑줄 또는 보더 |
| 다른 달 | transparent | `color/text/tertiary` |
| 비활성(min/max 범위 밖) | transparent | `color/text/tertiary`, 커서 not-allowed |

---

## 사이즈 동작

| 요소 | layoutSizingHorizontal | layoutSizingVertical |
|---|---|---|
| Trigger | `FILL` 또는 `HUG` | `HUG` (Size 토큰 기준) |
| Popover | `HUG` | `HUG` |
| Day Cell | `FIXED` (36px) | `FIXED` (36px) |

> Trigger와 Popover는 콘텐츠 기반 HUG. 각 Day 셀만 고정 크기. 임의 px 값으로 Fixed 지정 금지(셀 제외).

---

## 접근성
- Trigger: `aria-haspopup="dialog"`, `aria-expanded`, 포커스 가능
- Popover: `role="dialog"`, `aria-modal="true"`
- Day Grid: `role="grid"`, 각 셀 `role="gridcell"`
- 키보드: ← → ↑ ↓ 날짜 이동, PageUp/Down 월 이동, Enter 선택
- 스크린리더: 선택된 날짜 전체 형식으로 읽기 ("2026년 4월 10일 금요일")

---

### Variants 구성
- 모든 변형은 Figma의 **Combine as Variants** 기능을 사용하여 하나의 Component Set으로 통합한다.

---

### 아이콘 사용 규칙
- 트리거의 캘린더 아이콘(`calendar_today`)과 헤더의 이전/다음 쉐브론(`chevron_left`, `chevron_right`)은 반드시 `01 — Icons` 페이지에 정의된 아이콘 컴포넌트 인스턴스를 사용한다.
- 유니코드 문자, 특수 기호 텍스트(📅, ◀, ▶ 등)로 아이콘을 대체하는 것을 금지한다.
- 아이콘 크기는 컴포넌트의 사이즈 변형에 맞춰 조정한다.

---

## Figma Make 프롬프트

```
다음 스펙으로 날짜 & 시간 선택기(Date & Time Picker) 컴포넌트를 만들어줘:

변형: Date Picker, Time Picker, Date & Time Picker, Date Range Picker

Trigger:
- Input 스타일 (Input 컴포넌트 재사용)
- 우측에 calendar_today 아이콘 (Icons 페이지 인스턴스, 텍스트 기호 금지)
- Height에는 Size/Semantic Variables (size/input/*) 바인딩

Popover:
- 배경 흰색, 보더 반경 10px, 그림자 shadow/dropdown
- 패딩 16px
- Header: 월/년 레이블 + chevron_left, chevron_right 아이콘 버튼 (Icons 페이지 인스턴스)
- Weekday Row: 월 화 수 목 금 토 일 (회색)
- Day Grid: 6×7, 각 셀 36×36px, 보더 반경 8px
- 셀 상태: 기본/호버/선택(오렌지)/범위(오렌지 틴트)/오늘/다른 달/비활성

Time Picker:
- 시 분 컬럼 숫자 입력 또는 스크롤러
- 12h/24h 전환

네이밍: Date Picker / Trigger, Date Picker / Popover, Time Picker / Popover
```
