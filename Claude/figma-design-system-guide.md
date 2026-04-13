# Figma Design System 생성 규칙

## 개요

디자인 시스템을 Figma에서 생성할 때 따라야 하는 전체 규칙 문서.
페이지 네이밍, 프레임 구조, 컴포넌트 작성 기준을 포함한다.

### AI 네이티브 디자인 시스템의 4계층 구조

본 디자인 시스템은 사람뿐만 아니라 AI도 이해하고 활용할 수 있도록 아래 4계층 구조를 따른다.

| 계층 | 역할 | 예시 |
|---|---|---|
| **디자인 레이어** | Figma 컴포넌트 및 레이아웃 | 컴포넌트 배치, Auto Layout, 프레임 구조 |
| **토큰 레이어** | 시각적 속성 정의 | color.primary.500, spacing.16, radius.M |
| **논리 레이어** | 컴포넌트 속성 및 상호작용 규칙 | Variant 속성, 상태 전환, 반응형 동작 |
| **지식 레이어** | 문서화 및 제약 조건 | 사용 규칙, 접근성 기준, 컴포넌트 설명 |

이 구조가 갖춰지면 AI는 기존 컴포넌트를 활용한 UI 레이아웃 생성, 프로덕션 레디 코드 변환, 적절한 컴포넌트 추천, 디자인 의도와 제약 이해가 가능해진다.

---

## 1. 페이지 네이밍 규칙

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
- `Cover`, `Changelog` 는 번호 없이 이름만 작성한다.
- 섹션 구분자 없이 파일 최상단에 위치한다.

### 컴포넌트 Variants 네이밍
- Figma 컴포넌트의 Variants 네이밍은 `{이름}/{변형}/{크기}/{상태}` 형식을 따른다.
- 각 축은 슬래시(`/`)로 구분하고, 축이 불필요한 경우 생략할 수 있다.
- 약어를 지양하고, 일관된 구분자(`/`)를 사용하며, 예측 가능한 패턴을 유지한다.
- 예:
  - `Button / Primary / lg / Default`
  - `Icon Button / Ghost / md / Hover`
  - `Badge / Success / sm`
  - `Divider / Horizontal / Default`

### 전체 페이지 구조

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

---

## 2. 프레임 구조 규칙

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

#### 흰색 카드 프레임 스펙

| 항목 | 값 |
|---|---|
| 배경 | #FFFFFF |
| Border Radius | 16px |
| 내부 패딩 | 100px |
| 그림자 | Drop Shadow — rgba(26,25,22,0.08), y:4, blur:16 |
| 프레임 이름 | 컴포넌트 이름과 동일 (예: `Button`) |

#### 카드 프레임 리사이징 규칙

컴포넌트나 변수(Variable)를 추가·수정·삭제할 때, **반드시 카드 프레임의 크기를 재조정**한다.

- 카드 프레임 내부의 모든 자식 노드를 기준으로 상하좌우 100px 패딩이 유지되도록 프레임 크기를 재계산한다.
- 카드 프레임 크기를 재조정하지 않으면, 새로 추가된 컴포넌트가 프레임 경계 밖에 쌓이는 현상이 발생한다.
- 컴포넌트 추가/삭제 작업 후 카드 프레임 리사이징을 마지막 단계로 반드시 수행한다.

#### 금지 사항
- 컴포넌트를 흰색 카드 프레임 없이 캔버스 바닥에 직접 배치하는 것 금지
- 카드 프레임 없이 텍스트 노드만 캔버스에 배치하는 것 금지
- 카드 프레임 크기를 재조정하지 않고 컴포넌트를 추가하는 것 금지

---

## 3. Auto Layout 규칙

**모든 컴포넌트와 레이아웃 프레임에는 Auto Layout을 적용한다.**

Auto Layout을 통해 요소의 동작 방식(패딩, 간격, 정렬, 반응형 동작)을 명확히 정의하면, AI가 정적 형태 대신 구조와 동작을 인식할 수 있다.

