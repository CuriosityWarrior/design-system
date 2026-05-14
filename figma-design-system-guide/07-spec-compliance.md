# 컴포넌트 md ↔ Figma 정합성 검증 규칙

각 컴포넌트 md 파일은 해당 컴포넌트의 **사양서**이고, Figma 파일은 그 **구현**이다. 본 문서는 둘 사이의 정합성을 검증하는 절차를 정의한다.

> **관계 요약**: `components/{NN}-{name}.md` = 사양 (값·구조 정의) / Figma `{NN} — {Name}` 페이지 = 구현. 사양과 구현이 어긋나면 디자인 시스템 전체가 무너지므로, 변경 시마다 양쪽을 비교 검증한다.

---

## 검증 항목

각 컴포넌트 md에 정의된 다음 항목들이 Figma 구현과 일치하는지 검증한다.

| 검증 축 | md 정의 위치 | Figma 검증 대상 |
|---|---|---|
| **변형 목록** | "변형 (Variant)" / "종류" 섹션 + 네이밍 규칙 | Component Set의 variantProperties 및 각 variant 존재 여부 |
| **사이즈별 토큰 매핑** | "크기 (Size)" 섹션의 Size 토큰 표 | 각 사이즈 variant의 width / height boundVariables |
| **컬러 변형** | "변형 (Variant)" 섹션의 컬러 토큰 | 각 variant의 fills / strokes boundVariables |
| **상태 (State)** | "상태 (State)" 섹션 | 상태 변형 존재 + 상태별 시각 변화 (배경·보더·opacity 등) |
| **패딩 / 간격** | "디자인 토큰" 또는 "Size/Spacing 토큰 바인딩" 섹션 | paddingTop/Right/Bottom/Left, itemSpacing boundVariables |
| **반경 (Radius)** | "디자인 토큰" 섹션 | cornerRadius boundVariables |
| **타이포그래피** | "디자인 토큰" 또는 "폰트" 섹션 | 텍스트 노드의 textStyleId |
| **Sizing 모드** | "사이즈 동작" / "레이아웃 규칙" 섹션 (HUG/FILL/FIXED) | layoutSizingHorizontal / layoutSizingVertical |
| **아이콘 인스턴스** | "아이콘 사용 규칙" 섹션 | 텍스트 기호(✓✕→ 등) 부재, 아이콘 INSTANCE 사용 여부 |

---

## 검증 절차

### 1. 사전 준비

- `mcp__figma__get_metadata`로 검증 대상 페이지(또는 Component Set)의 raw 구조를 읽는다.
- 자동 검증 시 `page.loadAsync()`를 먼저 호출한다 ([04-token-binding.md#토큰-바인딩-검증-의무](04-token-binding.md#토큰-바인딩-검증-의무) 참조).
- 해당 컴포넌트의 `components/{NN}-{name}.md` 파일을 읽어 사양을 확보한다.

### 2. 항목별 비교

각 검증 축에 대해 md의 정의와 Figma 노드 속성을 1:1 비교한다.

#### 변형 목록 비교

- md에 정의된 모든 variant 조합 (예: Button — Style × Emphasis × Size × State = 3 × 3 × 5 × 4 = 180 조합)이 Figma Component Set에 모두 존재하는지 확인한다.
- Figma에만 있고 md에 없는 variant도 위반이다 (사양 누락 또는 잉여 variant).
- Variant 네이밍이 md와 일치하는지 확인한다 (T-Shirt 대문자 표기 등, [03-component-authoring.md#variants-네이밍-규칙](03-component-authoring.md#variants-네이밍-규칙) 준수).

#### 사이즈 토큰 매핑 비교

- md의 "크기 (Size)" 표에 명시된 토큰 (예: `size/avatar/XL → size/XL = 48px`)이 Figma variant의 width / height boundVariables와 일치하는지 확인한다.
- 사이즈가 px 하드코딩되어 있고 boundVariables가 비어있으면 위반이다.

#### 컬러 변형 비교

- md의 "변형 (Variant)" 섹션에 명시된 컬러 토큰 (예: Primary 배경 = `color/primary/default`)이 Figma variant의 fills / strokes boundVariables와 일치하는지 확인한다.

#### 상태 비교

- md "상태 (State)" 섹션의 모든 상태 (Default / Hover / Focus / Active / Disabled / Selected 등)가 Figma에 variant로 존재하는지 확인한다.
- 각 상태별 시각 차이 (예: Hover 배경 변화, Disabled opacity 0.4)가 md 정의대로 적용되어 있는지 확인한다.

### 3. 결과 분류

| 분류 | 의미 | 처리 |
|---|---|---|
| **PASS** | md ↔ Figma 일치 | 통과 보고 |
| **MISMATCH (auto-fixable)** | 명확한 1:1 매핑 불일치 (예: width=24인데 boundVariables 비어있음 → `size/S`로 바인딩) | 자동 수정 |
| **MISMATCH (report-only)** | 모호하거나 사양 변경 검토 필요 (예: Figma에 md에 없는 variant 존재) | 보고만 |
| **MISSING (md → Figma)** | md에 정의된 변형이 Figma에 없음 | 보고만 (사용자 확인 후 추가) |
| **MISSING (Figma → md)** | Figma에 있는데 md에 정의 없음 | 보고만 (md 보강 또는 Figma 제거 검토) |

---

## 자동 수정 vs 보고만 정책

본 정합성 검증은 [`.claude/skills/figma-ds-audit/SKILL.md`](../.claude/skills/figma-ds-audit/SKILL.md)에서 실행된다. 자동 수정 정책은 다음을 따른다.

### 자동 수정 가능 (skill §A)

- 토큰 1:1 매핑이 명확한 경우 (Size 5종, Radius 6종 등 [04-token-binding.md](04-token-binding.md) Semantic 토큰과 정확히 일치하는 값)
- 네이밍 규칙 위반 (T-Shirt 소문자 → 대문자 등)
- 페이지 좌표·헤더 스펙 불일치

### 보고만 (skill §B)

- 변형 누락 (md ↔ Figma 어느 쪽이든) — 어느 쪽이 맞는지 판단 필요
- 모호한 토큰 매핑 (예: padding=10px인데 라이브러리에 8과 12만 있음 → 신설 후보 또는 매핑 후보 제시)
- 컬러 변형 불일치 — 자동 변경 시 의도와 다를 위험
- Sizing 모드 (HUG/FILL/FIXED) 불일치 — 부모 레이아웃 영향

---

## 누락 토큰 발견 시

검증 중 md에 정의된 값이 Figma 라이브러리에 토큰으로 존재하지 않으면, [04-token-binding.md#토큰-부재-시-신설-의무](04-token-binding.md#토큰-부재-시-신설-의무) 절차에 따라 토큰을 먼저 신설하고 바인딩한다.

---

## 정합성 점검 트리거

| 시점 | 점검 범위 |
|---|---|
| 컴포넌트 md 수정 직후 | 해당 컴포넌트 페이지 |
| Figma 컴포넌트 수정 직후 | 해당 컴포넌트 페이지 |
| 가이드(`figma-design-system-guide/`) 수정 직후 | 영향받는 컴포넌트 전체 |
| 정기 (월 1회 권장) | 전체 38개 컴포넌트 |

자동 점검은 [`figma-ds-audit` skill](../.claude/skills/figma-ds-audit/SKILL.md)을 호출한다.
