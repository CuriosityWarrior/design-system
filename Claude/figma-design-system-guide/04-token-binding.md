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

> 📐 정확한 fontSize / lineHeight / letterSpacing / 사용처는 [`../design-system/foundations/02-typography.md`](../design-system/foundations/02-typography.md)의 Semantic 토큰 표를 단일 출처(SoT)로 한다. 위 표는 빠른 참조용 요약이며, 값 충돌 시 02-typography.md를 우선한다.
