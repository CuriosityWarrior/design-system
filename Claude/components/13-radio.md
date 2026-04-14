# 컴포넌트: 라디오 버튼 (Radio Button)

## 개요
상호 배타적인 옵션 그룹에서 단일 선택.

---

## 레이아웃 규칙

| 항목 | 값 |
|---|---|
| layoutSizingHorizontal | `FIXED` |
| layoutSizingVertical | `FIXED` |

> Radio 인디케이터는 정사각형 고정값으로 설정한다 (Width = Height).

---

## 사이즈 베리언트

> 📐 사이즈 기본 원칙은 [파운데이션: 사이즈](../foundations/07-size.md) 참조. 라디오 전용 Semantic 토큰은 현재 미정의 — Semantic 토큰이 추가되면 참조로 전환한다.
> Checkbox와 동일한 기준으로 XS, S, M, L, XL 5단계를 제공한다.

| 사이즈 | 인디케이터 크기 | 선택됨 점 크기 | 라벨 텍스트 크기 |
|---|---|---|---|
| XS | 12 × 12px | 5px | 11px |
| S | 16 × 16px | 7px | 13px |
| M | 20 × 20px | 8px | 14px |
| L | 24 × 24px | 10px | 16px |
| XL | 28 × 28px | 12px | 18px |

### Size/Spacing 토큰 바인딩

| 속성 | 토큰 | 값 |
|---|---|---|
| 인디케이터 크기 (XS) | `size/12` | 12px |
| 인디케이터 크기 (S) | `size/XS` | 16px |
| 인디케이터 크기 (M) | `size/20` | 20px |
| 인디케이터 크기 (L) | `size/S` | 24px |
| 인디케이터 크기 (XL) | `size/28` | 28px |
| 인디케이터–라벨 간격 | `spacing/10` | 10px |
| 라벨–부설명 간격 | `spacing/2` | 2px |

> Figma에서 해당 속성에 Variables를 직접 바인딩한다. 임의 px 고정값 사용 금지.

---

## 라벨 텍스트 토글

- Boolean 프로퍼티 `showLabel`로 라벨 텍스트를 켜고 끌 수 있다.
- `showLabel = true`: 라디오 인디케이터 + 라벨 텍스트 표시
- `showLabel = false`: 라디오 인디케이터만 표시

---

## 디자인 토큰

| 토큰 | 값 |
|---|---|
| 보더 반경 | `radius/FULL` (9999px — 원형) |
| 보더 | 1.5px solid `color/border/strong` |
| 선택됨 점 | 원형, `color/primary/default` |
| 포커스 링 | `shadow/focus` |
| 모션 | 100ms ease-out |

---

## 상태

| 상태 | 시각 표현 |
|---|---|
| 미선택 | 흰색 배경, 회색 보더 |
| 선택됨 | 흰색 배경, 오렌지 보더, 오렌지 중앙 점 (8px) |
| 비활성 | 흐린 배경, 연한 보더 |
| 호버 | 보더 → `color/primary/default` |
| 포커스 | `shadow/focus` 링 |

---

## 베리언트 구조

네이밍: `Radio/{사이즈}/{상태}`
- 사이즈: XS, S, M, L, XL
- 상태: Default, Selected, Disabled, Disabled Selected

---

## 레이블 포함 패턴
- Checkbox와 동일한 레이블 패턴
- 레이블 텍스트 크기: 사이즈별 상이 (사이즈 베리언트 표 참조)
- 라디오 그룹에는 위에 그룹 레이블 필요 (heading-sm)

---

## 아이콘 사용 규칙

> 컴포넌트 내 아이콘은 반드시 `01 — Icons` 페이지의 아이콘 컴포넌트 인스턴스를 사용한다.
> 텍스트 특수 문자(✓, ✕, →, ⋯ 등), 이모지, 직접 그린 벡터 도형으로 아이콘을 대체하는 것을 금지한다.
> 필요한 아이콘이 없는 경우, 먼저 `01 — Icons` 페이지에 추가한 후 인스턴스를 참조한다.

---

### Variants 구성
- 모든 변형은 Figma의 **Combine as Variants** 기능을 사용하여 하나의 Component Set으로 통합한다.

---

## Figma Make 프롬프트

```
다음 스펙으로 라디오 버튼(Radio Button) 컴포넌트를 만들어줘:

크기: 18×18px 원형 (border-radius 50%)
보더: 1.5px solid 회색

상태:
- 미선택: 흰색 배경, 회색 보더
- 선택됨: 흰색 배경, 오렌지 보더, 오렌지 채워진 점 (8px) 중앙
- 비활성: 흐린 상태, 상호작용 없음
- 호버: 보더 오렌지로 변경

레이블 포함 변형:
- 라디오 + 레이블 텍스트 (14px) 나란히, 10px 간격
- 선택적 부설명 텍스트 (12px 회색) 레이블 아래

포커스: 3px 오렌지 링

네이밍: Radio / {상태}, Radio / With Label / {상태}
```
