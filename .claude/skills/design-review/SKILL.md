---
name: design-review
description: Vetching Figma 디자인 시스템 가이드(figma-design-system-guide) 준수 여부를 검토하고, 안전한 위반은 즉시 자동 수정·모호한 위반은 보고만 한다. 트리거 — 사용자가 /design-review를 호출하거나, "이거 DS 규칙 맞아?" 같은 디자인 시스템 준수 여부 질문, 또는 Claude가 직전에 mcp__figma__use_figma 같은 Figma 쓰기 도구로 Figma 노드를 수정한 직후.
---

# Vetching Design System Review

현재 Figma 노드/페이지가 Vetching 디자인 시스템 규칙을 따르는지 검토한다.

## 0. 규칙 소스 (Single Source of Truth)

검토 전 반드시 아래 가이드를 다시 읽어 최신 룰을 확인한다 (캐시된 룰 신뢰 금지).

**경로는 본 SKILL.md 파일 기준 상대 경로.** (SKILL.md 위치: `design-system/.claude/skills/design-review/SKILL.md`)

- `../../../figma-design-system-guide/01-page-structure.md` — 페이지 네이밍, Change Log 양식, 메타 박스 금지
- `../../../figma-design-system-guide/02-frame-and-layout.md` — 카드 프레임 스펙, 페이지 좌표, 변형 그리드 계층
- `../../../figma-design-system-guide/03-component-authoring.md` — HUG/FILL/FIXED, Variants 구성·네이밍, T-Shirt 표기
- `../../../figma-design-system-guide/04-token-binding.md` — Size/Spacing/Radius/Color/Text Style 바인딩
- `../../../figma-design-system-guide/05-doc-conventions.md` — 국문 작성, 아이콘 사용 공통
- `../../../figma-design-system-guide/06-figma-mcp-snippets.md` — 자동화 스크립트
- 컴포넌트별 세부 사양: `../../../components/{NN}-{name}.md`
- 파운데이션 토큰 정의: `../../../foundations/`

## 1. 검토 범위 결정

호출 컨텍스트에 따라 범위를 정한다:

| 컨텍스트 | 범위 |
|---|---|
| `/design-review`만 입력 | Figma 현재 선택된 노드 (없으면 사용자에게 1회 확인) |
| `/design-review all` | 현재 열린 페이지 전체 |
| Claude가 직전 turn에 `use_figma`로 수정 | 수정한 노드들만 |
| 사용자가 특정 컴포넌트 명시 (예: "Button 검토해") | 해당 컴포넌트 페이지 |

## 2. Figma 노드 정보 읽기

- `mcp__figma__get_metadata` — 노드 raw 구조(좌표, 사이즈, layoutMode, boundVariables, fills, effects, cornerRadius). **좌표/패딩/토큰 바인딩 검증의 1차 소스**
- `mcp__figma__get_design_context` — 보조용(스크린샷, 코드 매핑)
- 변형 그리드 검증은 항상 `get_metadata` 우선

## 3. 룰 매칭 체크리스트

각 위반은 **(A) 안전 자동 수정** 또는 **(B) 보고만**으로 분류한다.

### A. 안전 자동 수정 (use_figma로 즉시 패치)

**A1. 페이지 네이밍** — `01-page-structure.md`
- 섹션 구분자 → `[ FOUNDATIONS ]`, `[ COMPONENTS ]` (대문자, 대괄호 양 옆 공백)
- 컴포넌트/파운데이션 페이지 → `{NN} — {Title Case}` (em dash `—`, 두 자리 zero-pad)
- 하이픈 `-` → em dash `—`, 소문자 → Title Case, `01-button` → `01 — Button`

**A2. 카드 프레임 스펙** — `02-frame-and-layout.md`
- `fills` ≠ #FFFFFF SOLID → 패치
- `cornerRadius` ≠ 16 → 16
- Drop Shadow 없음/어긋남 → `rgba(26,25,22,0.08), offsetY:4, blur:16`
- 카드 위치 ≠ (0,0) → (0,0)
- 카드 `name` ≠ 페이지명에서 `NN — ` 제거한 값 → 패치

**A3. 페이지 헤더 좌표/폰트**
- 타이틀: (100, 100), Inter Bold 32, #000
- 설명: (100, 144), Inter Medium 15, #000
- (페이지 헤더는 컴포넌트 정의 외부 → Inter 사용 정상)

**A4. 카드 4면 패딩 검증** (`page.loadAsync()` 후)
- `min(child.x) === 100` / `min(child.y) === 100`
- `card.width − max(child.x + child.width) === 100`
- `card.height − max(child.y + child.height) === 100`
- 어긋나면 카드를 콘텐츠에 맞춰 리사이즈

**A5. Variants 네이밍**
- `{이름}/{변형}/{크기}/{상태}` 슬래시 형식
- T-Shirt 사이즈 소문자(`xl, lg, md, sm`) → 대문자(`XL, L, M, S, XS`)
- 슬래시 양옆 공백은 일관되게 (예: `Button / Primary / LG / Default`)

