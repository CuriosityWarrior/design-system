# 컴포넌트: 네비게이션 바 (Navigation Bar)

## 개요
앱의 최상위 목적지(탑레벨 destination) 사이를 전환하는 네비게이션. 모바일 하단 바(Bottom Navigation), 데스크톱 좌측 레일(Navigation Rail), 사이드 드로어(Navigation Drawer) 3종을 포함한다. Tabs와 달리 "페이지/섹션 전환"이며, App Bar와 함께 앱 셸을 구성한다.

---

## 디자인 토큰

| 토큰 | 값 |
|---|---|
| 배경 | `color/surface/1` |
| 보더 | 1px solid `color/border/subtle` (상/우측) |
| 활성 아이콘 | `color/primary/default` |
| 비활성 아이콘 | `color/text/tertiary` |
| 활성 레이블 | `color/primary/default` |
| 비활성 레이블 | `color/text/tertiary` |
| 활성 인디케이터 배경 | `color/primary/subtle` |
| 폰트 (레이블) | 11px / Medium 500 |
| 모션 | 150ms ease-out |

> 이 컴포넌트는 직각 형태로, Radius 토큰을 적용하지 않는다 (`radius/0`). 화면 가장자리에 붙는 하단 내비게이션 바이므로 보더 반경이 불필요하다.

---

## 변형 (Variant)

### Navigation Bar (모바일 하단)
- 화면 하단 고정. 3~5개 탑레벨 destination
- 각 아이템: 아이콘 + 짧은 레이블 (세로 배치)
- Height: 64px (safe area 별도)
- 활성 아이템: 아이콘 주변에 알약형 인디케이터 배경

### Navigation Rail (데스크톱 좌측)
- 화면 좌측 고정. 3~7개 destination
- Width: 80px
- 각 아이템: 아이콘 + (옵션) 레이블
- 상단: 옵션 FAB 또는 로고
- 하단: 프로필/설정

### Navigation Drawer (사이드 메뉴)
- 모달 또는 고정 형태
- Width: 280~360px
- 아이템: 아이콘 + 레이블 (가로 배치, 긴 이름 지원)
- 섹션 그룹화 + Divider
- 활성 아이템: 배경 강조 + 좌측 인디케이터 바

---

### Size/Spacing 토큰 바인딩

| 속성 | 토큰 | 값 |
|---|---|---|
| Navigation Bar 높이 | `size/3XL` | 64px |
| Navigation Rail 너비 | `size/80` | 80px |
| Navigation Drawer 너비 | 280~360px (레이아웃 고정 — 토큰 미적용) |
| 아이콘 크기 (Bar/Rail) | `size/S` | 24px |
| 아이콘 크기 (Drawer) | `size/20` | 20px |
| 아이템 내 아이콘–레이블 간격 | `spacing/4` | 4px |
| Drawer 아이템 패딩 좌우 | `spacing/16` | 16px |
| Drawer 아이템 패딩 상하 | `spacing/12` | 12px |

> Figma에서 해당 속성에 Variables를 직접 바인딩한다. 임의 px 고정값 사용 금지.

---

## 네비게이션 아이템 구성

### Bottom / Rail
- **Icon** (24px, Icons 페이지 인스턴스)
- **Label** (11px Medium)
- **Badge** (옵션): 우상단 작은 Badge 컴포넌트

### Drawer
- **Leading Icon** (20px)
- **Label** (14px Regular)
- **Trailing** (옵션): 숫자 Badge / Chevron

---

## 상태 (State)

| 상태 | 아이콘 | 레이블 | 배경(인디케이터) |
|---|---|---|---|
| 기본(비활성) | `color/text/tertiary` | `color/text/tertiary` | transparent |
| 호버 | `color/text/secondary` | `color/text/secondary` | `color/surface/2` |
| 활성(선택) | `color/primary/default` | `color/primary/default` | `color/primary/subtle` (알약형/보더) |
| 포커스 | — | — | `shadow/focus` |
| 비활성(disabled) | `color/text/tertiary` | `color/text/tertiary` | opacity 0.4 |

---

## 사이즈 동작

