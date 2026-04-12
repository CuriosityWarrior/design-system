# 컴포넌트: 플로팅 액션 버튼 (FAB)

## 개요
화면의 주요 액션을 즉시 수행할 수 있도록 떠 있는 원형/둥근 사각형 버튼. 페이지의 주요 CTA를 고정된 위치에 노출한다. 일반 Button/Icon Button과 달리 엘리베이션(그림자)과 플로팅 위치를 특징으로 한다.

---

## 디자인 토큰

| 토큰 | 값 |
|---|---|
| 배경 | `color/primary/default` |
| 아이콘 색상 | `color/primary/on-primary` |
| 보더 반경 | `radius/fab` = 16px (기본) / 9999px (원형 변형) |
| 그림자 | `shadow/fab` = 0 6px 16px rgba(0,0,0,0.16) |
| 호버 그림자 | 0 8px 20px rgba(0,0,0,0.20) |
| 포커스 링 | `shadow/focus` |
| 호버 모션 | 150ms ease-out |
| 프레스 모션 | 50ms ease-in-out (scale 0.96) |

---

## 크기 (Size)

> 📐 Width/Height는 [파운데이션: 사이즈](../foundations/07-size.md)의 Semantic 토큰을 참조한다.

| 크기 | Size 토큰 | 가로 × 세로 | 아이콘 크기 |
|---|---|---|---|
| Large (lg) | `size/fab/lg` → `size/2xl` | 56 × 56px | 24px |
| Medium (md) | `size/fab/md` → `size/xl` | 48 × 48px | 24px |
| Small (sm) | `size/fab/sm` → `size/lg` | 40 × 40px | 20px |

---

## 변형 (Variant)

### FAB (기본)
- 아이콘만 포함한 정사각형(둥근 모서리) 버튼
- 아이콘은 `01 — Icons` 페이지 인스턴스

### Extended FAB
- 아이콘 + 텍스트 레이블을 한 행에 배치
- Height: 48px, 패딩 16px 20px, 레이블 14px Medium
- Width: HUG

### Surface FAB
- 배경 `color/surface/1`, 아이콘 `color/primary/default`
- 보더 1px `color/border/default`
- 덜 강조되는 보조 주요 액션

---

## 상태 (State)

| 상태 | 배경 | 그림자 |
|---|---|---|
| 기본 | `color/primary/default` | `shadow/fab` |
| 호버 | `color/primary/hover` | 확대된 그림자 |
| Active / Pressed | `color/primary/active` | `shadow/fab`, scale(0.96) |
| 포커스 | `color/primary/default` | `shadow/focus` |
| 비활성 | opacity 0.4 | 그림자 없음 |

---

## 위치 및 간격
- 화면 우하단 기본 (16~24px 여백)
- 모바일 하단 탭바와 겹치지 않도록 상단 추가 여백(16px)
- 페이지 중앙 하단도 가능 (예: 지도 확대/현재 위치)

---

## 사이즈 동작

| 변형 | layoutSizingHorizontal | layoutSizingVertical |
|---|---|---|
| FAB (기본) | `FIXED` | `FIXED` |
| Extended FAB | `HUG` | `FIXED` (48px) |

> 기본 FAB는 Size 토큰(`size/fab/*`)만으로 크기를 지정. Extended FAB는 가로만 콘텐츠 HUG.

---

## 접근성
- 아이콘 전용 FAB는 `aria-label` 필수 (예: `aria-label="글쓰기"`)
- 포커스 링 항상 표시
- 최소 터치 영역: 44px 이상 (sm 변형은 모바일에서 지양)
- 화면 가장자리 여백 확보하여 시스템 UI와 충돌 방지

---

## Figma Make 프롬프트

```
다음 스펙으로 플로팅 액션 버튼(FAB) 컴포넌트를 만들어줘:

변형: FAB (기본), Extended FAB, Surface FAB
크기: Large (56px), Medium (48px), Small (40px)
Width/Height에는 Size/Semantic Variables (size/fab/lg, md, sm) 바인딩

기본 FAB:
- 오렌지 배경 (#F26A00), 흰색 아이콘
- 보더 반경 16px
- 그림자: 0 6px 16px rgba(0,0,0,0.16)
- 아이콘은 Icons 페이지 인스턴스 사용 (텍스트 기호 금지)

Extended FAB:
- 아이콘 + 텍스트 레이블 (14px Medium)
- 패딩 16px 20px
- Height 48px, Width HUG

Surface FAB:
- 흰색 배경, 1px 보더, 오렌지 아이콘

상태: 기본, 호버(그림자 확대), 액티브(scale 0.96), 포커스(3px 오렌지 링), 비활성(40% 불투명도)

네이밍: FAB / {FAB|Extended|Surface} / {크기} / {상태}
```