- 컴포넌트 내부 구조는 반드시 Auto Layout으로 구성한다.
- 패딩과 간격은 `spacing/*` 토큰을 바인딩한다 (§9 참조).
- 정렬(Alignment), 방향(Direction), 배분(Distribution) 속성을 명시적으로 설정한다.
- `layoutSizingHorizontal` / `layoutSizingVertical` 값(HUG / FILL / FIXED)은 각 컴포넌트 md 파일에서 정의한다.
- 반응형 동작이 필요한 경우 Fill Container, Min/Max Width 등을 활용하여 정의한다.

#### 금지 사항
- Auto Layout 없이 절대 좌표(Absolute Position)만으로 컴포넌트를 구성하는 것 금지.
- Auto Layout 프레임 내에서 임의 px 값으로 패딩/간격을 하드코딩하는 것 금지 (토큰 바인딩 필수).

---

## 4. 컴포넌트 Sizing 규칙

컴포넌트의 `layoutSizingHorizontal` / `layoutSizingVertical` 값(HUG / FILL / FIXED)은 **각 컴포넌트 md 파일에서 개별로 정의**한다.
공통 규칙으로 일괄 강제하지 않는다.

- 각 컴포넌트 문서의 "크기 (Size)" 또는 "사이즈 동작" 섹션에서 해당 컴포넌트의 sizing 방식을 명시한다.
- 문서에 명시되지 않은 채 임의 값(예: `100px`)으로 Height를 Fixed 지정하는 것을 금지한다.

---

## 5. 의미 있는 레이어 네이밍 규칙

**Figma 내 모든 레이어(프레임, 그룹, 노드)에는 역할을 나타내는 의미 있는 이름을 부여한다.**

- `Frame 1`, `Rectangle 23`, `Group 5` 같은 자동 생성 이름을 그대로 사용하는 것을 금지한다.
- 레이어 이름은 해당 요소의 역할을 명확히 표현해야 한다.

| 금지 (자동 생성 이름) | 권장 (의미 기반 이름) |
|---|---|
| `Rectangle 23` | `Button Container` |
| `Text 1` | `Button Label` |
| `Frame 12` | `Input Field` |
| `Group 3` | `Card Header` |
| `Vector 5` | `Close Icon` |

- 네이밍은 영문 Title Case로 작성한다.
- 컴포넌트 내부 레이어도 동일 규칙을 적용한다.

---

## 6. 컴포넌트 설명(Description) 문서화 규칙

**모든 컴포넌트에는 Figma의 Component Description 필드에 설명을 작성한다.**

컴포넌트 설명은 AI가 해당 컴포넌트의 목적과 사용 맥락을 이해하는 지식 레이어 역할을 한다.

### 필수 포함 항목
- **목적**: 이 컴포넌트가 무엇을 위한 것인지 한 줄 요약.
- **사용 규칙**: 사용 시 지켜야 할 제약 조건 (예: "Primary 버튼은 화면당 한 번만 사용").
- **접근성 기준**: 최소 터치 영역(44px), 색상 대비 등 접근성 관련 수치 기준.

### 작성 예시
```
Primary 버튼 — 주요 행동 유도(CTA)에 사용. 화면당 하나만 배치.
최소 터치 영역 44×44px. color.button.primary.background 토큰 사용.
```

- 설명은 국문으로 작성한다 (§8 문서 작성 언어 규칙 참조).
- 토큰명, 속성명 등 고유 명칭은 영문 그대로 사용한다.

---

## 7. Figma MCP로 일괄 적용하는 방법

위 규칙들은 Figma MCP(`use_figma`)를 통해 자동화할 수 있다.

### 흰색 카드 프레임 적용 스크립트 (페이지 단위)

