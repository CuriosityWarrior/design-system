# 컴포넌트: 체크박스 (Checkbox)

## 개요
이진 선택 컨트롤. 단독 또는 그룹으로 사용 가능.

---

## 레이아웃 규칙

| 항목 | 값 |
|---|---|
| layoutSizingHorizontal | `FIXED` |
| layoutSizingVertical | `FIXED` |

> 체크박스 인디케이터는 정사각형 고정값으로 설정한다 (Width = Height).

---

## 사이즈 베리언트

> 📐 사이즈 기본 원칙은 [파운데이션: 사이즈](../foundations/07-size.md) 참조. 체크박스 전용 Semantic 토큰은 현재 미정의 — Semantic 토큰이 추가되면 참조로 전환한다.

| 사이즈 | 인디케이터 크기 | 보더 반경 | 체크마크 크기 | 라벨 텍스트 크기 |
|---|---|---|---|---|
| XS | 12 × 12px | `radius/XS` (4px) | 7×4px | 11px |
| S | 16 × 16px | `radius/XS` (4px) | 9×5px | 13px |
| M | 20 × 20px | `radius/S` (6px) | 11×6px | 14px |
| L | 24 × 24px | `radius/S` (6px) | 13×7px | 16px |
| XL | 28 × 28px | `radius/M` (8px) | 15×8px | 18px |

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
- `showLabel = true`: 체크박스 인디케이터 + 라벨 텍스트 표시
- `showLabel = false`: 체크박스 인디케이터만 표시

---

## 디자인 토큰

| 토큰 | 값 |
|---|---|
| 보더 반경 | `radius/XS` (4px) |
| 보더 | 1.5px solid `color/border/strong` |
| 체크됨 배경 | `color/primary/default` |
| 체크됨 보더 | `color/primary/default` |
| 체크마크 | 흰색, -45° 회전 |
| 포커스 링 | `shadow/focus` |
| 모션 | 100ms ease-out |

---

## 상태

| 상태 | 시각 표현 |
|---|---|
| 미선택 | 흰색 배경, 회색 보더 |
| 선택됨 | 오렌지 배경, 오렌지 보더, 흰색 체크마크 |
| 부분 선택 (Indeterminate) | 오렌지 배경, 흰색 가로 선 (8×2px) |
| 비활성 미선택 | 흐린 배경, 연한 보더, 상호작용 없음 |
| 비활성 선택됨 | 흐린 오렌지, 상호작용 없음 |
| 호버 | 보더 → `color/primary/default` |
| 포커스 | `shadow/focus` 링 |

---

## 베리언트 구조

네이밍: `Checkbox/{사이즈}/{상태}`
- 사이즈: XS, S, M, L, XL
- 상태: Default, Checked, Indeterminate, Disabled, Disabled Checked

---

## 레이블 포함 패턴
- 체크박스 좌측 정렬, 레이블 텍스트 우측, 10px 간격
- 레이블 텍스트 크기: 사이즈별 상이 (사이즈 베리언트 표 참조)
- 레이블 폰트: Regular, `color/text/primary`
- 선택적 부설명: 12px / Regular, `color/text/tertiary`, 레이블 아래 2px

---

## 접근성
- 키보드로 포커스 및 스페이스바로 토글 가능
- `aria-checked="mixed"` — 부분 선택 상태

---

## 아이콘 사용 규칙

> 컴포넌트 내 아이콘은 반드시 `01 — Icons` 페이지의 아이콘 컴포넌트 인스턴스를 사용한다.
> 텍스트 특수 문자(✓, ✕, →, ⋯ 등), 이모지, 직접 그린 벡터 도형으로 아이콘을 대체하는 것을 금지한다.
> 필요한 아이콘이 없는 경우, 먼저 `01 — Icons` 페이지에 추가한 후 인스턴스를 참조한다.

---

### Variants 구성
- 모든 변형은 Figma의 **Combine as Variants** 기능을 사용하여 하나의 Component Set으로 통합한다.

---

## 사용 원칙

| 원칙 | 설명 |
|---|---|
| 다중 선택 적합 | 여러 항목을 독립적으로 선택·해제할 수 있는 경우에 사용. 상호 배타적 선택에는 Radio를 사용한다. |
| 부분 선택 처리 | 상위 체크박스가 하위 항목 일부만 선택된 경우 Indeterminate 상태를 적용하고 `aria-checked="mixed"` 를 설정한다. |
| 레이블 필수 | 레이블 없이 인디케이터만 단독 사용하는 경우 `aria-label`을 반드시 제공한다. |
| 크기 일관성 | 한 폼·목록 내에서 체크박스 크기는 통일. Size 토큰으로 지정하고 임의 px 고정 금지. |
| 키보드 접근성 | 스페이스바로 토글, 탭으로 포커스 이동이 가능해야 한다. 포커스 시 `shadow/focus` 링을 표시한다. |
| 아이콘 규칙 | 컴포넌트 내 아이콘은 `01 — Icons` 페이지의 인스턴스만 사용. 텍스트 특수문자·이모지·직접 그린 벡터 금지. |

---

## Figma Make 프롬프트

```
다음 스펙으로 체크박스(Checkbox) 컴포넌트를 만들어줘:

크기: 18×18px 정사각형
보더 반경: 5px
보더: 1.5px solid 회색

상태:
- 미선택: 흰색 배경, 회색 보더
- 선택됨: 오렌지 배경 (#F26A00), 오렌지 보더, 흰색 체크마크 (✓)
- 부분 선택: 오렌지 배경, 흰색 가로 선
- 비활성: 흐린 회색, 상호작용 없음
- 호버: 보더 오렌지로 변경

레이블 포함 변형:
- 체크박스 + 레이블 텍스트 (14px) 나란히, 10px 간격
- 선택적 부설명 텍스트 (12px 회색) 레이블 아래

포커스: 체크박스에 3px 오렌지 링

네이밍: Checkbox / {상태}, Checkbox / With Label / {상태}
```
