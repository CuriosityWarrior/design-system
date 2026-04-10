# Figma Design System 생성 규칙

## 개요

디자인 시스템을 Figma에서 생성할 때 따라야 하는 전체 규칙 문서.
페이지 네이밍, 프레임 구조, 컴포넌트 작성 기준을 포함한다.

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
- 예:
  - `Button / Primary / lg / Default`
  - `Icon Button / Ghost / md / Hover`
  - `Badge / Success / sm`
  - `Divider / Horizontal / Default`

### 전체 페이지 구조

```
Cover
Changelog

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

#### 금지 사항
- 컴포넌트를 흰색 카드 프레임 없이 캔버스 바닥에 직접 배치하는 것 금지
- 카드 프레임 없이 텍스트 노드만 캔버스에 배치하는 것 금지

---

## 3. 컴포넌트 Sizing 규칙

컴포넌트의 `layoutSizingHorizontal` / `layoutSizingVertical` 값(HUG / FILL / FIXED)은 **각 컴포넌트 md 파일에서 개별로 정의**한다.
공통 규칙으로 일괄 강제하지 않는다.

- 각 컴포넌트 문서의 "크기 (Size)" 또는 "사이즈 동작" 섹션에서 해당 컴포넌트의 sizing 방식을 명시한다.
- 문서에 명시되지 않은 채 임의 값(예: `100px`)으로 Height를 Fixed 지정하는 것을 금지한다.

---

## 4. Figma MCP로 일괄 적용하는 방법

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

## 5. 아이콘 사용 규칙

컴포넌트 내 기호 표현(체크, X, 화살표, 검색, 메뉴 등)은 **반드시 `01 — Icons` 페이지의 아이콘 컴포넌트 인스턴스를 사용한다.**

### 금지
- 텍스트 특수 문자(`✓`, `✕`, `→`, `←`, `⋯`, `✱` 등)로 아이콘을 대체하는 것 금지
- 이모지(`✅`, `❌`, `🔍` 등)로 아이콘을 대체하는 것 금지
- 직접 그린 벡터 도형(Line, Ellipse 등)으로 아이콘을 대체하는 것 금지

### 필요한 아이콘이 없는 경우
1. 먼저 `01 — Icons` 페이지에 아이콘 컴포넌트를 추가한다.
2. 추가한 후 다른 컴포넌트에서 해당 인스턴스를 참조한다.
3. 임시로 텍스트 기호나 도형으로 대체하는 것을 금지한다.

### 검증
모든 컴포넌트 작성/수정 완료 후, 내부에 텍스트 노드로 기호가 들어있지 않은지 확인한다.

---

## 6. 토큰 / 라이브러리 일관성 규칙

새로운 컴포넌트 또는 파운데이션 항목을 추가할 때, **기존에 정의된 토큰·라이브러리·스타일이 있으면 반드시 재사용한다.**

- 컬러: `color/*` 변수 바인딩 사용. 하드코딩된 HEX 값 사용 금지.
- 사이즈: `size/*` 변수 바인딩 사용. 임의 px 고정값 사용 금지.
- 타이포그래피: 아래 §7 규칙 참조.
- 반경, 그림자, 모션: 해당 파운데이션 토큰 바인딩 사용.

---

## 7. 타이포그래피 규칙

**Figma 문서 내 모든 텍스트는 생성된 타이포그래피 라이브러리(Text Style)를 적용한다.**

- 제목, 본문, 레이블 등 모든 텍스트 노드에 `02 — Typography` 페이지에 정의된 Text Style을 바인딩한다.
- Text Style 없이 fontSize / fontWeight를 직접 지정하는 것을 금지한다.
- 타이포그래피 라이브러리에 없는 스타일이 필요한 경우, 먼저 `02 — Typography` 페이지에 스타일을 추가한 후 적용한다.

---

## 8. Variants 구성 규칙

동일한 컴포넌트가 다양한 베리언트로 구성된 경우, **Figma의 "Combine as Variants" 기능을 사용해 하나의 Component Set으로 통합한다.**

- 개별 COMPONENT 노드를 별개로 나열하는 방식 금지.
- Variant 속성명은 §1의 네이밍 규칙(`{이름}/{변형}/{크기}/{상태}`)을 따른다.

---

## 9. 페이지 내 배치 간격 규칙

한 페이지 내에 컴포넌트, 베리언트, 설명 텍스트 등 여러 그룹이 배치될 경우, **그룹 간 간격은 80px**을 기본으로 한다.

| 배치 대상 | 간격 |
|---|---|
| 카테고리 레이블 → 아이콘/컴포넌트 그룹 | 12px |
| 컴포넌트 그룹 간 (카테고리 사이) | 48px |
| 섹션 간 (대분류 사이) | 80px |

---

## 10. T-Shirt 사이즈 표기 규칙

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