```javascript
const page = figma.currentPage;
const children = [...page.children];
let minX = Infinity, minY = Infinity, maxX = -Infinity, maxY = -Infinity;

children.forEach(n => {
  minX = Math.min(minX, n.x);
  minY = Math.min(minY, n.y);
  maxX = Math.max(maxX, n.x + n.width);
  maxY = Math.max(maxY, n.y + n.height);
});

const padding = 100;
const cardFrame = figma.createFrame();
cardFrame.name = page.name.replace(/^\d+ — /, ''); // 번호 제거한 이름
cardFrame.x = 0;
cardFrame.y = 0;
cardFrame.resize(
  (maxX - minX) + padding * 2,
  (maxY - minY) + padding * 2
);
cardFrame.fills = [{ type: 'SOLID', color: { r: 1, g: 1, b: 1 } }];
cardFrame.cornerRadius = 16;
cardFrame.effects = [{
  type: 'DROP_SHADOW',
  color: { r: 0.1, g: 0.1, b: 0.086, a: 0.08 },
  offset: { x: 0, y: 4 },
  radius: 16,
  spread: 0,
  visible: true,
  blendMode: 'NORMAL'
}];

for (const node of children) {
  const newX = node.x - (minX - padding);
  const newY = node.y - (minY - padding);
  cardFrame.appendChild(node);
  node.x = newX;
  node.y = newY;
}
```

---

## 8. 문서 작성 언어 규칙

**디자인 시스템의 모든 문서(md 파일)는 국문(한국어)으로 작성한다.**

- 토큰명, 컴포넌트명 등 고유 명칭은 영문 그대로 사용 가능.
- 설명, 사용처, 규칙 등 서술 텍스트는 국문으로 작성한다.
- Figma Make 프롬프트 등 도구용 텍스트도 국문 기준으로 작성한다.

> 아이콘 사용 규칙은 각 컴포넌트 md 파일의 "아이콘 사용 규칙" 섹션에서 개별 정의한다.

---

## 9. 토큰 / 라이브러리 일관성 규칙

새로운 컴포넌트 또는 파운데이션 항목을 추가할 때, **기존에 정의된 토큰·라이브러리·스타일이 있으면 반드시 재사용한다.**

- 컬러: `color/*` 변수 바인딩 사용. 하드코딩된 HEX 값 사용 금지.
- 타이포그래피: 아래 §7 규칙 참조.
- 반경, 그림자, 모션: 해당 파운데이션 토큰 바인딩 사용.

### Size 토큰 적용 원칙

**모든 컴포넌트의 Width/Height에는 `size/*` Variables를 바인딩한다.** 임의 px 고정값 사용 금지.

- **Height가 고정인 컴포넌트** (버튼, 인풋, 아이콘 버튼, 아바타, 스피너 등): 해당 사이즈 변형에 맞는 `size/{T-Shirt}` Semantic 토큰을 Height에 바인딩한다.
- **정사각형 컴포넌트** (아이콘, 아이콘 버튼, 아바타, 스피너): Width와 Height 모두 동일한 `size/{T-Shirt}` 토큰을 바인딩한다.
- **Semantic 범위 밖의 값** (예: 20px): Primitive 토큰 `size/{숫자}`를 직접 참조한다.
- **보더 두께**: `size/1`, `size/2`, `size/4` Primitive를 직접 참조한다.
- 각 컴포넌트별 구체적인 사이즈 매핑은 해당 컴포넌트 md 파일의 "크기 (Size)" 섹션에서 정의한다.

### Spacing 토큰 적용 원칙

**모든 컴포넌트의 내부 패딩, 요소 간 간격에는 `spacing/*` Variables를 바인딩한다.** 임의 px 고정값 사용 금지.

- **내부 패딩 (paddingTop/Right/Bottom/Left)**: 해당 값에 맞는 `spacing/{숫자}` 토큰을 바인딩한다.
- **요소 간 간격 (itemSpacing)**: `spacing/{숫자}` 토큰을 바인딩한다.
- **아이콘-텍스트 간격**: `spacing/8` (기본).
- 각 컴포넌트별 구체적인 패딩/간격 값은 해당 컴포넌트 md 파일의 "크기 (Size)" 또는 "디자인 토큰" 섹션에서 정의한다.

### Radius 토큰 적용 원칙

**모든 컴포넌트의 cornerRadius에는 `radius/*` Variables를 바인딩한다.** 임의 px 고정값 사용 금지.

