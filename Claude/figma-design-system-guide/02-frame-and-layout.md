# 프레임 및 배치 규칙

페이지 안에 무엇을 어디에 어떻게 배치할지 — 카드 프레임 스펙, 요소 간 간격, 변형 그리드 배치, 페이지 좌표.

## 프레임 구조 규칙

### 흰색 카드 프레임으로 감싸기

각 컴포넌트 페이지의 배경 카드 프레임은 해당 페이지에 포함된 모든 컴포넌트 및 관련 내용을 기준으로 상하좌우 100px 패딩을 적용하여 생성한다.

```
[ Figma Canvas — 회색 바닥 ]
└── {ComponentName} Frame (흰색 카드)
    ├── 제목 텍스트
    ├── 설명 텍스트
    ├── 컴포넌트들...
    └── ...
```

### 흰색 카드 프레임 스펙

| 항목 | 값 |
|---|---|
| 배경 | #FFFFFF |
| Border Radius | 16px |
| 내부 패딩 | 100px |
| 그림자 | Drop Shadow — rgba(26,25,22,0.08), y:4, blur:16 |
| 프레임 이름 | 컴포넌트 이름과 동일 (예: `Button`) |

### 카드 프레임 리사이즈 규칙

컴포넌트·베리어블을 추가·삭제·수정하여 카드 프레임 내 콘텐츠 영역이 변경된 경우, **카드 프레임의 크기를 콘텐츠에 맞춰 재지정한다.**

- 콘텐츠 추가 시: 추가된 요소를 포함하여 상하좌우 100px 패딩이 유지되도록 프레임을 확장한다.
- 콘텐츠 삭제 시: 남은 요소 기준으로 상하좌우 100px 패딩에 맞춰 프레임을 축소한다.
- 프레임 크기를 재지정하지 않고 기존 프레임 안에 요소를 계속 추가하는 것을 금지한다 — 공간 부족으로 요소가 겹치거나 프레임 밖으로 밀려나는 원인이 된다.

### 금지 사항
- 컴포넌트를 흰색 카드 프레임 없이 캔버스 바닥에 직접 배치하는 것 금지
- 카드 프레임 없이 텍스트 노드만 캔버스에 배치하는 것 금지

---

## 페이지 내 배치 간격 규칙

한 페이지 내에 여러 요소가 배치될 경우, 아래 간격을 준수한다.

