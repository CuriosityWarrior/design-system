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

### Primary (주요)
- **배경**: `color/primary/default` (#F26A00 라이트 / #FF8A1E 다크)
- **텍스트**: `color/primary/on-primary` (#FFFFFF)
- **호버**: `color/primary/hover` (#C75200)
- **액티브**: `color/primary/active` (#9C3D00)
- **사용처**: 주요 CTA, 저장, 확인

### Secondary (보조)
- **배경**: `color/surface/1`
- **텍스트**: `color/text/primary`
- **보더**: 1px solid `color/border/default`
- **호버**: 보더 → `color/border/strong`, 배경 → `color/surface/2`
- **사용처**: 보조 액션, 취소

### Ghost
- **배경**: transparent
- **텍스트**: `color/primary/default`
- **보더**: 1px solid `color/primary/default`
- **호버**: 배경 → `color/primary/subtle`
- **사용처**: 인라인 액션, 경계선이 있는 보조 버튼

### Text (텍스트)

텍스트만으로 구성된 버튼. 배경도 보더도 없이 레이블 텍스트만 존재한다.
시각적으로 일반 텍스트처럼 보이지만 클릭 가능한 인터랙티브 요소이며, 호버 시 연한 배경이 나타나 버튼임을 인지시킨다.

| 속성 | Default | Hover | Focus | Disabled |
|---|---|---|---|---|
| 배경 (fills) | 없음 `[]` | `color/primary/subtle` (#FFF5ED) | 없음 `[]` | 없음 `[]` |
| 보더 (strokes) | 없음 `[]` | 없음 `[]` | 없음 `[]` | 없음 `[]` |
| 텍스트 색상 | `color/primary/default` | `color/primary/hover` (#C75200) | `color/primary/default` | `color/primary/default` |
| 포커스 링 | — | — | `shadow/focus` (3px 오렌지) | — |
| 불투명도 | 1 | 1 | 1 | 0.4 |

- **사용처**: 최소 강조 액션, 링크성 버튼, 인라인 텍스트 내 액션, "더 보기", "취소" 등
- **Figma 속성 요약**: `fills: []`, `strokes: []`, `strokeWeight: 0` — 배경·보더 모두 빈 배열

> ⚠️ **Ghost vs Text 차이점**
>
> | 구분 | Ghost | Text |
> |---|---|---|
> | 보더 | `1px solid color/primary/default` | **없음** |
> | 배경 (Default) | transparent | transparent |
> | 호버 배경 | `color/primary/subtle` | `color/primary/subtle` |
> | 호버 텍스트 | 그대로 | `color/primary/hover`로 변경 |
> | 시각적 인상 | 테두리가 있는 투명 버튼 | 텍스트만 있는 링크형 버튼 |
>
> Figma에서 Ghost를 클론하여 Text를 생성할 경우, 반드시 `strokes: []`, `strokeWeight: 0`으로 변경해야 한다.

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
| XS | `size/20` | 20px | `radius/XS` (4px) | `text/label-xs` (12px Medium) | 2px 6px |

> XS 사이즈는 Size Semantic 토큰 범위(최소 S=24px) 외의 값이므로 Primitive(`size/20`)를 직접 참조한다.

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

## Figma Make 프롬프트

```
다음 스펙으로 버튼(Button) 컴포넌트를 만들어줘:

변형: Primary, Secondary, Ghost, Text, Subtle, Danger
크기: XL (height 48px, 패딩 14px 20px, radius 8px), L (height 40px, 패딩 11px 16px, radius 8px), M (height 32px, 패딩 8px 12px, radius 8px), S (height 24px, 패딩 4px 8px, radius 6px), XS (height 20px, 패딩 2px 6px, radius 4px)
Height에는 Size/Semantic Variables (size/XL, L, M, S) 바인딩 (XS는 size/20 Primitive 직접)
폰트: Pretendard SemiBold 600 (XS, S는 Medium 500)

Primary: 배경 #F26A00, 흰색 텍스트, 호버 #C75200, 액티브 scale(0.97)
Secondary: 흰색 배경, 1px 회색 보더, 호버 시 보더 진해짐
Ghost: 투명 배경, 오렌지 보더(1px solid), 오렌지 텍스트, 호버 시 연한 오렌지 배경
Text: 투명 배경, 보더 완전히 없음(strokes:[], strokeWeight:0), 오렌지 텍스트, 호버 시 텍스트→primary/hover(#C75200) + 배경→primary/subtle(#FFF5ED). Ghost와의 핵심 차이: 보더 유무
Danger: 배경 #E8321E, 흰색 텍스트

상태: Default, Hover, Active, Focus(3px 오렌지 링), Disabled(40% 불투명도), Loading(스피너)

Combine as Variants 적용.
네이밍: Button / {변형} / {크기} / {상태}
```