- **Semantic T-Shirt 토큰**을 우선 사용한다: `radius/XS`(4px), `radius/S`(6px), `radius/M`(8px), `radius/L`(12px), `radius/XL`(16px), `radius/FULL`(9999px).
- 컴포넌트 사이즈 변형에 따라 적절한 Radius를 매핑한다 (05 — Radius 페이지의 매핑 표 참조).
- 컴포넌트별 구체적인 Radius 매핑은 해당 컴포넌트 md 파일의 "크기 (Size)" 섹션에서 정의한다.
- `radius/0` (직각)과 `radius/FULL` (완전 원형)은 특수 케이스로 Primitive를 직접 참조해도 된다.

---

## 10. 타이포그래피 규칙

**Figma 문서 내 모든 텍스트는 생성된 타이포그래피 라이브러리(Text Style)를 적용한다.**

- 제목, 본문, 레이블 등 모든 텍스트 노드에 `02 — Typography` 페이지에 정의된 Text Style을 바인딩한다.
- Text Style 없이 fontSize / fontWeight를 직접 지정하는 것을 금지한다.
- 타이포그래피 라이브러리에 없는 스타일이 필요한 경우, 먼저 `02 — Typography` 페이지에 스타일을 추가한 후 적용한다.

---

## 11. Variants 구성 규칙

동일한 컴포넌트가 다양한 베리언트로 구성된 경우, **Figma의 "Combine as Variants" 기능을 사용해 하나의 Component Set으로 통합한다.**

- 개별 COMPONENT 노드를 별개로 나열하는 방식 금지.
- Variant 속성명은 §1의 네이밍 규칙(`{이름}/{변형}/{크기}/{상태}`)을 따른다.
- 개별 변형 컴포넌트를 나열하는 대신, 단일 컴포넌트에 Variant / Size / State / Icon 등을 속성(Properties)으로 정의하여 시스템의 복잡성을 줄인다.

---

## 12. 페이지 내 배치 간격 및 설명 라벨 규칙

### 배치 간격

| 배치 대상 | 최소 간격 |
|---|---|
| 개별 컴포넌트/변수 간 | 50px 이상 |
| 설명 라벨 ↔ 컴포넌트/변수 | 50px 이상 |
| 상위 변형 그룹 간 (Variant 대분류 사이) | 100px 이상 |
| 섹션 간 (대분류 사이) | 100px 이상 |

### 설명 라벨 규칙

모든 컴포넌트 및 변수에는 **종류(Variant), 사이즈(Size), 상태(State) 등을 설명하는 라벨**이 반드시 존재해야 한다.

#### 라벨 배치 원칙
- 컴포넌트/변수를 설명하는 모든 라벨은 **하나의 프레임 안에 포함**하여 관리한다.
- 라벨 프레임은 해당 카드 프레임 내에서 **맨 하단 레이어**에 위치시킨다.
- 라벨의 위치와 스타일은 같은 페이지 내 다른 라벨과 **일관성**을 유지한다.
- 라벨 텍스트에도 타이포그래피 라이브러리(Text Style)를 적용한다 (§10 참조).

#### 라벨 생명주기
| 상황 | 처리 |
|---|---|
| 컴포넌트/변수 **추가** | 기존 라벨의 위치·스타일에 맞춰 설명 라벨을 함께 추가한다 |
| 컴포넌트/변수 **수정** | 변경된 내용에 맞게 해당 설명 라벨을 업데이트한다 |
| 컴포넌트/변수 **삭제** | 해당 컴포넌트/변수를 설명하던 라벨도 함께 제거한다 |

#### 금지 사항
- 설명 라벨 없이 컴포넌트/변수만 배치하는 것 금지.
- 삭제된 컴포넌트/변수의 라벨을 남겨두는 것 금지 (고아 라벨 금지).
- 라벨을 카드 프레임 밖에 배치하는 것 금지.

---

## 13. T-Shirt 사이즈 표기 규칙

Figma 내 컴포넌트의 베리언트 사이즈 표기는 **대문자 T-Shirt 사이즈**를 사용한다.

| 표기 | 의미 |
|---|---|
| `XXL` | Extra Extra Large |
| `XL` | Extra Large |
| `L` | Large |
| `M` | Medium |
| `S` | Small |
| `XS` | Extra Small |
| `XXS` | Extra Extra Small |

- 소문자(`xl`, `lg`, `md`, `sm`) 사용 금지.
- `lg` / `lg` 등 약어 혼용 금지 — 반드시 위 표기 기준을 따른다.

