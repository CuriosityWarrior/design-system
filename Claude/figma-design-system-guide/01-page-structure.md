# 페이지 구조 및 네이밍

페이지를 어떻게 명명하고 어떤 페이지를 둘지, 그리고 페이지 내에 어떤 콘텐츠를 두지 않을지에 대한 규칙.

## 페이지 네이밍 규칙

### 섹션 구분자
- 대괄호 `[ ]` 로 섹션 이름을 감싼다.
- 섹션 이름은 **모두 대문자(UPPERCASE)** 로 작성한다.
- 섹션 구분자 페이지는 실제 작업 내용을 포함하지 않는다.

```
[ FOUNDATIONS ]
[ COMPONENTS ]
```

### 컴포넌트 / 파운데이션 페이지
- `{두 자리 번호} — {이름}` 형식으로 작성한다.
- 번호는 `01`부터 시작하는 두 자리 숫자로 패딩한다.
- 구분자는 **em dash(`—`)** 를 사용한다. (하이픈 `-` 사용 금지)
- 이름은 영문 Title Case로 작성한다.

```
01 — Color
02 — Typography
01 — Icons
02 — Button
```

### 특수 페이지
- `Cover`, `Change Log` 는 번호 없이 이름만 작성한다.
- 섹션 구분자 없이 파일 최상단에 위치한다.

## Change Log 페이지 콘텐츠 양식

Figma `Change Log` 페이지의 카드 프레임 내부는 다음 2개 영역으로 구성한다.

```
[ Change Log 카드 프레임 (흰색, r16, 100px 패딩) ]
├── Header
│   ├── 타이틀 텍스트 ("Change Log") — text/heading-XL
│   └── 설명 텍스트 — text/body-SM
└── Entries (수직 Auto Layout, item spacing 24px)
    └── 각 entry 프레임 (이름: vX.Y 또는 vX.Y.Z)
        ├── meta (가로 80px 고정)
        │   ├── 버전 (vX.Y / vX.Y.Z) — text/label-SM
        │   └── 날짜 (YYYY.MM.DD) — text/label-XS, color/text/secondary
        └── 본문 텍스트 (1줄, 마침표로 종결) — text/body-SM
```

**작성 규칙**:
- 새 항목은 Entries 프레임의 **하단에 append**한다 — Entries Auto Layout 바깥(카드 프레임 자식 등)에 단독 텍스트 노드로 배치 금지.
- 본문은 한 줄로 작성하되, 길어질 경우 폭(1000px)이 자동 wrap 처리하도록 한다. 별도 줄바꿈 강제 금지.
- 본문은 **마침표(`.`)로 종결**한다 — [CHANGELOG.md](CHANGELOG.md)와 동일.
- 버전과 날짜 형식은 [CHANGELOG.md](CHANGELOG.md)와 1:1 동일하게 기록한다.
- v2.1 이후 누락분 또는 양식 깬 단일 텍스트 노드 발견 시, 즉시 Entries Auto Layout 내부 entry 프레임으로 정규화한다.
- **정책·노트 박스 금지** ([페이지 내 메타 박스 금지](#페이지-내-메타-박스-금지) 참조) — Change Log 동기화 정책 등 메타 텍스트는 md에만 기록한다.

## Cover 페이지 콘텐츠 양식

> _※ Cover 페이지의 콘텐츠는 디자이너 작업 후 본 가이드에 반영한다._

## 페이지 내 메타 박스 금지

디자인 시스템 페이지 내부(카드 프레임 또는 캔버스 상)에 아래 유형의 텍스트·프레임을 두지 않는다. 이러한 메타 정보는 모두 md 문서에서만 관리하고, Figma 파일은 시각 데모와 토큰 바인딩에만 집중한다.

| 금지 유형 | 예시 | 정보가 있어야 할 곳 |
|---|---|---|
| **정책·노트 박스** | "정책: 이 페이지는 md와 동기화됩니다…" | 본 가이드 폴더 (`figma-design-system-guide/`) |
| **버전 콜아웃** | "📝 v1.6 — Border/Surface 2가지 스타일…" | [CHANGELOG.md](CHANGELOG.md) + Figma `Change Log` 페이지 |
| **컴포넌트 스펙 요약 박스** | "Component Name / Variant: A/B/C / Size: L/M/S / State: …" | `../design-system/components/{NN}-{name}.md` |
| **페이지 메타 인덱스** | 카테고리 명만 나열한 텍스트 목록 (예: Icons 페이지의 영문 카테고리 목록) | 페이지 헤더 설명 또는 md |

**변형 그리드 메타 라벨과의 차이**:
- [02-frame-and-layout.md#메타-라벨-부재-정책](02-frame-and-layout.md#메타-라벨-부재-정책)의 메타 라벨은 **개별 컴포넌트·베리어블 옆에 붙는 변형 식별 라벨**(예: "Primary", "LG / Default") — v2.11에서 폐지됨.
- 본 절의 금지 대상은 **페이지 단위로 한 번에 모아 놓는 메타 박스/요약/노트** — REMOVE.

페이지 내 메타 박스가 발견되면 즉시 제거하고, 해당 정보가 md에 누락되어 있으면 md에 추가한다.

## 전체 페이지 구조

```
Cover
Change Log

[ FOUNDATIONS ]
01 — Color
02 — Typography
03 — Spacing
04 — Shadow
05 — Radius
06 — Motion
07 — Size

[ COMPONENTS ]
01 — Icons
02 — Button
03 — Icon Button
04 — Badge & Tag
05 — Avatar
06 — Spinner
07 — Divider
08 — Tooltip
09 — Input
10 — Text Area
11 — Select
12 — Checkbox
13 — Radio
14 — Toggle
15 — Alert
16 — Toast
17 — Progress Bar
18 — Skeleton
19 — Data Case
20 — Card
21 — Modal
22 — Drawer
23 — Tabs
24 — Breadcrumb
25 — Pagination
26 — Table
27 — List Item
28 — Stat Card
29 — Chip
30 — Label
31 — Search
32 — Menu
33 — Date & Time Picker
34 — Slider
35 — FAB
36 — Navigation Bar
37 — App Bar
38 — Bottom Sheet
```
