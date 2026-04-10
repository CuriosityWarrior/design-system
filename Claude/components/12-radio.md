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

---

## 라벨 텍스트 토글

- Boolean 프로퍼티 `showLabel`로 라벨 텍스트를 켜고 끌 수 있다.
- `showLabel = true`: 라디오 인디케이터 + 라벨 텍스트 표시
- `showLabel = false`: 라디오 인디케이터만 표시

---

## 디자인 토큰

| 토큰 | 값 |
|---|---|
| 보더 반경 | 50% (원형) |
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
