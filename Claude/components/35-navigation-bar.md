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
