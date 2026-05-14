# 토큰 및 스타일 바인딩 규칙

컴포넌트에 어떤 토큰·스타일을 바인딩해서 사용할지에 대한 규칙 — Size · Spacing · Radius Variables, 타이포그래피 Text Style.

## 토큰 / 라이브러리 일관성 규칙

새로운 컴포넌트 또는 파운데이션 항목을 추가할 때, **기존에 정의된 토큰·라이브러리·스타일이 있으면 반드시 재사용한다.**

- 컬러: `color/*` 변수 바인딩 사용. 하드코딩된 HEX 값 사용 금지.
- 타이포그래피: 아래 [타이포그래피 규칙](#타이포그래피-규칙) 참조.
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

## 타이포그래피 규칙

**컴포넌트 정의 내부의 모든 텍스트는 생성된 타이포그래피 라이브러리(Pretendard Text Style)를 적용한다.**

- 컴포넌트(Component / Component Set) 내부의 제목, 본문, 레이블 등 모든 텍스트 노드에 `02 — Typography` 페이지에 정의된 Text Style을 바인딩한다.
- Text Style 없이 fontSize / fontWeight를 직접 지정하는 것을 금지한다.
- 타이포그래피 라이브러리에 없는 스타일이 필요한 경우, 먼저 `02 — Typography` 페이지에 스타일을 추가한 후 적용한다.

> ⚠️ **페이지 헤더와 Change Log entries는 Inter** — 페이지 타이틀(Inter Bold 32)과 페이지 설명(Inter Medium 15), Change Log entries 텍스트는 폰트 로드 비용·메타 라벨 정책에 따라 Pretendard가 아닌 **Inter**를 사용한다. 페이지 헤더 정본 스펙은 [02-frame-and-layout.md#페이지-헤더-모든-컴포넌트파운데이션-페이지-공통](02-frame-and-layout.md#페이지-헤더-모든-컴포넌트파운데이션-페이지-공통)을 참조한다. 본 절의 Pretendard 규칙은 **컴포넌트 정의 내부 텍스트에만** 적용된다.

### Style × Size 매트릭스 (요약)

| 카테고리 | XL | LG | MD | SM | XS |
|---|---|---|---|---|---|
| **Display** | 40 Bold | 32 Bold | 28 Bold | 24 SemiBold | — |
| **Display 2XL** (별도) | 48 Bold | — | — | — | — |
| **Heading** | 20 SemiBold | 18 SemiBold | 16 SemiBold | 14 SemiBold | 13 SemiBold |
| **Body** | 20 Regular | 18 Regular | 16 Regular (BASE) | 14 Regular | 13 Regular |
| **Label** | — | 16 SemiBold | 14 SemiBold | 13 SemiBold | 12 SemiBold |
| **Caption** | — | — | — | — | 12 Regular |

> 📐 정확한 fontSize / lineHeight / letterSpacing / 사용처는 [`../foundations/02-typography.md`](../foundations/02-typography.md)의 Semantic 토큰 표를 단일 출처(SoT)로 한다. 위 표는 빠른 참조용 요약이며, 값 충돌 시 02-typography.md를 우선한다.

---

## 토큰 바인딩 검증 의무

컴포넌트의 속성을 추가·변경한 직후, **해당 속성이 Variables(또는 Text Style)에 바인딩되어 있는지 반드시 검증**한다. 임의 px·HEX 값으로 남아있지 않은지 확인한다.

### 속성별 검증 항목

| 속성 | 검증식 (boundVariables 또는 styleId 존재) |
|---|---|
| Width | `boundVariables.width` 존재, 또는 부모 Auto Layout에 의해 결정 |
| Height | `boundVariables.height` 존재, 또는 부모 Auto Layout에 의해 결정 |
| paddingTop / paddingRight / paddingBottom / paddingLeft | 4면 모두 `boundVariables.padding{Top|Right|Bottom|Left}` 존재 |
| itemSpacing | `boundVariables.itemSpacing` 존재 |
| cornerRadius | 균일한 경우 `boundVariables.cornerRadius`, 비균일이면 4모서리별 `boundVariables.{topLeft|topRight|bottomLeft|bottomRight}Radius` |
| fills (SOLID 컬러) | `boundVariables.fills` 또는 `fillStyleId` 존재 |
| strokes (SOLID 컬러) | `boundVariables.strokes` 또는 `strokeStyleId` 존재 |
| 텍스트 노드 | `textStyleId !== ""` (fontSize / fontWeight / lineHeight / letterSpacing 직접 지정 금지) |
| effects (Drop Shadow 등) | `effectStyleId !== ""` |

- 어느 한 속성이라도 직접 값으로 들어가 있고 boundVariables / styleId에 없으면 **위반**이다.
- 자동 검증 스크립트는 `page.loadAsync()`를 호출한 후 `mcp__figma__get_metadata`로 노드를 읽어야 한다 (dynamic-page 모드 stale 데이터 방지).

### 검증 대상 제외

- 그라데이션 fills (GRADIENT_LINEAR / GRADIENT_RADIAL 등), 이미지 fills (IMAGE) 등 SOLID 단일 컬러가 아닌 fills는 Variables 바인딩 대상이 아니다.
- Component Set 노드 자체의 width / height는 변형 배치에 의해 자동 결정되므로 검증 대상에서 제외한다.

---

## 토큰 부재 시 신설 의무

**컴포넌트가 사용해야 하는 값이 Variables 라이브러리(또는 Text Style / Effect Style 라이브러리)에 존재하지 않으면, 먼저 토큰을 신설한 후 바인딩한다.** 라이브러리에 없는 값을 그대로 사용하는 것을 금지한다.

| 토큰 종류 | md 정의 위치 | Figma 페이지 | 라이브러리 형식 |
|---|---|---|---|
| Color | [`../foundations/01-color.md`](../foundations/01-color.md) | `01 — Color` | Variables (COLOR) |
| Typography | [`../foundations/02-typography.md`](../foundations/02-typography.md) | `02 — Typography` | Text Style |
| Spacing | [`../foundations/03-spacing.md`](../foundations/03-spacing.md) | `03 — Spacing` | Variables (FLOAT) |
| Shadow | [`../foundations/04-shadow.md`](../foundations/04-shadow.md) | `04 — Shadow` | Effect Style |
| Radius | [`../foundations/05-radius.md`](../foundations/05-radius.md) | `05 — Radius` | Variables (FLOAT) |
| Motion | [`../foundations/06-motion.md`](../foundations/06-motion.md) | `06 — Motion` | (코드 토큰) |
| Size | [`../foundations/07-size.md`](../foundations/07-size.md) | `07 — Size` | Variables (FLOAT) |

### 신설 절차

1. **확인** — 사용하려는 값이 라이브러리에 있는지 검색한다 (`mcp__figma__get_variable_defs` 또는 Figma Variables 패널).
2. **없으면 신설** — 위 표의 md 위치에 토큰 정의를 추가하고, Figma 해당 페이지에도 동기화한다.
3. **바인딩** — 신설된 토큰을 컴포넌트 속성에 바인딩한다.
4. **CHANGELOG 기록** — 토큰 추가 사실을 [`CHANGELOG.md`](CHANGELOG.md)와 Figma `Change Log` 페이지에 동시 기록한다.

> 📌 본 절은 위 [타이포그래피 규칙](#타이포그래피-규칙)의 "라이브러리에 없는 스타일이 필요한 경우, 먼저 `02 — Typography` 페이지에 스타일을 추가한 후 적용한다"를 Color · Size · Spacing · Radius · Shadow까지 확장한 것이다. 이제 모든 토큰 종류에 동일한 "선(先)신설 → 후(後)바인딩" 원칙이 적용된다.

### 자주 발생하는 신설 케이스

- `padding: 10px`가 필요한데 `spacing/8`(8px)과 `spacing/12`(12px)만 있는 경우 → `spacing/10`을 신설.
- 신규 컬러 변형(예: `color/info/tint`)이 필요한 경우 → `01 — Color` 페이지에 추가 후 바인딩.
- 신규 사이즈 변형이 필요한 경우 (예: 18px 아이콘) → `size/18` Primitive와 필요 시 `size/icon/XXS` Semantic alias 신설.
