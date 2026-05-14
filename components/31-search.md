# 컴포넌트: 검색 (Search)

## 개요
사용자가 키워드를 입력해 콘텐츠를 빠르게 찾을 수 있는 검색 전용 입력 컴포넌트. 일반 Input과 분리하여 검색 고유의 UX(프리픽스 아이콘, 클리어 버튼, 최근/제안 리스트, 단축키 힌트)를 포함한다.

---

## 디자인 토큰

| 토큰 | 값 |
|---|---|
| 폰트 | 14px / Regular 400 → `text/body-SM` |
| 배경 | `color/surface/2` |
| 보더 | 1px solid `color/border/default` |
| 보더 반경 | `radius/input` = 8px |
| 패딩 (좌·우) | `spacing/12` (12px) (아이콘 포함 시 좌측 `size/XL` (36px)) |
| 포커스 링 | `shadow/focus` = 0 0 0 3px rgba(242,106,0,0.20) |
| 플레이스홀더 | `color/text/tertiary` |
| 모션 | 100ms ease-out |

---

## 크기 (Size)

> 📐 Height는 [파운데이션: 사이즈](../foundations/07-size.md)의 Semantic 토큰을 참조한다. Width는 배치 컨텍스트에 따라 FILL 또는 HUG.

| 크기 | Height 토큰 | Height | 폰트 |
|---|---|---|---|
| Large (L) | `size/input/L` → `size/XL` | 48px | 16px |
| Medium (M) | `size/input/M` → `size/L` | 40px | 14px |
| Small (S) | `size/input/S` → `size/S` | 24px | 13px |

---

## 변형 (Variant)

### Search Bar (기본)
- 단일 행 인풋 형태. 프리픽스 검색 아이콘 + 플레이스홀더 + (입력 시) 클리어 버튼
- 헤더, 페이지 상단, 리스트 필터 상단에 배치

### Search Bar with Shortcut
- 우측에 `⌘K` 또는 `Ctrl K` 키 힌트 표시 (Label 컴포넌트 또는 `color/surface/3` 배경 + Border 처리)
- 글로벌 검색 진입용

### Search Field in Modal (검색 뷰)
- 모달 상단에 검색 인풋 + 하단에 최근 검색 / 제안 결과 리스트
- ESC로 닫기, Enter로 검색 확정

---

## 구성 요소
- **Prefix Icon**: `01 — Icons` 페이지의 `search` 아이콘 인스턴스
- **Placeholder**: "검색…" 또는 구체적 힌트 ("사용자, 문서 검색")
- **Clear Button**: 입력값이 있을 때만 노출. `01 — Icons` 페이지의 `close` 아이콘 인스턴스
- **Shortcut Hint** (옵션): 우측, `color/text/tertiary`, Label 스타일

---

## 상태 (State)

| 상태 | 보더 | 그림자 | 배경 |
|---|---|---|---|
| 기본 | `color/border/default` | — | `color/surface/2` |
| 호버 | `color/border/strong` | — | `color/surface/2` |
| 포커스 | `color/primary/default` | `shadow/focus` | `color/surface/1` |
| 입력 중 | `color/primary/default` | `shadow/focus` | `color/surface/1` |
| 비활성 | `color/border/subtle` | — | `color/surface/2` |

---

## 사이즈 동작

| 속성 | 값 |
|---|---|
| layoutSizingHorizontal | `FILL` 또는 `HUG` (배치 컨텍스트) |
| layoutSizingVertical | `HUG` |

> Height는 Size 토큰(`size/input/*`) 기준 콘텐츠 + 패딩으로 자동 결정된다. 임의 px 값으로 Height Fixed 지정 금지.

---

## 접근성
- `role="search"` + `<input type="search">` 사용
- `aria-label="검색"` 필수
- 클리어 버튼은 별도 `aria-label="검색어 지우기"`
- 단축키 힌트는 `aria-hidden="true"`

---

### Variants 구성
- 모든 변형은 Figma의 **Combine as Variants** 기능을 사용하여 하나의 Component Set으로 통합한다.

---

### 아이콘 사용 규칙
- 프리픽스 검색 아이콘(`search`)과 클리어 버튼 아이콘(`close`)은 반드시 `01 — Icons` 페이지에 정의된 아이콘 컴포넌트 인스턴스를 사용한다.
- 유니코드 문자, 특수 기호 텍스트(🔍, ✕ 등)로 아이콘을 대체하는 것을 금지한다.
- 아이콘 크기는 컴포넌트의 사이즈 변형에 맞춰 조정한다.

---

---

## 사용 원칙

| 원칙 | 설명 |
|---|---|
| 일반 Input과 분리 | Search는 검색 전용 UX(검색 아이콘, 클리어 버튼, 단축키 힌트)를 포함하므로 일반 텍스트 입력에는 Input 컴포넌트를 사용한다. |
| 검색 아이콘 항상 포함 | 사용자가 해당 입력 필드가 검색용임을 즉시 인지할 수 있도록 프리픽스 검색 아이콘을 항상 포함한다. |
| 클리어 버튼 입력 시 노출 | 검색어가 입력된 경우에만 클리어 버튼을 노출한다. 빈 상태에서는 클리어 버튼을 숨겨 불필요한 혼란을 방지한다. |
| 글로벌 검색엔 단축키 힌트 제공 | 앱 전체를 검색하는 글로벌 검색 진입점에는 ⌘K 단축키 힌트를 함께 표시하여 키보드 사용자의 접근성을 높인다. |
| 결과 없음 상태 처리 | 검색 결과가 없을 때 빈 화면 대신 Data Case의 No Results 변형을 표시하여 사용자에게 명확한 피드백을 제공한다. |

## Figma Make 프롬프트

```
다음 스펙으로 검색(Search) 컴포넌트를 만들어줘:

변형: Search Bar, Search Bar with Shortcut, Search Field in Modal
크기: Large (48px), Medium (40px), Small (24px)
Height에는 Size/Semantic Variables (size/input/L, M, S)를 바인딩

기본 구조:
- 좌측: search 아이콘 (Icons 페이지 인스턴스 사용, 텍스트 기호 금지)
- 중앙: 플레이스홀더/입력 텍스트 (14px Regular)
- 우측(옵션): 입력값 있을 때 close 아이콘 버튼 (Icons 페이지 인스턴스)
- 우측(옵션): ⌘K 단축키 힌트 (Label 스타일)

스타일:
- 배경: 연한 서피스, 보더 1px
- 보더 반경: 8px
- 포커스: 오렌지 보더 + 3px 오렌지 링

네이밍: Search / {변형} / {크기} / {상태}
```
