# 컴포넌트: 앱 바 (App Bar)

## 개요
페이지 상단에 고정되어 페이지 제목, 주요 액션, 네비게이션 진입점을 노출하는 바. Top App Bar는 페이지 헤더 역할을 한다.

---

## 디자인 토큰

| 토큰 | 값 |
|---|---|
| 배경 | `color/surface/1` |
| 보더 | 1px solid `color/border/subtle` (하단) |
| 그림자 (스크롤 시) | `shadow/appbar` = 0 2px 8px rgba(0,0,0,0.06) |
| 패딩 (좌우) | `spacing/16` (16px) |
| 제목 폰트 | `text/title-md` (17px / SemiBold 600) |
| 모션 | 200ms ease-out |

> 이 컴포넌트는 직각 형태로, Radius 토큰을 적용하지 않는다 (`radius/0`). 화면 가장자리에 고정되므로 보더 반경이 불필요하다.

---

## 변형 (Variant)

### Top App Bar (단일)
- Height: 56px
- 구조: [Leading Icon Button] [Title] [Trailing Icon Buttons × N]
- 제목 좌측 정렬, 한 줄 생략

---

### Size/Spacing 토큰 바인딩

| 속성 | 토큰 | 값 |
|---|---|---|
| Height | `size/XXL` | 56px |
| 좌우 패딩 | `spacing/16` | 16px |
| 제목–아이콘 간격 | `spacing/8` | 8px |
| Trailing 아이콘 간 간격 | `spacing/8` | 8px |

> Figma에서 해당 속성에 Variables를 직접 바인딩한다. 임의 px 고정값 사용 금지.

---

## 구성 요소

### Leading Area (좌측)
- Back 버튼 (`arrow_back` Icons 인스턴스) 또는 메뉴 버튼 (`menu` Icons 인스턴스)
- 또는 로고/브랜드

### Title Area
- 제목 텍스트 (1줄 생략)

### Trailing Area (우측)
- Icon Button 액션 N개 (최대 3개 권장)
- More 메뉴 (`more_vert` Icons 인스턴스) — 4개 이상 시 메뉴로 통합

---

## 상태 (State)

| 상태 | 배경 | 그림자 |
|---|---|---|
| 기본 (상단 고정) | `color/surface/1` | 없음 또는 1px 하단 보더 |
| 스크롤 (콘텐츠가 아래에 있을 때) | `color/surface/1` | `shadow/appbar` |

---

## 사이즈 동작

| 속성 | 값 |
|---|---|
| layoutSizingHorizontal | `FILL` |
| layoutSizingVertical | `FIXED` (56px) |

---

## 접근성
- 컨테이너: `role="banner"`
- 제목: `<h1>` 권장
- Back 버튼: `aria-label="뒤로 가기"`
- More 메뉴: `aria-label="더 보기"` + `aria-haspopup="menu"`
- 키보드: Leading → Title → Trailing 순 Tab

---

### Variants 구성
- 단일 변형 컴포넌트로, 개별 `COMPONENT` 노드로 유지한다. Component Set 적용 금지.

---

### 아이콘 사용 규칙
- Leading 영역의 뒤로 가기(`arrow_back`), 메뉴(`menu`) 아이콘과 Trailing 영역의 더보기(`more_vert`) 등 모든 아이콘은 `01 — Icons` 페이지에 정의된 아이콘 컴포넌트 인스턴스를 사용한다.
- 유니코드 문자, 특수 기호 텍스트(←, ☰, ⋮ 등)로 아이콘을 대체하는 것을 금지한다.
- 아이콘 크기: 24px

---

## 토큰 바인딩 체크리스트

본 컴포넌트의 Figma 구현 시 다음을 모두 충족해야 한다 ([`04-token-binding.md#토큰-바인딩-검증-의무`](../figma-design-system-guide/04-token-binding.md#토큰-바인딩-검증-의무) 참조).

| 속성 종류 | 바인딩 대상 | 검증 |
|---|---|---|
| Width / Height | `size/*` Variables (또는 부모 Auto Layout에 의해 결정) | `boundVariables.width` / `boundVariables.height` |
| Padding 4면 / itemSpacing | `spacing/*` Variables | `boundVariables.padding{Top|Right|Bottom|Left}` / `boundVariables.itemSpacing` |
| cornerRadius | `radius/*` Variables | `boundVariables.cornerRadius` (또는 4모서리별) |
| fills / strokes (SOLID 컬러) | `color/*` Variables | `boundVariables.fills` / `strokes` 또는 `fillStyleId` / `strokeStyleId` |
| 텍스트 노드 | Text Style (Pretendard) | `textStyleId !== ""` |
| 그림자 (effects) | Effect Style | `effectStyleId !== ""` |

위 "디자인 토큰" / "크기" 섹션에 명시된 값은 모두 위 토큰에 바인딩되어야 한다. 임의 px·HEX 값으로 남아있으면 위반이다.

**라이브러리에 없는 값**이 필요한 경우 [`04-token-binding.md#토큰-부재-시-신설-의무`](../figma-design-system-guide/04-token-binding.md#토큰-부재-시-신설-의무)에 따라 먼저 토큰을 신설한 후 바인딩한다.

---

## 사용 원칙

| 원칙 | 설명 |
|---|---|
| 단일 사이즈 | 56px 고정 높이 하나만 사용한다. 페이지별로 다른 높이를 사용하지 않는다. |
| 제목 필수 | 모든 페이지는 App Bar에 제목을 포함해야 한다. |
| 아이콘 최대 3개 | Trailing 영역 아이콘은 최대 3개. 초과 시 `more_vert`로 통합한다. |
| 스크롤 시 그림자 | 콘텐츠가 App Bar 아래로 스크롤되면 `shadow/appbar`를 적용한다. |

---

## Figma Make 프롬프트

```
다음 스펙으로 앱 바(App Bar) 컴포넌트를 만들어줘:

단일 변형 (단일 COMPONENT, Component Set 미사용):
- Height 56px (size/XXL 토큰 바인딩)
- 배경 color/surface/1
- 너비 Fill
- 좌우 패딩 16px (spacing/16)
- 좌측: arrow_back 또는 menu Icons 인스턴스
- 중앙: 제목 텍스트 (text/title-md, 좌측 정렬, 1줄 생략)
- 우측: Icon Button 최대 3개 (more_vert 포함)
- 스크롤 상태: 하단 1px 보더(color/border/subtle) 또는 shadow/appbar

모든 아이콘은 Icons 페이지 인스턴스 사용 (텍스트 기호 금지)

네이밍: App Bar
```