---

## 14. 아이콘 및 기호 사용 규칙

**Figma 문서 내에서 기호적인 요소(화살표, 체크, 닫기, 메뉴 등)가 필요한 경우, 반드시 `01 — Icons` 페이지의 아이콘 컴포넌트 인스턴스를 사용한다.**

#### 금지 대상
- 텍스트 특수 문자(`✓`, `✕`, `→`, `⋯`, `▼` 등)로 아이콘을 대체하는 것 금지.
- 이모지로 아이콘을 대체하는 것 금지.
- 직접 그린 벡터 도형으로 아이콘을 대체하는 것 금지.

#### 원칙
- 필요한 아이콘이 `01 — Icons` 페이지에 없는 경우, **먼저 아이콘 페이지에 추가한 후** 인스턴스를 참조한다.
- 아이콘 크기는 사용되는 컴포넌트의 사이즈 변형에 맞춰 조정한다.
- 이 규칙은 모든 컴포넌트에 공통 적용되며, 각 컴포넌트 md 파일에서 별도로 명시하지 않아도 반드시 준수한다.

> 이 규칙이 각 컴포넌트 md 파일에도 명시되어 있지만, 글로벌 규칙으로서 본 가이드에서 최상위 우선순위로 강제한다.

---

## 15. 디자인-코드 연결 규칙

**디자인 토큰은 코드와 동기화 가능한 형태로 관리한다.**

토큰을 JSON 형식으로 내보낼 수 있도록 구조화하면, 디자인과 개발 간 일관성을 보장하고 AI가 토큰을 직접 참조하여 코드를 생성할 수 있다.

### 토큰 Export 구조 예시

```json
{
  "color": {
    "primary": {
      "500": "#4F46E5"
    },
    "button": {
      "primary": {
        "background": "{color.primary.500}"
      }
    }
  },
  "spacing": {
    "4": "4px",
    "8": "8px",
    "16": "16px"
  },
  "radius": {
    "M": "8px",
    "L": "12px"
  }
}
```

### 권장 도구
- **Figma Variables**: Figma 네이티브 변수 시스템 (현재 사용 중).
- **Tokens Studio**: Figma 플러그인 기반 토큰 관리 및 JSON Export.
- **Style Dictionary**: 토큰 JSON을 플랫폼별 코드(CSS, iOS, Android)로 변환.

### 원칙
- Figma Variables에 정의된 토큰과 코드에서 사용하는 토큰 이름을 일치시킨다.
- Primitive 토큰 → Semantic 토큰 → 컴포넌트 바인딩의 참조 체인을 유지한다.
- 토큰 변경 시 Figma와 코드 양쪽에 동시 반영한다.

---

## Change Log

> **정책**: 이 문서를 수정할 때마다 아래 Change Log에 항목을 추가하고, **Figma의 `Change Log` 페이지도 동일 내용으로 즉시 동기화한다.**
> Figma 작업(컴포넌트 추가·수정·삭제 등)이 발생한 경우에도 해당 변경 내용을 이 문서의 Change Log와 Figma Change Log 페이지에 동시에 기록한다.

