# 컴포넌트: 앱 바 (App Bar)

## 개요
페이지 상단(또는 하단)에 고정되어 페이지 제목, 주요 액션, 네비게이션 진입점을 노출하는 바. Top App Bar는 페이지 헤더 역할, Bottom App Bar는 모바일에서 주요 액션 묶음 역할.

---

## 디자인 토큰

| 토큰 | 값 |
|---|---|
| 배경 | `color/surface/1` |
| 보더 | 1px solid `color/border/subtle` (하단 또는 상단) |
| 그림자 (스크롤 시) | `shadow/appbar` = 0 2px 8px rgba(0,0,0,0.06) |
| 패딩 (좌우) | 16px |
| 제목 폰트 | 17px / SemiBold 600 (기본) → `text/title-md` |
| 배경 (Large 변형) | `color/surface/1` |
| 모션 | 200ms ease-out (스크롤 축소 전환) |

> 이 컴포넌트는 직각 형태로, Radius 토큰을 적용하지 않는다 (`radius/0`). 상단/하단 앱 바는 화면 가장자리에 고정되므로 보더 반경이 불필요하다.

---

## 변형 (Variant)

### Top App Bar — Small (기본)
- Height: 56px
- 구조: [Leading Icon Button] [Title] [Trailing Icon Buttons × N]
- 제목 좌측 정렬, 한 줄 생략

### Top App Bar — Center Aligned
- Height: 56px
- 제목 중앙 정렬 (보통 iOS 스타일)

### Top App Bar — Medium
- Height: 96px
- 상단 56px에 아이콘 액션, 하단 40px에 제목 (24px Bold)
- 스크롤 시 Small로 축소

### Top App Bar — Large
- Height: 136px
- 상단 56px + 하단 80px (28px Bold 제목)
- 스크롤 시 Small로 축소

### Bottom App Bar (모바일)
- Height: 64px
- 좌측: Icon Button 그룹 (2~4개)
- 우측: FAB 또는 Primary Button
- 하단 safe area 고려

---

### Size/Spacing 토큰 바인딩

| 속성 | 토큰 | 값 |
|---|---|---|
| Height — Small / Center Aligned | `size/XXL` | 56px |
| Height — Medium | `size/96` | 96px |
| Height — Large | `size/136` | 136px |
| Height — Bottom App Bar | `size/3XL` | 64px |
| 좌우 패딩 | `spacing/16` | 16px |
| 제목–아이콘 간격 | `spacing/8` | 8px |
| Trailing 아이콘 간 간격 | `spacing/8` | 8px |

> Figma에서 해당 속성에 Variables를 직접 바인딩한다. 임의 px 고정값 사용 금지.

---

## 구성 요소

### Leading Area (좌측)
- Back 버튼 (`arrow_back` Icons 인스턴스) 또는 메뉴 버튼 (`menu` Icons 인스턴스)
- 또는 로고/브랜드

### Title Area (중앙)
- 제목 텍스트 (1줄 생략)
- 옵션 부제목 (Small 변형은 제외)

### Trailing Area (우측)
- Icon Button 액션 N개 (최대 3개 권장)
- More 메뉴(`more_vert` Icons 인스턴스) — 4개 이상 시 메뉴로 통합
- 옵션 Avatar/프로필 버튼

---

## 상태 (State)

| 상태 | 배경 | 그림자 |
|---|---|---|
| 기본 (상단 고정) | `color/surface/1` | 없음 또는 1px 하단 보더 |
| 스크롤 (콘텐츠가 아래에 있을 때) | `color/surface/1` | `shadow/appbar` |
| 축소 (Medium/Large → Small 전환) | — | 200ms 전환 모션 |

---

## 사이즈 동작

| 변형 | layoutSizingHorizontal | layoutSizingVertical |
|---|---|---|
| Top App Bar — Small / Center | `FILL` | `FIXED` (56px + safe area) |
| Top App Bar — Medium | `FILL` | `FIXED` (96px + safe area) |
| Top App Bar — Large | `FILL` | `FIXED` (136px + safe area) |
| Bottom App Bar | `FILL` | `FIXED` (64px + safe area) |

> 각 변형별 Height는 고정(스크롤 시 전환 포함). 너비는 항상 Fill.

---

## 접근성
- 컨테이너: `role="banner"` (Top) / `role="contentinfo"` (Bottom)
- 제목: `<h1>` 권장
- Back 버튼: `aria-label="뒤로 가기"`
- More 메뉴: `aria-label="더 보기"` + `aria-haspopup="menu"`
- 키보드: Leading → Title → Trailing 순 Tab

---

## Figma Make 프롬프트

```
다음 스펙으로 앱 바(App Bar) 컴포넌트를 만들어줘:

변형: Top App Bar — Small, Center Aligned, Medium, Large, Bottom App Bar

공통:
- 배경 흰색 (color/surface/1)
- 너비 Fill
- 좌우 패딩 16px
- 좌측 Icon Button, 중앙 제목, 우측 Icon Button 그룹
- 모든 아이콘은 Icons 페이지 인스턴스 사용 (arrow_back, menu, more_vert 등, 텍스트 기호 금지)

Top App Bar — Small:
- Height 56px
- 제목 17px SemiBold, 좌측 정렬

Center Aligned:
- Height 56px, 제목 중앙 정렬

Medium:
- Height 96px, 상단 56px 액션 영역 + 하단 40px 제목 영역 (24px Bold)

Large:
- Height 136px, 상단 56px + 하단 80px 제목 영역 (28px Bold)

Bottom App Bar:
- Height 64px
- 좌측 Icon Button 그룹, 우측 FAB 인스턴스

스크롤 상태: 하단 1px 보더 또는 shadow/appbar 그림자

네이밍: App Bar / {Top Small|Top Center|Top Medium|Top Large|Bottom} / {상태}
```
