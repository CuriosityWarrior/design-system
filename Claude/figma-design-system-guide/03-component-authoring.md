# 컴포넌트 작성 규칙

개별 컴포넌트를 Figma에 작성할 때 따르는 구조 규칙 — Sizing, Variants 구성·네이밍, T-Shirt 사이즈 표기.

## 컴포넌트 Sizing 규칙

컴포넌트의 `layoutSizingHorizontal` / `layoutSizingVertical` 값(HUG / FILL / FIXED)은 **각 컴포넌트 md 파일에서 개별로 정의**한다.
공통 규칙으로 일괄 강제하지 않되, 아래 판단 기준을 따른다.

### HUG / FILL / FIXED 판단 기준

| 모드 | 사용 시점 | 대표 컴포넌트 예시 |
|---|---|---|
| **HUG** | 콘텐츠(텍스트·자식 요소) 길이에 따라 자연스럽게 크기가 결정되어야 할 때 | Button(가로), Badge, Chip, Tooltip |
| **FILL** | 부모 컨테이너의 가용 공간을 채워야 할 때 (가변 폭/높이) | Input(가로), Text Area(가로), Card 본문 영역, Modal 내부 폼 |
| **FIXED** | T-Shirt 토큰(`size/*`) 또는 디자인 시스템에서 정의한 정해진 값이 필요할 때 | Avatar, Icon, Icon Button, Spinner, 고정 Height 버튼 |

### 추가 원칙
- **Height 고정 컴포넌트** (Button, Input 등)는 Height만 FIXED(`size/{T-Shirt}` 바인딩), Width는 HUG 또는 FILL로 자유롭게 가변.
- **정사각 컴포넌트** (Avatar, Icon, Icon Button, Spinner)는 Width·Height 모두 FIXED + 동일 토큰.
- **반응형은 좌우 가변(FILL/HUG)으로 제공**한다. 디바이스(모바일/태블릿/데스크탑)별 별도 변형은 현재 버전에서는 정의하지 않는다 — 향후 v3.0에서 검토.
- 각 컴포넌트 문서의 "크기 (Size)" 또는 "사이즈 동작" 섹션에서 해당 컴포넌트의 sizing 방식을 명시한다.
- 문서에 명시되지 않은 채 임의 값(예: `100px`)으로 Height를 Fixed 지정하는 것을 금지한다.

---

## Variants 구성 규칙

**적용 조건**: 동일한 컴포넌트에 Style(변형), Size(크기), State(상태) 중 **하나라도 2종 이상 존재하는 경우**, Figma의 "Combine as Variants" 기능을 사용해 하나의 **Component Set**으로 통합한다.

- **단일 변형 컴포넌트**: Style·Size·State 각각 1종씩만 존재하면 개별 `COMPONENT` 노드로 유지한다 — Component Set 강제 적용 금지.
- **다중 변형 컴포넌트**: 변형이 2개 이상임에도 개별 `COMPONENT` 노드로 별개 나열하는 것을 금지한다.
- Variant 속성명은 아래 [Variants 네이밍 규칙](#variants-네이밍-규칙)을 따른다.

> **판단 기준 예시**
> - Button — Fill/Border/Text × Primary/Secondary/Danger × XL/L/M/S × Default/Hover/Focus/Disabled → 다중 변형 → Component Set ✅
> - Card — 변형 없이 Default 1종만 존재 → 단일 변형 → 개별 COMPONENT 유지 ✅
> - Modal — Default 1종만 존재 → 단일 변형 → 개별 COMPONENT 유지 ✅

---

## Variants 네이밍 규칙

- Figma 컴포넌트의 Variants 네이밍은 `{이름}/{변형}/{크기}/{상태}` 형식을 따른다.
- 각 축은 슬래시(`/`)로 구분하고, 축이 불필요한 경우 생략할 수 있다.
- 예:
  - `Button / Primary / LG / Default`
  - `Icon Button / Tertiary / MD / Hover`
  - `Badge / Success / SM`
  - `Divider / Horizontal / Default`

---

## T-Shirt 사이즈 표기 규칙

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
- `lg` / `md` / `sm` 등 소문자 약어와 대문자 표기를 혼용 금지 — 반드시 위 표기 기준(`XS`, `S`, `M`, `L`, `XL`)을 따른다.
