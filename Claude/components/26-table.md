# 컴포넌트: 테이블 (Table)

## 개요
행과 열로 구성된 구조적 데이터 표시. 정렬, 선택, 밀도 옵션 지원.

---

## 디자인 토큰

| 토큰 | 값 |
|---|---|
| 헤더 폰트 | 12px / Medium 500, `color/text/tertiary`, 대문자 |
| 헤더 배경 | `color/surface/2` |
| 헤더 보더 | 1px solid `color/border/default` |
| 셀 폰트 | 14px / Regular, `color/text/primary` |
| 셀 패딩 (기본) | `spacing/10` (10px) `spacing/12` (12px) |
| 셀 패딩 (컴팩트) | `spacing/6` (6px) `spacing/12` (12px) |
| 행 보더 | 1px solid `color/border/subtle` |
| 행 호버 | `color/surface/2` |
| 보더 반경 (컨테이너) | `radius/M` (8px) |
| 행 선택됨 | `color/primary/subtle` |

---

> 📐 사이즈 기본 원칙은 [파운데이션: 사이즈](../foundations/07-size.md) 참조. 보더는 `size/border/thin`(1px), 내부 체크박스/뱃지/아이콘 버튼은 해당 컴포넌트의 Semantic 토큰을 따른다.

## 기능

### 정렬
- 컬럼 헤더: 클릭 가능
- 정렬 표시: `arrow_upward` 아이콘 인스턴스 (오름차순) / `arrow_downward` 아이콘 인스턴스 (내림차순) (`01 — Icons`) 헤더 텍스트 뒤에 추가
- 기본: 표시 없음

### 행 선택
- 좌측에 체크박스 컬럼 (40px 너비)
- 전체 선택: 헤더 체크박스
- 선택된 행: `color/primary/subtle` 배경

### 밀도
- 기본: `spacing/10` (10px) `spacing/12` (12px) 셀 패딩
- 컴팩트: `spacing/6` (6px) `spacing/12` (12px) 셀 패딩

---

## 셀 종류
- **텍스트 셀**: 표준 텍스트
- **이름 셀**: 굵은 이름 + 아래 회색 부제 (12px)
- **날짜 셀**: 13px / Regular, `color/text/secondary`
- **뱃지 셀**: 상태 뱃지 컴포넌트
- **액션 셀**: 아이콘 버튼 (편집, 삭제 등)

---

## 사이즈 동작

| 속성 | 값 |
|---|---|
| layoutSizingHorizontal | `FILL` (부모 너비) |
| layoutSizingVertical | `HUG` |

> 행 수에 따라 Height 자동 조정. 각 행의 Height도 HUG(콘텐츠 + 패딩). 임의 px 값으로 Fixed 지정 금지.

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
| 비교가 필요한 데이터에 사용 | Table은 여러 항목의 속성을 비교해야 할 때 사용한다. 단순 목록에는 List Item 패턴이 더 적합하다. |
| 밀도 상황에 맞게 선택 | 정보량이 많아 공간이 부족하면 Compact 변형을 사용한다. 가독성이 중요하거나 입력/편집이 있는 테이블에는 기본 밀도를 유지한다. |
| 컬럼 수 최적화 | 테이블에 너무 많은 컬럼을 나열하지 않는다. 중요도가 낮은 컬럼은 숨기거나 상세 보기로 이동시킨다. |
| 정렬 가능한 컬럼 명확히 표시 | 정렬이 가능한 컬럼은 헤더에 정렬 아이콘을 통해 명확히 표시한다. 정렬이 불가능한 컬럼과 시각적으로 구분한다. |
| 빈 상태 처리 | 데이터가 없을 때 빈 테이블 행을 나열하지 않고 Data Case 컴포넌트의 Empty 또는 No Results 변형을 사용한다. |

## Figma Make 프롬프트

```
다음 스펙으로 데이터 테이블(Table) 컴포넌트를 만들어줘:

헤더 행:
- 12px Medium 대문자 회색 텍스트
- 행보다 약간 어두운 배경
- 정렬 가능한 컬럼 (arrow_upward / arrow_downward 아이콘 인스턴스, 01 — Icons)
- 선택 전체 체크박스 (선택적)

데이터 행:
- 14px Regular 텍스트
- 행 사이 미세한 하단 보더
- 호버: 연한 회색 배경
- 선택됨: 연한 오렌지 배경

셀 종류:
- 텍스트, 이름+부제, 날짜, 상태 뱃지, 액션 버튼

밀도: 기본 (넓게) 및 컴팩트 변형

네이밍: Table / Default, Table / Compact
```
