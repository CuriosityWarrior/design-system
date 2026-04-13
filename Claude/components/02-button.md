# 컴포넌트: 버튼 (Button)

## 개요
사용자의 액션을 트리거하는 클릭 가능한 인터랙티브 요소. 디자인 시스템의 가장 기본적인 컴포넌트.

---

## 디자인 토큰

| 토큰 | 값 |
|---|---|
| 폰트 | Pretendard, `text/label-*` (크기별 상이) |
| 포커스 링 | `shadow/focus` = 0 0 0 3px rgba(242,106,0,0.20) |
| 호버 모션 | 100ms cubic-bezier(0, 0, 0.2, 1) |
| 프레스 모션 | 50ms cubic-bezier(0.4, 0, 0.2, 1) |

---

## 변형 (Variant)

버튼은 시각적 스타일에 따라 **Fill / Border / Text** 3가지 대분류로 나뉘며, 각 대분류 안에 **Primary / Secondary** 강조 단계가 존재한다. 추가로 특수 목적의 **Subtle**, **Danger** 변형이 있다.

### 변형 구조 요약

| 대분류 | 강조 | 설명 |
|---|---|---|
| **Fill** | Primary | 채워진 브랜드 컬러 배경. 가장 강한 시각적 강조 |
| **Fill** | Secondary | 채워진 뉴트럴 배경. 보조적 강조 |
| **Border** | Primary | 브랜드 컬러 보더. 중간 강조 |
| **Border** | Secondary | 뉴트럴 보더. 낮은 강조 |
| **Text** | Primary | 브랜드 컬러 텍스트만. 최소 강조 |
| **Text** | Secondary | 뉴트럴 텍스트만. 최소 강조 보조 |
| **Subtle** | — | 연한 브랜드 배경. 저강조 CTA |
| **Danger** | — | 에러 컬러 배경. 삭제/위험 액션 전용 |

---

