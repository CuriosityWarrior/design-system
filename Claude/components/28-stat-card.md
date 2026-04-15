# 컴포넌트: 스탯 카드 (Stat Card)

## 개요
레이블과 트렌드 인디케이터가 포함된 핵심 지표 표시 카드.

---

## 디자인 토큰

| 토큰 | 값 |
|---|---|
| 배경 | `color/surface/1` |
| 보더 | 1px solid `color/border/default` |
| 보더 반경 | `radius/card` = 12px |
| 패딩 | `spacing/18` (18px) `spacing/20` (20px) |
| 레이블 폰트 | 12px / Medium 500, `color/text/tertiary`, 대문자 |
| 값 폰트 | 28px / Bold 700, 자간 -0.02em |
| 변화 폰트 | 12px / Regular |

---

> 📐 사이즈 기본 원칙은 [파운데이션: 사이즈](../foundations/07-size.md) 참조. 보더는 `size/border/thin`(1px) 적용.

## 구조
1. **레이블**: 12px Medium 대문자, `color/text/tertiary`
   - 하단 여백: `spacing/8` (8px)
2. **값**: 28px Bold, `color/text/primary`
   - 하단 여백: `spacing/6` (6px)
3. **변화 인디케이터**: 트렌드 화살표 + 퍼센트 텍스트
   - 증가: `trending_up` 아이콘 인스턴스 (`01 — Icons`) + `color/success/text` 텍스트
   - 감소: `trending_down` 아이콘 인스턴스 (`01 — Icons`) + `color/error/text` 텍스트
   - 중립: `trending_flat` 아이콘 인스턴스 (`01 — Icons`) + `color/text/tertiary` 텍스트

---

## 그리드 레이아웃
- 일반적으로 2~4열 그리드에서 사용
- 각 카드: 최소 너비 180px

---

## 사이즈 동작

| 속성 | 값 |
|---|---|
| layoutSizingHorizontal | `FILL` 또는 `HUG` |
| layoutSizingVertical | `HUG` |

> Height는 레이블 + 값 + 트렌드 인디케이터 + 패딩 기준으로 자동 조정된다. 대시보드 그리드에서 높이 정렬이 필요하면 부모 그리드에서 `FILL`로 동기화. 임의 px 값으로 Fixed 지정 금지.

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
| 핵심 지표만 표시 | Stat Card 하나에 하나의 핵심 지표만 표시한다. 여러 수치를 한 카드에 나열하면 시각적 계층이 무너진다. |
| 트렌드 방향 의미 준수 | 증가가 긍정적이면 초록(성공), 부정적이면 빨간(오류) 트렌드 색상을 사용한다. 맥락에 따라 색상의 의미가 달라질 수 있으므로 레이블로 보완한다. |
| 그리드 레이아웃 적용 | Stat Card는 2~4열 그리드로 배치하여 지표를 나란히 비교할 수 있도록 한다. 단독으로 사용하지 않는다. |
| 값 형식 일관성 | 같은 대시보드 내 Stat Card들의 숫자 형식(단위, 소수점, 천 단위 구분자)을 일관되게 유지한다. |
| 레이블 대문자 사용 | 레이블 텍스트는 항상 대문자(uppercase)로 표시하여 주요 값과 시각적으로 구분한다. |

## Figma Make 프롬프트

```
다음 스펙으로 스탯 카드/KPI 카드(Stat Card) 컴포넌트를 만들어줘:

배경: 흰색 / 다크 서피스
보더: 1px 연한 회색, 보더 반경 12px
패딩: 18px 20px

콘텐츠:
1. 레이블: 12px Medium 대문자 회색 텍스트 (예: "총 사용자")
2. 값: 28px Bold 대형 숫자 (예: "12,482")
3. 변화: 트렌드 화살표가 있는 소형 텍스트
   - trending_up 아이콘 인스턴스(01 — Icons) + 초록 텍스트 증가 (예: "trending_up 12.5% 지난 달 대비")
   - trending_down 아이콘 인스턴스(01 — Icons) + 빨간 텍스트 감소
   - trending_flat 아이콘 인스턴스(01 — Icons) + 회색 텍스트 중립

그리드: 4개 카드로 구성된 4열 레이아웃 예시

네이밍: Stat Card / Positive, Stat Card / Negative, Stat Card / Neutral
```
