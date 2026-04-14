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

버튼은 **Fill · Border · Text** 3가지 스타일 대분류로 나뉘며, 각 스타일마다 **Primary · Secondary · Danger** 3가지 강조 수준을 갖는다.

| 스타일 | 설명 |
|---|---|
| **Fill** | 배경이 채워진 버튼 |
| **Border** | 배경 없이 테두리만 있는 버튼 |
| **Text** | 배경·테두리 없이 텍스트만 있는 버튼 |

| 강조 | 설명 |
|---|---|
| **Primary** | 브랜드 컬러 기반 — 가장 높은 강조 |
| **Secondary** | 중립(Gray) 톤 — 보조 액션 |
| **Danger** | 에러/위험 컬러 기반 — 삭제 등 위험 액션 |

---

### Fill / Primary
- **배경**: `color/primary/default` (#F26A00 라이트 / #FF8A1E 다크)
- **텍스트**: `color/primary/on-primary` (#FFFFFF)
- **호버**: 배경 → `color/primary/hover` (#C75200)
- **액티브**: 배경 → `color/primary/active` (#9C3D00)
- **사용처**: 주요 CTA, 저장, 확인 — 화면 내 가장 높은 강조

### Fill / Secondary
- **배경**: `color/secondary/default` (neutral/600, #66635B)
- **텍스트**: `color/secondary/on-secondary` (#FFFFFF)
- **호버**: 배경 → `color/secondary/hover` (neutral/700, #47443E)
- **액티브**: 배경 → `color/secondary/active` (neutral/800, #2E2C27)
- **사용처**: 보조 CTA, 취소, 닫기 — Fill이되 주목도를 낮춘 보조 액션

### Fill / Danger
- **배경**: `color/error/default` (#E8321E)
- **텍스트**: `color/common/white` (#FFFFFF)
- **호버**: 배경 → `color/error/text` (#C72816 계열)
- **액티브**: 배경 → `color/error/active` (토큰 기반 호버 상태)
- **사용처**: 삭제 확인, 계정 탈퇴 등 되돌리기 어려운 위험 액션

---

### Border / Primary
- **배경**: transparent
- **텍스트**: `color/primary/default` (#F26A00)
- **보더**: 1px solid `color/primary/default`
- **호버**: 배경 → `color/primary/subtle` (#FFF5ED)
- **사용처**: 인라인 액션, 브랜드 컬러 강조가 필요한 보조 버튼

### Border / Secondary
- **배경**: `color/surface/1` (#FFFFFF)
- **텍스트**: `color/text/primary` (#1A1916)
- **보더**: 1px solid `color/border/default` (#E8E6E1)
- **호버**: 보더 → `color/border/strong` (#D4D1CA), 배경 → `color/surface/2` (#FAFAF8)
- **사용처**: 보조 액션, 취소 — 중립적 톤의 테두리 버튼

### Border / Danger
- **배경**: transparent
- **텍스트**: `color/error/default` (#E8321E)
- **보더**: 1px solid `color/error/default`
- **호버**: 배경 → `color/error/subtle` (연한 레드 배경)
- **사용처**: 삭제 버튼 중 시각적 무게를 줄인 보조 위험 액션

---

### Text / Primary
- **배경**: 없음 `[]`
- **텍스트**: `color/primary/default` (#F26A00)
- **보더**: 없음 `[]`
- **호버**: 텍스트 → `color/primary/hover` (#C75200), 배경 → `color/primary/subtle` (#FFF5ED)
- **사용처**: 최소 강조 액션, 링크성 버튼, "더 보기" 등

| 속성 | Default | Hover | Focus | Disabled |
|---|---|---|---|---|
| 배경 (fills) | 없음 `[]` | `color/primary/subtle` | 없음 `[]` | 없음 `[]` |
| 보더 (strokes) | 없음 `[]` | 없음 `[]` | 없음 `[]` | 없음 `[]` |
| 텍스트 색상 | `color/primary/default` | `color/primary/hover` | `color/primary/default` | `color/primary/default` |
| 포커스 링 | — | — | `shadow/focus` | — |
| 불투명도 | 1 | 1 | 1 | 0.4 |

### Text / Secondary
- **배경**: 없음 `[]`
- **텍스트**: `color/text/secondary` (#66635B)
- **보더**: 없음 `[]`
- **호버**: 텍스트 → `color/text/primary`, 배경 → `color/secondary/subtle` (neutral/50)
- **사용처**: 저강조 보조 액션, 부가 링크, 메타 액션 — 시각적 존재감을 최소화

| 속성 | Default | Hover | Focus | Disabled |
|---|---|---|---|---|
| 배경 (fills) | 없음 `[]` | `color/secondary/subtle` | 없음 `[]` | 없음 `[]` |
| 보더 (strokes) | 없음 `[]` | 없음 `[]` | 없음 `[]` | 없음 `[]` |
| 텍스트 색상 | `color/text/secondary` | `color/text/primary` | `color/text/secondary` | `color/text/secondary` |
| 포커스 링 | — | — | `shadow/focus` | — |
| 불투명도 | 1 | 1 | 1 | 0.4 |

### Text / Danger
- **배경**: 없음 `[]`
- **텍스트**: `color/error/default` (#E8321E)
- **보더**: 없음 `[]`
- **호버**: 텍스트 → `color/error/text`, 배경 → `color/error/subtle`
- **사용처**: 삭제 링크, 인라인 위험 텍스트 액션 — 최소 시각 무게의 위험 표현

---

## 크기 (Size)

> 📐 Height는 [파운데이션: 사이즈](../foundations/07-size.md)의 Semantic T-Shirt 토큰을 참조한다. Width는 콘텐츠에 따라 가변.
> 📐 보더 반경은 [파운데이션: 레디우스](../foundations/05-radius.md)의 Semantic 토큰을 참조한다.

| 크기 | Height 토큰 | Height | Radius 토큰 | 폰트 토큰 | 패딩 (세로 × 가로) |
|---|---|---|---|---|---|
| XL | `size/XL` | 48px | `radius/M` (8px) | `text/label-lg` (16px SemiBold) | 14px 20px |
| L | `size/L` | 40px | `radius/M` (8px) | `text/label-md` (14px SemiBold) | 11px 16px |
| M | `size/M` | 32px | `radius/S` (6px) | `text/label-sm` (13px SemiBold) | 8px 12px |
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
- 최소 터치 영역: 높이 44px (XL 사이즈 충족, L 이하는 터치 타깃 확보 필요)

---

## 사이즈 동작

| 속성 | 값 |
|---|---|
| layoutSizingHorizontal | `HUG` |
| layoutSizingVertical | `HUG` |

> Width, Height 모두 콘텐츠 + 패딩 기준으로 자동 결정된다. 임의 px 값으로 Fixed 지정 금지.

---

## Figma Variants 네이밍

```
Button / Fill / Primary / {크기} / {상태}
Button / Fill / Secondary / {크기} / {상태}
Button / Fill / Danger / {크기} / {상태}
Button / Border / Primary / {크기} / {상태}
Button / Border / Secondary / {크기} / {상태}
Button / Border / Danger / {크기} / {상태}
Button / Text / Primary / {크기} / {상태}
Button / Text / Secondary / {크기} / {상태}
Button / Text / Danger / {크기} / {상태}
```

---

## Figma Make 프롬프트

```
다음 스펙으로 버튼(Button) 컴포넌트를 만들어줘:

스타일 대분류: Fill, Border, Text
각 스타일마다 Primary, Secondary, Danger 3단계
크기: XL (height 48px, 패딩 14px 20px, radius 8px), L (height 40px, 패딩 11px 16px, radius 8px), M (height 32px, 패딩 8px 12px, radius 8px), S (height 24px, 패딩 4px 8px, radius 6px)
Height에는 Size/Semantic Variables (size/XL, L, M, S) 바인딩
폰트: Pretendard SemiBold 600 (S는 Medium 500)

Fill/Primary: 배경 color/primary/default(#F26A00), 흰색 텍스트, 호버 color/primary/hover(#C75200)
Fill/Secondary: 배경 color/secondary/default, 텍스트 color/secondary/on-secondary, 호버 배경 color/secondary/hover
Fill/Danger: 배경 color/error/default(#E8321E), 흰색 텍스트, 호버 배경 darken
Border/Primary: 투명 배경, 오렌지 보더(1px solid color/primary/default), 오렌지 텍스트, 호버 배경 color/primary/subtle
Border/Secondary: 흰색 배경, 보더 1px solid color/border/default, 텍스트 color/text/primary, 호버 보더 color/border/strong
Border/Danger: 투명 배경, 보더 1px solid color/error/default, 레드 텍스트, 호버 배경 color/error/subtle
Text/Primary: 배경·보더 없음(fills:[], strokes:[], strokeWeight:0), 오렌지 텍스트, 호버 텍스트→primary/hover + 배경→primary/subtle
Text/Secondary: 배경·보더 없음, 텍스트 color/text/secondary, 호버 텍스트→text/primary + 배경→color/secondary/subtle
Text/Danger: 배경·보더 없음, 텍스트 color/error/default, 호버 텍스트→error/text + 배경→error/subtle

상태: Default, Hover, Active, Focus(3px 오렌지 링), Disabled(40% 불투명도), Loading(스피너)

Combine as Variants 적용.
네이밍: Button / {스타일} / {강조} / {크기} / {상태}
```
