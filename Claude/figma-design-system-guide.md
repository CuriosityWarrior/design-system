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

### 전체 페이지 구조

```
Cover
Changelog

[ FOUNDATIONS ]
01 — Color
02 — Typography
03 — Spacing
04 — Shadow
05 — Border Radius
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
10 — Textarea
11 — Select
12 — Checkbox
13 — Radio
14 — Toggle
15 — Alert
16 — Toast
17 — Progress Bar
18 — Skeleton
19 — Empty State
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

## 3. 컴포넌트 Height 규칙

### Height → Hug Contents

모든 컴포넌트의 Height 값은 **Hug Contents** (`HUG`) 로 설정한다.
Fixed 고정값 사용 금지.

| 설정 | 값 |
|---|---|
| layoutSizingVertical | `HUG` |
| layoutSizingHorizontal | 컴포넌트 성격에 따라 결정 |

#### 이유
- Fixed Height는 콘텐츠 변경 시 레이아웃 이탈이 발생함
- Hug Contents는 내부 콘텐츠 크기에 맞게 자동 조정됨
- Auto Layout과 함께 사용할 때 일관성 유지

#### 적용 범위
- 모든 컴포넌트(`COMPONENT` 타입) 노드
- 컴포넌트 내부의 Auto Layout 프레임

#### 예외
- 명시적으로 고정 높이가 필요한 컴포넌트 (예: Avatar, Spinner 등 정사각형 요소)
  - 이 경우 Width와 Height 모두 Fixed로 설정하고 주석으로 명시

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

### Height Hug Contents 일괄 적용 스크립트

```javascript
const page = figma.currentPage;
const cardFrame = page.children.find(n => n.type === 'FRAME');
const components = cardFrame.findAll(n => n.type === 'COMPONENT');

for (const c of components) {
  if (c.layoutSizingVertical === 'FIXED') {
    c.layoutSizingVertical = 'HUG';
  }
}
```

---

## 5. 아이콘 사용 규칙

컴포넌트 내 기호 표현이 필요할 때, `01 — Icons` 페이지에 동일한 형태의 아이콘이 존재하면 텍스트 특수 문자 대신 해당 아이콘 컴포넌트 인스턴스를 사용한다.

---

## 6. 신규 컴포넌트 추가 시 체크리스트

- [ ] 페이지 이름이 `{두 자리 번호} — {이름}` 형식인지 확인
- [ ] `[ COMPONENTS ]` 섹션 하단에 순서대로 배치
- [ ] 모든 노드가 흰색 카드 프레임 안에 있는지 확인
- [ ] 카드 프레임 이름이 컴포넌트 이름과 동일한지 확인
- [ ] 컴포넌트 Height가 `HUG` 로 설정되어 있는지 확인
- [ ] 컴포넌트 네이밍이 `{이름}/{변형}/{크기}/{상태}` 형식인지 확인

---

## 7. 금지 사항

| 항목 | 금지 | 대신 |
|---|---|---|
| 페이지 이름 | 하이픈(`-`) 사용 | em dash(`—`) 사용 |
| 페이지 이름 | 한글 작성 | 영문 Title Case |
| 섹션 구분자 | 소문자 | 항상 UPPERCASE |
| 컴포넌트 배치 | 캔버스 바닥 직접 배치 | 흰색 카드 프레임 안에 배치 |
| 컴포넌트 Height | FIXED 고정값 | HUG (예외 제외) |

---

## 버전 히스토리

| 버전 | 날짜 | 변경 내용 |
|---|---|---|
| v1.0 | 2026.04.08 | 최초 작성 — 페이지 네이밍, 프레임 구조, Height 규칙 통합 |
| v1.1 | 2026.04.09 | 배경 카드 프레임 패딩 48px → 100px 변경, 프레임 생성 규칙 문장 수정 |
