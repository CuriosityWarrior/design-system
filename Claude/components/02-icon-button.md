# 컴포넌트: 아이콘 버튼 (Icon Button)

## 개요
아이콘만 포함하는 정사각형 버튼. 텍스트 레이블이 불필요한 간결한 액션 트리거에 사용.

---

## 디자인 토큰

| 토큰 | 값 |
|---|---|
| 보더 반경 | `radius/button` = 8px |
| 포커스 링 | `shadow/focus` = 0 0 0 3px rgba(242,106,0,0.20) |
| 호버 모션 | 100ms cubic-bezier(0, 0, 0.2, 1) |
| 프레스 모션 | 50ms cubic-bezier(0.4, 0, 0.2, 1) |

---

## 크기 (Size)

> 📐 Width와 Height 모두 [파운데이션: 사이즈](../foundations/07-size.md)의 Semantic 토큰을 참조한다 (정사각형).

| 항목 | 값 |
|---|---|
| layoutSizingHorizontal | `HUG` |
| layoutSizingVertical | `HUG` |

> 가로·세로 모두 Hug Contents로 설정하여 아이콘 및 패딩에 맞게 자동 조정한다.

| 크기 | Size 토큰 | 가로 × 세로 | 아이콘 크기 |
|---|---|---|---|
| XLarge (xl) | `size/icon-button/xl` → `size/xl` | 48 × 48px | 24px |
| Large (lg) | `size/icon-button/lg` → `size/lg` | 40 × 40px | 20px |
| Medium (md) | `size/icon-button/md` → `size/md` | 32 × 32px | 16px |
| Small (sm) | `size/icon-button/sm` → `size/sm` | 24 × 24px | 14px |

---

## 변형 (Variant)

### Primary
- **배경**: `color/primary/default`
- **아이콘 색상**: `color/primary/on-primary`
- **호버**: `color/primary/hover`

### Secondary
- **배경**: `color/surface/1`
- **아이콘 색상**: `color/text/primary`
- **보더**: 1px solid `color/border/default`
- **호버**: 보더 → `color/border/strong`

### Ghost
- **배경**: transparent
- **아이콘 색상**: `color/text/secondary`
- **호버**: 배경 → `color/surface/2`, 아이콘 → `color/text/primary`

---

## 상태 (State)

| 상태 | 설명 |
|---|---|
| Default | 기본 상태 |
| Hover | 배경/보더 변화 — 100ms ease-out |
| Active | scale(0.94) — 50ms ease-in-out |
| Focus | `shadow/focus` 링 |
| Disabled | opacity 0.4, 커서 not-allowed |

---

## 접근성
- 액션을 설명하는 `aria-label` 항상 필요 (예: `aria-label="편집"`)
- 호버 시 툴팁으로 액션 레이블 표시
- 최소 터치 영역: 44px (xl 사이즈 충족, lg 이하는 터치 타깃 확보 필요)

---

## Figma Make 프롬프트

```
다음 스펙으로 아이콘 버튼(Icon Button) 컴포넌트를 만들어줘:

크기: XLarge (48×48px, 아이콘 24px), Large (40×40px, 아이콘 20px), Medium (32×32px, 아이콘 16px), Small (24×24px, 아이콘 14px)
Width/Height에는 Size/Semantic Variables (size/icon-button/xl, lg, md, sm)를 바인딩
변형: Primary, Secondary, Ghost
보더 반경: 8px

Primary: 오렌지 배경 (#F26A00), 흰색 아이콘
Secondary: 흰색 배경, 1px 회색 보더, 어두운 아이콘
Ghost: 투명 배경, 회색 아이콘, 호버 시 연한 배경

상태: 기본, 호버, 액티브(scale 0.94), 포커스(3px 오렌지 링), 비활성(40% 불투명도)

아이콘은 반드시 `01 — Icons` 페이지의 아이콘 컴포넌트 인스턴스를 사용한다 (텍스트 기호·이모지·직접 그린 벡터 금지).
아이콘이 가운데 정렬된 정사각형 Auto Layout 사용.
네이밍: Icon Button / {변형} / {크기} / {상태}
```