| 변형 | layoutSizingHorizontal | layoutSizingVertical |
|---|---|---|
| Navigation Bar (하단) | `FILL` (뷰포트 너비) | `FIXED` (64px + safe area) |
| Navigation Rail (좌측) | `FIXED` (80px) | `FILL` (뷰포트 높이) |
| Navigation Drawer | `FIXED` (280~360px) | `FILL` (뷰포트 높이) |

> 각 변형별로 고정 축과 채움 축이 명확히 다르다. 각 네비 아이템 자체는 HUG.

---

## 접근성
- 컨테이너: `role="navigation"` + `aria-label="주 네비게이션"`
- 각 아이템: `<a>` 또는 `role="link"`
- 활성 아이템: `aria-current="page"`
- 키보드: Tab 순차 이동
- 배지 숫자는 `aria-label`에 포함 ("알림, 3개 새로운 알림")

---

### Variants 구성
- 모든 변형은 Figma의 **Combine as Variants** 기능을 사용하여 하나의 Component Set으로 통합한다.

---

### 아이콘 사용 규칙
- 네비게이션 아이템의 모든 아이콘은 `01 — Icons` 페이지에 정의된 아이콘 컴포넌트 인스턴스를 사용한다.
- 유니코드 문자, 특수 기호 텍스트(🏠, ⚙ 등)로 아이콘을 대체하는 것을 금지한다.
- Bar/Rail 변형의 아이콘 크기는 `size/S` (24px), Drawer 변형은 `size/20` (20px)을 사용한다.

---

---

## 사용 원칙

| 원칙 | 설명 |
|---|---|
| 플랫폼에 맞는 변형 선택 | 모바일에는 Navigation Bar(하단), 데스크톱에는 Navigation Rail 또는 Navigation Drawer를 사용한다. 플랫폼 고유의 탐색 패턴을 따른다. |
| 탑레벨 목적지만 포함 | Navigation Bar에는 앱의 최상위 목적지(홈, 검색, 알림, 프로필 등)만 포함한다. 하위 페이지 이동에는 Tabs나 Breadcrumb를 사용한다. |
| 목적지 수 제한 준수 | Bottom Navigation은 3~5개, Rail은 3~7개 목적지를 기준으로 한다. 항목이 너무 많으면 Navigation Drawer로 전환을 검토한다. |
| 항상 고정 표시 | Navigation Bar는 스크롤에 관계없이 화면에 항상 고정된다. 일부 콘텐츠 화면에서만 숨기더라도 일관된 패턴을 유지한다. |
| Tabs와 혼용 금지 | 같은 화면에서 Navigation Bar와 Tabs를 같은 계층 전환 목적으로 동시에 사용하지 않는다. Navigation Bar는 앱 전역, Tabs는 페이지 내부에서만 사용한다. |

## Figma Make 프롬프트

```
다음 스펙으로 네비게이션 바(Navigation Bar) 컴포넌트를 만들어줘:

변형: Navigation Bar (모바일 하단), Navigation Rail (데스크톱 좌측), Navigation Drawer (사이드)

Navigation Bar:
- 높이 64px, 너비 Fill
- 상단 1px 보더, 흰색 배경
- 3~5개 아이템, 각각: 24px 아이콘 (Icons 페이지 인스턴스) + 11px Medium 레이블
- 활성 아이템: 아이콘 주변 알약형 오렌지 틴트 배경, 아이콘·레이블 오렌지 색상

Navigation Rail:
- 너비 80px, 높이 Fill, 우측 1px 보더
- 상단 옵션 FAB/로고, 하단 프로필
- 아이템 세로 배치

Navigation Drawer:
- 너비 280~360px, 높이 Fill, 우측 1px 보더
- 아이템 가로 배치 (20px 아이콘 + 14px 레이블)
- 섹션 구분 Divider
- 활성: 배경 강조 + 좌측 3px 오렌지 인디케이터 바

모든 아이콘은 Icons 페이지 인스턴스 사용 (텍스트 기호 금지)

네이밍: Navigation Bar / {Bar|Rail|Drawer}, Navigation Item / {상태}
```
