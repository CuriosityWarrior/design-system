# 컴포넌트: 브레드크럼 (Breadcrumb)

## 개요
계층 구조 내 현재 페이지 위치를 보여주는 네비게이션 보조 도구.

---

## 디자인 토큰

| 토큰 | 값 |
|---|---|
| 폰트 | 13px / Regular |
| 링크 색상 | `color/text/tertiary` |
| 현재 페이지 색상 | `color/text/primary` / Medium 500 |
| 호버 색상 | `color/text/primary` |
| 구분자 | `/` 또는 `›`, `color/text/tertiary` |
| 구분자 패딩 | 0 2px |
| 항목 패딩 | 2px 4px |
| 보더 반경 | `radius/XS` (4px) (호버 배경) |
| 모션 | `motion/hover` = 100ms |

> 이 컴포넌트는 텍스트 기반 내비게이션으로, Radius 토큰을 적용하지 않는다. 호버 배경의 보더 반경(4px)은 `spacing/4` 값을 사용한다.

---

> 📐 사이즈 기본 원칙은 [파운데이션: 사이즈](../foundations/07-size.md) 참조.

### Size/Spacing 토큰 바인딩

| 속성 | 토큰 | 값 |
|---|---|---|
| 항목 간 간격 (gap) | `spacing/2` | 2px |
| 구분자 좌우 패딩 | `spacing/2` | 2px |
| 항목 내부 패딩 상하 | `spacing/2` | 2px |
| 항목 내부 패딩 좌우 | `spacing/4` | 4px |
| 호버 배경 보더 반경 | `spacing/4` | 4px |

> Figma에서 해당 속성에 Variables를 직접 바인딩한다. 임의 px 고정값 사용 금지.

---

## 구조
- 플렉스 행, 줄 바꿈 허용, 간격 2px
- 각 항목: 클릭 가능한 링크 (마지막 항목 제외)
- 항목 사이에 구분자
- 마지막 항목: 현재 페이지 — 클릭 불가, Primary 텍스트, Medium 굵기

---

## 사이즈 동작

| 속성 | 값 |
|---|---|
| layoutSizingHorizontal | `HUG` |
| layoutSizingVertical | `HUG` |

> 콘텐츠(경로 텍스트 + 구분자) 기반으로 가로·세로 자동 조정. 임의 px 값으로 Fixed 지정 금지.

---

## 아이콘 사용 규칙

> 컴포넌트 내 아이콘은 반드시 `01 — Icons` 페이지의 아이콘 컴포넌트 인스턴스를 사용한다.
> 텍스트 특수 문자(✓, ✕, →, ⋯ 등), 이모지, 직접 그린 벡터 도형으로 아이콘을 대체하는 것을 금지한다.
> 필요한 아이콘이 없는 경우, 먼저 `01 — Icons` 페이지에 추가한 후 인스턴스를 참조한다.

---

### Variants 구성
- 모든 변형은 Figma의 **Combine as Variants** 기능을 사용하여 하나의 Component Set으로 통합한다.

---

---

## 토큰 바인딩 체크리스트

본 컴포넌트의 Figma 구현 시 다음을 모두 충족해야 한다 ([`04-token-binding.md#토큰-바인딩-검증-의무`](../figma-design-system-guide/04-token-binding.md#토큰-바인딩-검증-의무) 참조).

| 속성 종류 | 바인딩 대상 | 검증 |
|---|---|---|
| Width / Height | `size/*` Variables (또는 부모 Auto Layout에 의해 결정) | `boundVariables.width` / `boundVariables.height` |
| Padding 4면 / itemSpacing | `spacing/*` Variables | `boundVariables.padding{Top|Right|Bottom|Left}` / `boundVariables.itemSpacing` |
| cornerRadius | `radius/*` Variables | `boundVariables.cornerRadius` (또는 4모서리별) |
| fills / strokes (SOLID 컬러) | `color/*` Variables | `boundVariables.fills` / `strokes` 또는 `fillStyleId` / `strokeStyleId` |
| 텍스트 노드 | Text Style (Pretendard) | `textStyleId !== ""` |
| 그림자 (effects) | Effect Style | `effectStyleId !== ""` |

위 "디자인 토큰" / "크기" 섹션에 명시된 값은 모두 위 토큰에 바인딩되어야 한다. 임의 px·HEX 값으로 남아있으면 위반이다.

**라이브러리에 없는 값**이 필요한 경우 [`04-token-binding.md#토큰-부재-시-신설-의무`](../figma-design-system-guide/04-token-binding.md#토큰-부재-시-신설-의무)에 따라 먼저 토큰을 신설한 후 바인딩한다.

---

## 사용 원칙

| 원칙 | 설명 |
|---|---|
| 계층 구조가 있는 곳에만 사용 | Breadcrumb는 2단계 이상의 명확한 계층 구조가 있는 페이지에서만 사용한다. 단일 레벨 또는 선형 플로우에는 Back 버튼을 사용한다. |
| 현재 페이지 클릭 불가 | 마지막 항목(현재 페이지)은 항상 클릭 불가 상태로 표시하여 이미 해당 위치에 있음을 명확히 한다. |
| 계층 전체 표시 | 루트부터 현재 페이지까지 모든 계층을 표시한다. 모바일 등 공간이 부족한 경우 중간 계층을 생략할 수 있으나 루트와 현재 페이지는 항상 표시한다. |
| 페이지 제목과 중복 지양 | Breadcrumb의 현재 페이지 항목이 페이지 제목(H1)과 완전히 동일하면 Breadcrumb에서 현재 페이지를 생략하거나 페이지 제목으로 통합한다. |
| 구분자 일관성 | 한 서비스 내에서 구분자(/ 또는 ›)를 일관되게 사용한다. 혼용하지 않는다. |

## Figma Make 프롬프트

```
다음 스펙으로 브레드크럼(Breadcrumb) 네비게이션 컴포넌트를 만들어줘:

항목: "/" 또는 "›"로 구분된 클릭 가능한 링크 (13px 회색)
현재 페이지: 마지막 항목, 어두운 텍스트 (13px Medium), 클릭 불가
호버: 약간 어두워지는 텍스트 색상

예시: 홈 / 프로젝트 / 디자인 시스템 / **컴포넌트**

플렉스 행 레이아웃, 소형 화면에서 줄 바꿈

네이밍: Breadcrumb / Default
```