| 버전 | 날짜 | 변경 내용 |
|---|---|---|
| v1.0 | 2026.04.08 | 최초 작성 — 페이지 네이밍, 프레임 구조, Height 규칙 통합 |
| v1.1 | 2026.04.09 | 배경 카드 프레임 패딩 48px → 100px 변경, 프레임 생성 규칙 문장 수정 |
| v1.2 | 2026.04.10 | 아이콘 사용 규칙 강제화(§5), 공통 Height HUG 규칙 제거(컴포넌트별 개별 정의로 이관), 신규 컴포넌트 8종 페이지 목록 추가 |
| v1.3 | 2026.04.10 | 중복 제거 — Variants 네이밍 규칙 §1 이관, 체크리스트(§6) 및 금지 사항 표(§7) 제거 |
| v1.4 | 2026.04.10 | §6 토큰 일관성 규칙, §7 타이포그래피 규칙, §8 Variants 구성(Combine as Variants), §9 배치 간격 규칙, §10 T-Shirt 사이즈 표기 규칙 추가. "버전 히스토리" → "Change Log"로 명칭 변경 |
| v1.5 | 2026.04.10 | Change Log Figma 동기화 정책 추가 — md 수정 및 Figma 작업 시 양쪽 Change Log 동시 기록 의무화 |
| v1.6 | 2026.04.10 | Typography Label weight Medium→SemiBold(lg/md/sm). Size Primitive를 실제px값 기반으로, Semantic을 T-Shirt 공통 체계로 변경. Spacing Semantic 제거·Primitive 토큰명 실제 px 기반으로 변경. Border Radius→Radius 파일명·페이지명 변경, Semantic T-Shirt 체계로 변경. Button 좌우 패딩 한 단계 축소·XS 사이즈 추가·Text 변형 추가. Select Surface 스타일·3가지 사이즈·아이콘 크기 사이즈별 추가. Textarea→Text Area 파일명·페이지명 변경·3가지 사이즈 추가. Alert·Toast 기호 텍스트→아이콘 인스턴스로 변경. Empty State→Data Case 파일명·페이지명 변경·Error/Loading/No Permission/Offline 변형 추가. Card·Drawer 액션 버튼을 Button 컴포넌트 인스턴스로 명시 |
| v1.8 | 2026.04.12 | md 파일 넘버링을 Figma 페이지 넘버링과 동기화(01→02~37→38). Typography Label/xs SemiBold 600으로 통일. §5 아이콘 사용 규칙을 각 컴포넌트 md로 이관, 공통 가이드에서 제거. §5를 '문서 작성 언어 규칙(국문 작성)' 으로 교체. |
| v2.0 | 2026.04.13 | AI 네이티브 4계층 구조 개요 추가. §2 카드 프레임 리사이징 규칙 추가. §3 Auto Layout 규칙 신설. §5 레이어 네이밍 규칙 신설. §6 컴포넌트 Description 문서화 규칙 신설. §12 배치 간격 대폭 개정 — 설명 라벨 규칙(배치·생명주기·금지사항) 추가, 간격 기준 세분화. §14 아이콘 및 기호 사용 규칙 신설(글로벌 강제). §15 디자인-코드 연결 규칙 신설. §1 Variants 네이밍 보완. §11 Variants 구성에 속성 활용 원칙 보완. 전체 섹션 재넘버링(§1~§15). Button 변형 체계 재구조화(Fill/Border/Text × Primary/Secondary, XS 사이즈 제거) |
| v1.7 | 2026.04.11 | Figma 파일 v1.6 전면 동기화: (1) 페이지 rename — Changelog 표기 통일, 05 Border Radius→Radius, 10 Textarea→Text Area, 19 Empty State→Data Case. (2) 누락 페이지 8개 생성(31~38 Search/Menu/Date & Time Picker/Slider/FAB/Navigation Bar/App Bar/Bottom Sheet). (3) 03 Icon Button·05 Avatar 페이지의 orphan 컴포넌트를 카드 프레임에 재parent. (4) Variables 재구성 — Spacing(semantic 제거, px 기반 16개), Radius(컬렉션명 Border Radius→Radius/Primitive, Radius/Semantic T-Shirt 6종 신규), Size(Primitive px 19종, Semantic T-Shirt 8종 재작성). (5) Effect Styles — Shadow/Focus spread 3px 수정. (6) 전 컴포넌트 페이지 23종을 Combine as Variants로 결합, variant property 이름/T-Shirt 대문자 표기 일괄 정규화. (7) Button에 XS 사이즈·Text 변형 추가, Select에 Border/Surface×L/M/S×4state 24변형 구성, Text Area L/M/S 사이즈 추가, Data Case Empty/Error/Loading/No Permission/Offline 변형 추가. (8) Card·Drawer·Alert·Toast 페이지에 v1.6 규칙 노트 추가. (9) Change Log Figma 페이지에 v1.0~v1.6 전체 이력 기록. ⚠️ 알려진 이슈: Label/xs는 수동 수정 시 모두 SemiBold로 바뀐 상태 — Figma 데스크탑에서 Medium으로 되돌려야 함 |