### Fill / Primary
- **배경**: `color/primary/default` (#F26A00)
- **텍스트**: `color/primary/on-primary` (#FFFFFF)
- **호버**: 배경 → `color/primary/hover` (#C75200)
- **액티브**: 배경 → `color/primary/active` (#9C3D00)
- **사용처**: 주요 CTA, 저장, 확인

### Fill / Secondary
- **배경**: `color/neutral/100` (#F0F0F0)
- **텍스트**: `color/text/primary`
- **호버**: 배경 → `color/neutral/200` (#E0E0E0)
- **액티브**: 배경 → `color/neutral/300` (#D0D0D0)
- **사용처**: 보조 액션, 덜 강조된 CTA, 주요 버튼과 나란히 배치 시

### Border / Primary
- **배경**: transparent
- **텍스트**: `color/primary/default`
- **보더**: 1px solid `color/primary/default`
- **호버**: 배경 → `color/primary/subtle`
- **사용처**: 인라인 액션, 경계선이 있는 브랜드 보조 버튼

### Border / Secondary
- **배경**: `color/surface/1`
- **텍스트**: `color/text/primary`
- **보더**: 1px solid `color/border/default`
- **호버**: 보더 → `color/border/strong`, 배경 → `color/surface/2`
- **사용처**: 보조 액션, 취소, 뉴트럴 톤 보조 버튼

### Text / Primary
텍스트만으로 구성된 브랜드 컬러 버튼. 배경도 보더도 없이 레이블 텍스트만 존재한다.

| 속성 | Default | Hover | Focus | Disabled |
|---|---|---|---|---|
| 배경 | 없음 `[]` | `color/primary/subtle` (#FFF5ED) | 없음 `[]` | 없음 `[]` |
| 보더 | 없음 `[]` | 없음 `[]` | 없음 `[]` | 없음 `[]` |
| 텍스트 색상 | `color/primary/default` | `color/primary/hover` (#C75200) | `color/primary/default` | `color/primary/default` |
| 포커스 링 | — | — | `shadow/focus` (3px 오렌지) | — |
| 불투명도 | 1 | 1 | 1 | 0.4 |

- **사용처**: 최소 강조 액션, 링크성 버튼, "더 보기", "취소" 등
- **Figma 속성**: `fills: []`, `strokes: []`, `strokeWeight: 0`

### Text / Secondary
텍스트만으로 구성된 뉴트럴 컬러 버튼.

| 속성 | Default | Hover | Focus | Disabled |
|---|---|---|---|---|
| 배경 | 없음 `[]` | `color/neutral/100` (#F0F0F0) | 없음 `[]` | 없음 `[]` |
| 보더 | 없음 `[]` | 없음 `[]` | 없음 `[]` | 없음 `[]` |
| 텍스트 색상 | `color/text/secondary` | `color/text/primary` | `color/text/secondary` | `color/text/secondary` |
| 포커스 링 | — | — | `shadow/focus` (3px 오렌지) | — |
| 불투명도 | 1 | 1 | 1 | 0.4 |

- **사용처**: 최소 강조 보조 액션, 뉴트럴 톤 인라인 액션
- **Figma 속성**: `fills: []`, `strokes: []`, `strokeWeight: 0`

> ⚠️ **Border vs Text 차이점**
>
> | 구분 | Border | Text |
> |---|---|---|
> | 보더 | 1px solid (브랜드 또는 뉴트럴) | **없음** |
> | 배경 (Default) | transparent 또는 surface | transparent |
> | 시각적 인상 | 테두리가 있는 버튼 | 텍스트만 있는 링크형 버튼 |
>
> Border 버튼을 클론하여 Text 버튼을 생성할 경우, 반드시 `strokes: []`, `strokeWeight: 0`으로 변경해야 한다.

### Subtle (저강조)
- **배경**: `color/primary/subtle`
- **텍스트**: `color/primary/default`
- **호버**: 배경 → `color/primary/tint`
- **사용처**: 저강조 CTA

### Danger (위험)
- **배경**: `color/error/default`
- **텍스트**: #FFFFFF
- **호버**: 배경 → `color/error/text`
- **사용처**: 삭제, 위험 액션

---

## 크기 (Size)

> 📐 Height는 [파운데이션: 사이즈](../foundations/07-size.md)의 Semantic T-Shirt 토큰을 참조한다. Width는 콘텐츠에 따라 가변.
> 📐 보더 반경은 [파운데이션: 레디우스](../foundations/05-radius.md)의 Semantic 토큰을 참조한다.

| 크기 | Height 토큰 | Height | Radius 토큰 | 폰트 토큰 | 패딩 (세로 × 가로) |
|---|---|---|---|---|---|
| XL | `size/XL` | 48px | `radius/M` (8px) | `text/label-lg` (16px SemiBold) | 14px 20px |
| L | `size/L` | 40px | `radius/M` (8px) | `text/label-md` (14px SemiBold) | 11px 16px |
| M | `size/M` | 32px | `radius/M` (8px) | `text/label-sm` (13px SemiBold) | 8px 12px |
| S | `size/S` | 24px | `radius/S` (6px) | `text/label-xs` (12px Medium) | 4px 8px |

---

## 상태 (State)

| 상태 | 설명 |
|---|---|
| Default | 기본 상태 |
| Hover | 배경/색상 미세 변화 — 100ms ease-out |
| Active / Pressed | 더 어두운 색상 — 50ms ease-in-out, scale(0.97) |
| Focus | `shadow/focus` 링 (오렌지, 3px) |
| Disabled | opacity 0.4, 커서 not-allowed, 포인터 이벤트 없음 |
| Loading | 텍스트 숨김, 중앙 스피너 오버레이 |

---

## 아이콘 포함
- 아이콘은 레이블 좌측 또는 우측, `spacing/8` 간격
- 아이콘은 `01 — Icons` 페이지의 인스턴스 사용 (텍스트 기호 금지)
- 아이콘 크기는 버튼 사이즈의 폰트 크기에 맞춤

---

## 접근성
- 아이콘 전용 버튼은 `aria-label` 필수
- 비활성 상태: `aria-disabled="true"` 사용
- 포커스 링 항상 표시
- 최소 터치 영역: 높이 44px (XL 사이즈 충족, L/M/S는 터치 타깃 확보 필요)

---

## 사이즈 동작

| 속성 | 값 |
|---|---|
| layoutSizingHorizontal | `HUG` |
| layoutSizingVertical | `HUG` |

> Width, Height 모두 콘텐츠 + 패딩 기준으로 자동 결정된다. 임의 px 값으로 Fixed 지정 금지.

---

## Figma Make 프롬프트

```
다음 스펙으로 버튼(Button) 컴포넌트를 만들어줘:

대분류 3가지: Fill, Border, Text
각 대분류에 강조 2단계: Primary, Secondary
특수 변형: Subtle, Danger

크기: XL (48px, 패딩 14px 20px, radius 8px), L (40px, 패딩 11px 16px, radius 8px), M (32px, 패딩 8px 12px, radius 8px), S (24px, 패딩 4px 8px, radius 6px)
Height에는 Size/Semantic Variables (size/XL, L, M, S) 바인딩
폰트: Pretendard SemiBold 600 (S는 Medium 500)

Fill/Primary: 배경 #F26A00, 흰색 텍스트, 호버 #C75200
Fill/Secondary: 배경 #F0F0F0(neutral/100), 검정 텍스트, 호버 #E0E0E0(neutral/200)
Border/Primary: 투명 배경, 오렌지 보더(1px solid), 오렌지 텍스트, 호버 시 연한 오렌지 배경
Border/Secondary: 흰색 배경, 1px 회색 보더, 호버 시 보더 진해짐
Text/Primary: 배경·보더 없음(strokes:[], strokeWeight:0), 오렌지 텍스트, 호버 시 연한 오렌지 배경
Text/Secondary: 배경·보더 없음, 회색 텍스트(text/secondary), 호버 시 연한 뉴트럴 배경
Subtle: 연한 오렌지 배경, 오렌지 텍스트
Danger: 배경 #E8321E, 흰색 텍스트

상태: Default, Hover, Active, Focus(3px 오렌지 링), Disabled(40% 불투명도), Loading(스피너)

Combine as Variants 적용.
네이밍: Button / {대분류} / {강조} / {크기} / {상태}
```
