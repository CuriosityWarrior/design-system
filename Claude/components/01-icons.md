# 컴포넌트: 아이콘 (Icons)

## 개요

디자인 시스템 전반에서 사용하는 **단일 아이콘 라이브러리**를 Figma 컴포넌트로 등재하고, 모든 사용처에서 **인스턴스 교체** 방식으로 사용한다.

- 아이콘 자체는 디자인 시스템 외부의 **사내 아이콘 라이브러리**에서 수급한다.
- Figma에는 라이브러리 아이콘 1종 → 1 Component로 등재한다.
- 사용처(버튼·인풋·알럿 등)에서는 항상 **컴포넌트 인스턴스**를 배치하고, 필요 시 인스턴스 단위로 색상·크기를 오버라이드한다.

---

## 아이콘 라이브러리 출처

> 🔁 **변경 가능 파라미터** — 사내 라이브러리가 교체되면 아래 두 줄만 수정하면 된다.

| 항목 | 값 |
|---|---|
| 라이브러리 이름 | `_TBD: 사내 아이콘 라이브러리 이름_` |
| 소스 URL | `_TBD: GitHub repo URL 또는 라이브러리 페이지 URL_` |
| 라이선스 | `_TBD_` |
| 등재 기준 버전 | `_TBD: vX.Y.Z_` |

- 라이브러리 버전 업그레이드 시: 본 문서의 "등재 기준 버전"을 갱신하고, Figma `01 — Icons` 페이지의 컴포넌트 셋도 같은 버전으로 일괄 교체한다. Change Log에 변경 사항을 기록한다.

---

## 디자인 토큰

| 토큰 | 값 |
|---|---|
| 기본 색상 | `color/primary/default` (#F26A00) |
| 사이즈 토큰 | `size/{T-Shirt}` Semantic 토큰 바인딩 (Width = Height) |
| 사용처 오버라이드 | 인스턴스 단위 `fills` 변경으로 색상·상태 표현 |

> 📐 색상과 상태(Hover/Disabled 등)는 **아이콘 컴포넌트 자체에 정의하지 않는다.** 사용처(버튼·인풋·알럿 등)에서 인스턴스 오버라이드로 표현한다.

---

## 크기 (Size)

| 크기 | 토큰 | Width × Height |
|---|---|---|
| **L** | `size/L` | 24 × 24px |
| **M** | `size/M` | 20 × 20px |
| **S** | `size/S` | 16 × 16px |
| **XS** | `size/XS` | 12 × 12px |

- **모든 사이즈는 정사각** (`layoutSizingHorizontal` / `layoutSizingVertical` 모두 `FIXED`, Width = Height).
- 사용처별 권장 사이즈는 해당 컴포넌트 md의 "아이콘 포함" 섹션에서 정의한다 (예: Button XL → 아이콘 M, Button S → 아이콘 XS).

---

## 색상 (Color)

- **기본 색상은 `color/primary/default`** (오렌지)로 설정한다.
- 사용처에서 의미에 따라 인스턴스 단위로 변경:

| 사용 맥락 | 권장 토큰 |
|---|---|
| 기본/액션 강조 | `color/primary/default` |
| 본문 텍스트 옆 인라인 | `color/text/primary` |
| 보조/메타 | `color/text/secondary` |
| 비활성 | `color/text/disabled` |
| 반전 배경 | `color/text/inverse` |
| Success / Warning / Error / Info | `color/{status}/default` |

---

## 상태 (State)

- 아이콘 컴포넌트 자체에 State Variant를 두지 않는다.
- Hover / Disabled / Active 등 상태 표현은 **사용처 컴포넌트의 인스턴스 오버라이드**로 처리한다.
  - 예: Button Disabled 상태 → 버튼 내 아이콘 인스턴스의 fill을 `color/text/disabled`로 오버라이드.

---

## 사이즈 동작

| 속성 | 값 |
|---|---|
| layoutSizingHorizontal | `FIXED` |
| layoutSizingVertical | `FIXED` |
| 비율 | Width = Height (정사각 강제) |

---

## Figma Variants 네이밍

```
Icon / {Name} / {Size}
```

예시:
- `Icon / Check / L`
- `Icon / Close / M`
- `Icon / ChevronDown / S`
- `Icon / Search / XS`

- `{Name}`은 라이브러리 원본 이름을 그대로 사용한다 (PascalCase 권장).
- `{Size}`는 `XS / S / M / L` 중 하나 (대문자 T-Shirt 표기, [figma-design-system-guide/03-component-authoring.md#t-shirt-사이즈-표기-규칙](../figma-design-system-guide/03-component-authoring.md#t-shirt-사이즈-표기-규칙) 준수).

---

## 사용 원칙

> 📌 시각 정렬, 텍스트와 비례, 인스턴스 의무 등 **공통 사용 원칙은 [figma-design-system-guide/05-doc-conventions.md#아이콘-사용-규칙-공통](../figma-design-system-guide/05-doc-conventions.md#아이콘-사용-규칙-공통)** 을 따른다.

본 문서는 아이콘 컴포넌트 자체의 스펙(라이브러리 출처, 사이즈, 색상, 네이밍)만 정의한다.

---

## Figma 등재 방식

사내 아이콘 라이브러리에서 SVG / Figma 컴포넌트를 직접 가져와 **Figma MCP로 `01 — Icons` 페이지에 붙여넣는 방식**으로 등재한다. Figma Make 프롬프트는 사용하지 않는다.

### 등재 순서
1. 사내 라이브러리 (위 "아이콘 라이브러리 출처" 참조)에서 아이콘 SVG / Figma 컴포넌트를 복사한다.
2. Figma MCP로 `01 — Icons` 페이지의 카드 프레임 내부에 붙여넣는다.
3. 각 아이콘을 Component로 변환 후 [Variants 네이밍 규칙](../figma-design-system-guide/03-component-authoring.md#variants-네이밍-규칙)(`Icon / {Name} / {Size}`)을 적용한다.
4. 4 사이즈(XS / S / M / L) 변형을 생성하고 Width·Height에 `size/{T-Shirt}` Variables를 바인딩한다.
5. 기본 색상 `color/primary/default`를 fills에 바인딩한다.
6. 4 사이즈를 **Combine as Variants**로 결합한다 ([Variants 구성 규칙](../figma-design-system-guide/03-component-authoring.md#variants-구성-규칙)).

### 등재 전략 (협의 필요)
사내 라이브러리의 총 아이콘 수와 도메인에 따라 등재 범위가 달라진다. 본 가이드와 별도로 **디자인 시스템 생성 커맨드**에서 도메인·개수를 인터랙티브 질의해 맞춤 등재할 예정.

- 라이브러리 총 아이콘 수 < `N` (예: 200) → **전체 등재**
- 라이브러리 총 아이콘 수 ≥ `N` → **도메인별 핵심 + 공통 자주 사용 아이콘**만 등재 (총 n00개 이내, "자주 사용" 기준은 협의)
