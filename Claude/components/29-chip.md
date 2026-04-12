# 컴포넌트: 칩 / 필터 (Chip)

## 개요
콘텐츠 필터링 또는 다중 선택 시나리오를 위한 간결한 인터랙티브 레이블.

---

## 디자인 토큰

| 토큰 | 값 |
|---|---|
| 폰트 | 13px / Medium 500 |
| 보더 반경 | `radius/badge` = 9999px (필 형태) |
| 보더 | 1px solid `color/border/default` |
| 배경 (기본) | `color/surface/1` |
| 배경 (활성) | `color/primary/subtle` |
| 보더 (활성) | `color/primary/default` |
| 텍스트 (기본) | `color/text/secondary` |
| 텍스트 (활성) | `color/primary/default` |
| 패딩 | 6px 12px |
| 모션 | `motion/hover` = 100ms |

---

> 📐 사이즈 기본 원칙은 [파운데이션: 사이즈](../foundations/07-size.md) 참조. 칩은 텍스트+패딩 기반으로 Height가 결정되므로 Semantic 토큰 미적용. 보더는 `size/border/thin`(1px).

## 상태

| 상태 | 배경 | 보더 | 텍스트 |
|---|---|---|---|
| 기본 | `color/surface/1` | `color/border/default` | `color/text/secondary` |
| 호버 | `color/surface/1` | `color/border/strong` | `color/text/primary` |
| 활성/선택됨 | `color/primary/subtle` | `color/primary/default` | `color/primary/default` |
| 비활성 | `color/surface/2` | `color/border/subtle` | `color/text/disabled` |

---

## 점 인디케이터 포함
- 좌측에 6px 원형
- 색상이 필터 카테고리 또는 변형에 맞음

---

## 사용 패턴
- **단일 선택**: 한 번에 하나의 칩만 활성 (탭 유사 동작)
- **다중 선택**: 여러 칩 동시 활성 가능

---

## 사이즈 동작

| 속성 | 값 |
|---|---|
| layoutSizingHorizontal | `HUG` |
| layoutSizingVertical | `HUG` |

> 텍스트(+아이콘) + 패딩 기준으로 가로·세로 자동 조정. 임의 px 값으로 Fixed 지정 금지.

---

## 아이콘 사용 규칙

> 컴포넌트 내 아이콘은 반드시 `01 — Icons` 페이지의 아이콘 컴포넌트 인스턴스를 사용한다.
> 텍스트 특수 문자(✓, ✕, →, ⋯ 등), 이모지, 직접 그린 벡터 도형으로 아이콘을 대체하는 것을 금지한다.
> 필요한 아이콘이 없는 경우, 먼저 `01 — Icons` 페이지에 추가한 후 인스턴스를 참조한다.

---

## Figma Make 프롬프트

```
다음 스펙으로 칩/필터 태그(Chip) 컴포넌트를 만들어줘:

형태: 필 (전체 보더 반경)
폰트: 13px Medium
패딩: 6px 12px

상태:
- 기본: 흰색 배경, 회색 보더, 보조 텍스트
- 호버: 약간 진한 보더, 주요 텍스트
- 활성/선택됨: 오렌지 틴트 배경 (#FFF5ED), 오렌지 보더, 오렌지 텍스트
- 비활성: 흐린 상태

선택적: 카테고리 색상 인디케이터를 위한 좌측 6px 점

사용법: 가로 flex-wrap 그룹으로 배열

네이밍: Chip / Default, Chip / Active, Chip / Disabled
```