| 배치 대상 | 간격 |
|---|---|
| Component Set 내 변형 간 | 20px ([변형 그리드 배치 규칙](#변형-그리드-배치-규칙)) |
| 카드 프레임 내 페이지 헤더 ↔ Component Set 간 | 100px (카드 프레임 패딩으로 보장) |
| 상위 그룹 간 (한 페이지에 여러 컴포넌트 그룹 존재 시) | 100px |

---

## 변형 그리드 배치 규칙

컴포넌트 페이지의 변형(variant)들은 카드 프레임 안에 단순한 그리드로 배치한다. **별도의 식별용 텍스트 라벨(메타 라벨)을 두지 않는다** — 변형은 시각적 차이와 Figma Variant Property 패널로 식별한다.

### 페이지 헤더 (모든 컴포넌트·파운데이션 페이지 공통)

페이지 정체성 표시를 위한 헤더만 유지한다.

| 위치 | 폰트 | 색상 |
|---|---|---|
| 페이지 타이틀 (예: "Avatar") | Inter **Bold 32** | `#000000` |
| 페이지 설명 (타이틀 아래 한 줄 설명) | Inter **Medium 15** | `#000000` |

### 메타 라벨 부재 정책

**`[ COMPONENTS ]` 섹션 이하 모든 페이지에서 변형 식별용 텍스트 라벨을 두지 않는다.**

- 그리드/스택 자체와 Variant Property 패널로 식별
- 예외 (이 정책에서 제외 — 라벨/텍스트 유지):
  - 페이지 헤더(타이틀·설명) — 위 표 참조
  - Foundations 페이지의 토큰 칩 라벨 (예: `color/primary/default`, `#F26A00`) — 토큰 자체의 설명
  - Change Log 페이지 entries — 버전 이력
- 카드 프레임 내부에 "Labels", "Spec", "Meta" 등 별도 프레임/그룹을 생성하지 않는다 ([01-page-structure.md#페이지-내-메타-박스-금지](01-page-structure.md#페이지-내-메타-박스-금지)).

### 변형 배치 규칙 (계층 기반)

컴포넌트의 변형 축을 **그룹 > 위계 > 상태 > 사이즈** 의미적 계층으로 정렬하고, 각 계층 간 간격을 다르게 적용한다.

| 계층 | 의미 | 대표 예시 | 변형 간 간격 |
|---|---|---|---|
| **그룹** | 의미적으로 분리되는 최상위 분류 (스타일 분류, 시멘틱 컬러 등) | Button의 `Fill / Border / Text`, Text Area/Select/Input의 `Border / Surface`, Badge/Progress Bar의 `Primary / Success / Error` | **100px** |
| **위계** | 강조 수준 또는 importance | Button의 `Primary / Secondary / Danger`, Icon Button의 `Primary / Secondary / Tertiary` | **50px** |
| **상태** | 인터랙션 상태 | `Default / Hover / Focus / Disabled / Selected / ...` | **20px** |
| **사이즈** | T-Shirt 사이즈 | `XL / L / M / S / XS` | **20px** |

### 축 수별 적용 패턴

| 축 수 | 대표 컴포넌트 | 계층 적용 | 배치 |
|---|---|---|---|
| **1축 (Size 또는 Variant)** | Avatar, Spinner, Chip, Label, Stat Card, Tooltip, Tabs, Alert, Toast, Skeleton, List Item, Data Case 등 | 사이즈/상태 20px | 가로 1행 또는 (wide variant ≤5는) 세로 1열 스택, 20px 간격 |
| **2축 (Size × State)** | Toggle, Checkbox, Radio | 사이즈/상태 20px | 행 = Size, 열 = State, 모두 20px 간격 |
| **2축 (Variant × Size, 그룹 분리)** | Badge, Progress Bar | Variant 그룹 100px / Size 20px | 행 = Variant (100px), 열 = Size (20px) |
| **3축 (Style × Size × State)** | Text Area, Select, Input | Style **그룹 100px** / Size·State 20px | 각 Style 블록(Size × State 2D 그리드)을 세로로 100px 간격 스택 |
| **3축 (Variant × Size × State, 위계 분리)** | Icon Button | Variant **위계 50px** / Size·State 20px | 각 Variant 블록을 세로로 50px 간격 스택 |
| **4축 (Style × Emphasis × Size × State)** | Button | Style **100** / Emphasis **50** / Size·State 20 | Style 블록을 100px 간격으로 세로 스택, 각 Style 블록 내에 Emphasis 블록을 50px 간격으로 스택, 각 Emphasis 블록은 Size × State 2D 그리드 |

### 그리드 셀 규칙

- **컬럼 너비**: Component Set 내 최대 변형 너비 (모든 셀 동일 너비, 변형은 left-top 정렬)
- **행 높이**: 해당 사이즈의 변형 높이 (사이즈마다 다른 행 높이 허용 — 사이즈 내림차순 정렬 권장)
- **그리드 외곽 padding 없음** (카드 프레임 100px 패딩만 적용 — [프레임 구조 규칙](#프레임-구조-규칙))
- **Component Set 위치**: 카드 내 `(100, 190)` — 페이지 헤더 아래 적정 거리

### 그룹/위계 블록 정렬 방향

- **기본: 세로 스택** (블록들이 위→아래로 쌓임, 같은 너비 유지)
- 가로 스택은 별도 검토 (예: 작은 시멘틱 변형이 많을 때 가로가 시각적으로 유리한 경우)

### 작은 변형 그룹의 간격 예외

- **변형 크기가 작아 100px 그룹 간격이 시각적으로 과한 경우**, 그룹 간격을 **50px**로 축소한다 (위계 수준으로 다운그레이드).
- 예: Badge — Primary/Success/Warning/Error/Info/Neutral 변형들이 모두 22×68px 이하의 작은 칩이라 100px 간격이 비대칭적으로 보임 → **Variant 간 50px**.
- 판단 기준: 변형 높이 < 50px 또는 변형 너비 < 100px 정도면 50px 권장.

### 한 페이지 다중 컴포넌트 정책

한 페이지에 **독립된 2개 이상의 컴포넌트가 존재**하는 경우 (예: `04 — Badge & Tag` 페이지의 Tag + Badge):

- 각 컴포넌트(Component / Component Set) 사이 간격 **100px** (그룹 수준)
- 컴포넌트는 세로로 스택 (단순한 것부터 → 복잡한 것 순서 권장)
- 모든 컴포넌트는 x=100 좌측 정렬 유지
- 카드 패딩은 전체 컴포넌트 그룹의 최외곽 기준 100px 유지

### 페이지 레이아웃 좌표 (전 페이지 공통)

| 요소 | 좌표 |
|---|---|
| 카드 프레임 | (0, 0), 패딩 100px 사방 |
| 페이지 타이틀 | (100, 100) — Inter Bold 32, #000 |
| 페이지 설명 | (100, 144) — Inter Medium 15, #000 |
| 첫 번째 Component Set / Component | (100, **헤더 bottom + 50px**) — 설명이 있으면 `description.y + description.height + 50`, 없으면 `title.y + title.height + 50` |
| 다중 컴포넌트의 다음 컴포넌트 | (100, 이전 컴포넌트 bottom + **100px**) |

- **모든 요소 좌측 x=100 정렬** (페이지 헤더와 컴포넌트들이 같은 선상)
- 카드 너비 = `100 + max(title.width, description.width, content.width) + 100`
- 카드 높이 = `마지막 컴포넌트.bottom + 100`

> 📌 **참고**: 페이지 설명 텍스트의 렌더링 높이가 변하면 첫 Component Set의 y 좌표도 함께 바뀐다 (보통 ~217 부근). 좌표를 절대값으로 고정하지 않고 헤더 bottom 기반으로 동적 계산할 것.

### 간격 조정 시 패딩 검증 의무

레이아웃 작업(변형 재배치, 헤더 위치 변경, 컴포넌트 추가/삭제 등) **직후 반드시 카드 패딩 4면 모두 100px인지 검증**한다.

| 항목 | 검증식 |
|---|---|
| 좌측 패딩 | `min(child.x for child in card.children) === 100` |
| 상단 패딩 | `min(child.y for child in card.children) === 100` |
| 우측 패딩 | `card.width − max(child.x + child.width for child in card.children) === 100` |
| 하단 패딩 | `card.height − max(child.y + child.height for child in card.children) === 100` |

- 패딩이 어긋난 경우 카드 프레임을 즉시 리사이즈한다 ([카드 프레임 리사이즈 규칙](#카드-프레임-리사이즈-규칙) 참조).
- 자동 검증 스크립트 작성 시 `page.loadAsync()`를 호출한 후 카드 자식을 읽어야 한다 (Figma dynamic-page 모드에서 stale 데이터 방지).

### 절대 좌표 배치

- Component Set의 **Auto Layout 사용 금지** (`layoutMode = NONE`)
- 변형들은 위 알고리즘으로 계산한 `(x, y)` **절대 좌표**로 Component Set 내에 배치한다.
- Component Set 크기는 변형 배치에 맞춰 결정 (외곽 padding 없음):
  - 그리드: `width = 5 × maxVariantWidth + 4 × 20`, `height = N × maxVariantHeight + (N-1) × 20`
  - 스택: `width = max(variant.width)`, `height = Σvariant.height + (N-1) × 20`
- 카드 프레임은 Component Set + 헤더 + 100px 패딩에 맞춰 자동 확장한다 ([프레임 구조 규칙](#프레임-구조-규칙)).

### 변형 추가/삭제 시

- 새 변형이 추가되면 위 규칙에 따라 위치 재계산 후 Component Set 크기를 재지정한다.
- 변형 삭제 시도 동일하게 남은 변형들을 재배열하고 빈 공간을 제거한다.
- 페이지 헤더와 Component Set 사이의 수직 간격은 카드 프레임 패딩(100px)으로 자동 보장된다.
