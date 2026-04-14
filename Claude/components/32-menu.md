# 컴포넌트: 메뉴 (Menu)

## 개요
트리거 요소를 클릭/호버할 때 나타나는 액션 또는 옵션 목록. Select(값 선택)와 달리 "수행할 액션"의 모음에 사용. 컨텍스트 메뉴, 더보기(`more_horiz` 아이콘 인스턴스, `01 — Icons`) 메뉴, 드롭다운 액션 메뉴 모두 포함.

---

## 디자인 토큰

| 토큰 | 값 |
|---|---|
| 배경 | `color/surface/1` |
| 보더 | 1px solid `color/border/default` |
| 보더 반경 | `radius/dropdown` = 10px |
| 그림자 | `shadow/dropdown` |
| 패딩 (컨테이너) | 4px |
| 폰트 | 13px / Regular 400 → `text/body-sm` |
| 아이템 패딩 | 8px 12px |
| 아이템 보더 반경 | 6px |
| 아이템 간격 | 2px |
| 트리거와의 간격 | 4px |
| 모션 | `motion/scale` = 150ms ease-out |

---

### Size/Spacing 토큰 바인딩

| 속성 | 토큰 | 값 |
|---|---|---|
| 컨테이너 패딩 | `spacing/4` | 4px |
| 아이템 패딩 상하 | `spacing/8` | 8px |
| 아이템 패딩 좌우 | `spacing/12` | 12px |
| 아이템 간격 | `spacing/2` | 2px |
| 아이템 보더 반경 | `spacing/6` | 6px |
| 트리거와의 간격 | `spacing/4` | 4px |
| Leading Icon 크기 | `size/XS` | 16px |
| 최소 너비 | 160px (레이아웃 고정 — 토큰 미적용) |
| 최대 너비 | 320px (레이아웃 고정 — 토큰 미적용) |

> Figma에서 해당 속성에 Variables를 직접 바인딩한다. 임의 px 고정값 사용 금지.

---

## 구조

```
Menu (컨테이너)
├── Menu Item (기본)
│   ├── (옵션) Leading Icon
│   ├── Label
│   └── (옵션) Trailing Shortcut / Chevron / Badge
├── Menu Item (destructive)
├── Divider (Subtle)
└── Menu Item ...
```

---

## 변형 (Variant)

### Dropdown Menu
- 버튼/Icon Button 트리거에서 열리는 액션 리스트
- 예: 더보기(`more_horiz` 아이콘 인스턴스, `01 — Icons`) 메뉴, 정렬 메뉴

### Context Menu
- 우클릭 시 표시. 커서 위치에 나타남
- 동일한 Menu Item 구조 재사용

### Sub Menu
- Menu Item 우측 끝에 `chevron_right` 아이콘(인스턴스) → 호버 시 하위 Menu 펼침

---

## 메뉴 아이템 구성
- **Leading Icon** (옵션): `01 — Icons` 인스턴스, 16px, `color/text/secondary`
- **Label**: 13px / Regular, `color/text/primary`
- **Trailing**: 다음 중 하나
  - Shortcut: `⌘K` 스타일 Label (`color/text/tertiary`)
  - Chevron: 서브메뉴 존재 시
  - Check: 선택된 상태(라디오형 그룹)

---

## 상태 (State)

| 상태 | 배경 | 텍스트 |
|---|---|---|
| 기본 | transparent | `color/text/primary` |
| 호버 / 포커스 | `color/surface/2` | `color/text/primary` |
| 활성(선택) | `color/primary/subtle` | `color/primary/default` |
| 비활성 | transparent | `color/text/tertiary`, 커서 not-allowed |
| Destructive 기본 | transparent | `color/error/default` |
| Destructive 호버 | `color/error/tint` | `color/error/text` |

---

## 사이즈 동작

| 속성 | 값 |
|---|---|
| layoutSizingHorizontal | `HUG` (min-width 160px, max-width 320px) |
| layoutSizingVertical | `HUG` |

> 메뉴 컨테이너와 각 아이템 모두 콘텐츠 + 패딩 기준으로 자동 조정된다. 임의 px 값으로 Fixed 지정 금지.

---

## 접근성
- 컨테이너: `role="menu"`
- 각 아이템: `role="menuitem"`
- 키보드: ↑↓로 이동, Enter 선택, Esc 닫기
- 포커스 트랩: 메뉴 열려있는 동안 내부에 유지
- 트리거: `aria-haspopup="menu"`, `aria-expanded` 동기화

---

### Variants 구성
- 모든 변형은 Figma의 **Combine as Variants** 기능을 사용하여 하나의 Component Set으로 통합한다.

---

### 아이콘 사용 규칙
- Leading Icon, 트리거 아이콘(`more_horiz`, `more_vert`), 서브메뉴 쉐브론(`chevron_right`) 등 모든 아이콘은 `01 — Icons` 페이지에 정의된 아이콘 컴포넌트 인스턴스를 사용한다.
- 유니코드 문자, 특수 기호 텍스트(▶, ⋮ 등)로 아이콘을 대체하는 것을 금지한다.
- Leading Icon 크기는 `size/XS` (16px)를 사용한다.

---

## Figma Make 프롬프트

```
다음 스펙으로 메뉴(Menu) 컴포넌트를 만들어줘:

변형: Dropdown Menu, Context Menu, Sub Menu

컨테이너:
- 배경: 흰색, 보더 1px, 보더 반경 10px
- 패딩: 4px, 그림자: shadow/dropdown
- min-width 160px

메뉴 아이템:
- 폰트: 13px Regular
- 패딩: 8px 12px, 보더 반경 6px
- 좌측(옵션): Leading Icon (Icons 페이지 인스턴스, 16px)
- 중앙: Label
- 우측(옵션): Shortcut Label 또는 chevron_right 아이콘 (Icons 페이지 인스턴스)
- 호버: 연한 회색 배경
- Destructive 변형: 빨간 텍스트, 호버 시 빨간 틴트 배경

Divider: 아이템 그룹 사이 1px 구분선 (Divider Subtle 인스턴스)

네이밍: Menu / Container, Menu Item / {Default|Destructive} / {상태}
```