**A6. Component Set Auto Layout**
- Component Set의 `layoutMode === "NONE"` 검증, 아니면 NONE으로

**A7. 메타 라벨/박스 제거** (`[ COMPONENTS ]` 페이지)
- 변형 식별 라벨 텍스트(예: "Primary", "LG / Default") 발견 → 삭제
- 카드 내 별도 "Labels", "Spec", "Meta" 프레임/그룹 → 삭제
- (페이지 헤더, Foundations 토큰 칩 라벨, Change Log entries는 예외 — 유지)

### B. 보고만 (자동 수정 금지)

다음은 추론이 필요해 잘못 매핑하면 손해가 크므로 **수정하지 말고 보고만**한다.

**B1. 토큰 바인딩 누락**
- 텍스트 노드 `textStyleId` 비어있음 + `fontSize`/`fontWeight` 직접 지정 → 가이드 04장 Style×Size 매트릭스 참조해서 **권장 Text Style 후보 제시**
- `cornerRadius` 직접 px (`boundVariables.cornerRadius` 비어있음) → `radius/*` 후보 제시 (4→XS, 6→S, 8→M, 12→L, 16→XL, 9999→FULL)
- `width`/`height` 직접 px → `size/*` 후보 제시 (해당 컴포넌트 md 참조)
- `paddingTop/Right/Bottom/Left`, `itemSpacing` 직접 px → `spacing/{값}` 후보 제시
- `fills`/`strokes` SOLID 하드코딩 (`boundVariables.fills` 비어있음) → `color/*` 후보 제시 (foundations/01-color.md 참조)

**B2. Component Set 통합 필요**
- 같은 페이지에 여러 개별 COMPONENT 노드 + 이름 패턴이 `Name/A`, `Name/B`처럼 변형으로 보이면 → "Combine as Variants 필요" 보고

**B3. 변형 계층 재배치**
- 변형 좌표가 그룹(100)/위계(50)/상태·사이즈(20) 간격과 어긋남 → **권장 좌표만 보고**. 의미적 분류(어느 축이 그룹인지)는 사용자 확인 필요

**B4. 기호 텍스트 → 아이콘 컴포넌트**
- 텍스트 노드에 `✓ ✕ ▶ ◀ ⚠ → ←` 등 기호 발견 → 어떤 아이콘으로 교체할지 추론 불확실 → 노드 위치/내용 보고만

**B5. Change Log 페이지 위반** — `01-page-structure.md`
- Entries Auto Layout 바깥에 단독 텍스트 노드 → "entry 프레임으로 정규화 필요" 보고
- 본문이 마침표(`.`)로 끝나지 않음 → 보고

**B6. Sizing 모드 (HUG/FILL/FIXED)**
- 컴포넌트 md에 명시된 모드와 다름 → 보고. 자동 변경 시 부모 레이아웃이 무너질 수 있으므로 사용자 확인

## 4. 자동 수정 절차

1. A 카테고리 위반을 모두 모은다.
2. 각 위반을 1줄 요약: `[카테고리] 노드ID/이름: 현재값 → 목표값`
3. `mcp__figma__use_figma`로 패치 (가능한 한 1회 호출에 묶음)
4. 수정 후 핵심 값을 `get_metadata`로 1회 재검증
5. **자동 수정은 한 호출당 최대 30건.** 초과 시 첫 30건만 수정하고 나머지는 다음 호출에서 처리하도록 안내

수정 시 절대 좌표(`x, y`)는 의도된 변경이 아니라면 보존 — 의도치 않은 재배치 방지.

## 5. 출력 형식

```
## Design System Review — {대상 노드/페이지 이름}

### 자동 수정됨 (N건)
- [페이지 네이밍] `01-button` → `01 — Button`
- [카드 스펙] cornerRadius 8 → 16
- [T-Shirt 표기] `Button/Primary/lg/Default` → `Button / Primary / L / Default` (3개 variant)
- [메타 라벨 제거] "Primary" 텍스트 노드 1개 삭제

### 수동 확인 필요 (N건)
- [토큰 바인딩] `Button/Primary/L` Height 48px 하드코딩 → `size/L` 바인딩 권장
- [기호 텍스트] `Alert/Warning` 내 ⚠ → `icon/warning` 인스턴스 교체 권장
- [변형 계층] `Button` 사이즈 간 간격 30px → 20px 권장

### 통과 (N건)
- 카드 프레임 패딩 100px ✓
- Component Set Auto Layout NONE ✓
- 페이지 헤더 좌표 ✓
```

## 6. 주의사항

- **검출이 불확실하면 수정하지 말고 보고만 한다.** 잘못된 자동 수정이 가장 큰 손해.
- 가이드 MD가 업데이트되었을 수 있으니 검토 시점마다 0절의 파일들을 다시 읽는다.
- 한 컴포넌트의 사이즈/상태 매핑이 모호하면 해당 `components/{NN}-{name}.md`를 직접 읽어 확인한다.
- 자동 수정 후 사용자가 "되돌려달라"고 요청할 가능성을 염두에 두고, 수정 전 값을 보고에 포함한다.
