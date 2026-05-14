# 컴포넌트: 목록 항목 (List Item)

## 개요
목록의 단일 행. 아이콘, 주요 텍스트, 보조 텍스트, 후행 메타 정보를 결합.

---

## 디자인 토큰

| 토큰 | 값 |
|---|---|
| 패딩 | `spacing/12` (12px) `spacing/16` (16px) |
| 하단 보더 | 1px solid `color/border/subtle` |
| 호버 배경 | `color/surface/2` |
| 모션 | `motion/hover` = 100ms |
| 아이콘 컨테이너 | 36×36px, `radius/button` = 8px, `color/primary/subtle` |
| 제목 폰트 | `text/label-MD` = 14px / Medium |
| 설명 폰트 | 12px / Regular, `color/text/tertiary` |
| 메타 폰트 | 12px / Regular, `color/text/tertiary` |

---

> 📐 사이즈 기본 원칙은 [파운데이션: 사이즈](../foundations/07-size.md) 참조. 아이콘 컨테이너는 `size/icon-button/L`(40px) 또는 `size/icon-button/M`(32px) 적용 가능.

## 구조 (좌측에서 우측)
1. **아이콘 컨테이너** (선택): 36×36px 둥근 정사각형
2. **콘텐츠** (flex-1):
   - 제목: 14px / Medium, `color/text/primary`
   - 설명 (선택): 12px / Regular, `color/text/tertiary`, 제목 아래 `spacing/2` (2px)
3. **메타** (선택): 12px / Regular, `color/text/tertiary`, 우측 정렬

---

## 사이즈 동작

| 속성 | 값 |
|---|---|
| layoutSizingHorizontal | `FILL` (부모 너비) |
| layoutSizingVertical | `HUG` |

> Height는 아이콘/텍스트/메타 콘텐츠 + 패딩 기준으로 자동 조정된다. 임의 px 값으로 Fixed 지정 금지.

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

## 사용 원칙

| 원칙 | 설명 |
|---|---|
| 균일한 항목 나열에 사용 | List Item은 동일한 구조를 반복하는 목록에 사용한다. 항목마다 구조가 크게 다를 경우 Card 패턴을 고려한다. |
| 아이콘 컨테이너 일관성 | 한 목록 내에서 아이콘 유무를 일관되게 유지한다. 일부 항목에만 아이콘을 사용하면 시각적 불균형이 발생한다. |
| 클릭 가능 여부 명확히 | 클릭 가능한 항목은 호버 배경이 표시되어야 하며, 클릭 불가 항목과 시각적으로 구분한다. |
| 메타 정보 간결하게 | 우측 메타 텍스트는 날짜, 수량, 상태 등 핵심 보조 정보만 포함한다. 길이가 길어 주요 텍스트를 가리지 않도록 한다. |
| 항목 간 구분선 | 하단 보더로 항목을 구분하되, 마지막 항목에는 구분선을 생략하거나 컨테이너 보더로 대체한다. |

## Figma Make 프롬프트

```
다음 스펙으로 목록 항목(List Item) 컴포넌트를 만들어줘:

레이아웃: 가로 플렉스, 패딩 12px 16px, 미세한 하단 보더
호버: 연한 회색 배경

좌측: 선택적 36×36px 아이콘 컨테이너 (오렌지 틴트 배경, 8px 반경)
중앙: 제목 (14px Medium) + 선택적 설명 (12px 회색) 아래
우측: 선택적 메타 텍스트 (12px 회색)

모든 요소 세로 중앙 정렬

목록 컨테이너에서 반복 행으로 사용

네이밍: List Item / Default, List Item / With Icon, List Item / With Description
```
