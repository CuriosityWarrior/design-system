# 컴포넌트: 페이지네이션 (Pagination)

## 개요
콘텐츠 페이지 간 이동을 위한 네비게이션.

---

## 디자인 토큰

| 토큰 | 값 |
|---|---|
| 버튼 크기 | `size/icon-button/md` → `size/md` = 32 × 32px |
| 보더 반경 | `radius/button` = 8px |
| 보더 | 1px solid `color/border/default` |
| 배경 | `color/surface/1` |
| 활성 배경 | `color/primary/default` |
| 활성 텍스트 | `color/primary/on-primary` |
| 폰트 | 13px / Medium |
| 간격 | 버튼 사이 `spacing/4` (4px) |
| 모션 | `motion/hover` = 100ms |

---

> 📐 버튼 크기는 [파운데이션: 사이즈](../foundations/07-size.md)의 `size/icon-button/md`(32px) Semantic 토큰을 참조한다.

## 요소
- 이전 버튼: `chevron_left` 아이콘 인스턴스 (`01 — Icons`) — 첫 번째 페이지에서 비활성
- 페이지 번호 버튼: 클릭 가능
- 활성 페이지: Primary 색상 배경
- 말줄임표: `more_horiz` 아이콘 인스턴스 (`01 — Icons`) — 건너뛴 페이지 표시
- 다음 버튼: `chevron_right` 아이콘 인스턴스 (`01 — Icons`) — 마지막 페이지에서 비활성

---

## 정보 포함 패턴
- 전체 개수 텍스트: 좌측 정렬 ("전체 128개 중 21–30번째")
- 페이지네이션: 우측 정렬
- 플렉스 행, space-between

---

## 사이즈 동작

| 속성 | 값 |
|---|---|
| layoutSizingHorizontal | `HUG` |
| layoutSizingVertical | `HUG` |

> 페이지 아이템들 + 이전/다음 버튼 기준으로 자동 조정. 임의 px 값으로 Fixed 지정 금지.

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
| 대용량 데이터에 사용 | 항목이 많아 한 화면에 표시하기 어려울 때 Pagination을 사용한다. 항목이 적으면 모두 표시하거나 "더 보기" 버튼을 사용한다. |
| 현재 위치 명확히 표시 | 활성 페이지 번호를 항상 Primary 색상으로 강조하여 사용자가 현재 위치를 즉시 파악할 수 있도록 한다. |
| 경계 상태 처리 | 첫 페이지에서 이전 버튼, 마지막 페이지에서 다음 버튼을 비활성화한다. 클릭해도 반응하지 않는 상태가 아닌 명확히 비활성(disabled)으로 표시한다. |
| 전체 개수 정보 제공 | 가능하면 전체 항목 수와 현재 보고 있는 범위를 함께 표시하여 사용자가 콘텐츠 규모를 파악할 수 있도록 한다. |
| 인피니트 스크롤과 혼용 금지 | 동일 목록에서 Pagination과 인피니트 스크롤을 함께 사용하지 않는다. 하나의 탐색 패러다임을 일관되게 적용한다. |

## Figma Make 프롬프트

```
다음 스펙으로 페이지네이션(Pagination) 컴포넌트를 만들어줘:

버튼: 32×32px 정사각형 (size/icon-button/md), 보더 반경 8px, 1px 회색 보더
폰트: 13px Medium

상태:
- 기본: 흰색 배경, 회색 보더
- 호버: 진한 보더, 진한 텍스트
- 활성: 오렌지 배경 (#F26A00), 흰색 텍스트
- 비활성: 40% 불투명도 (이전/다음 화살표)

요소: chevron_left 이전, 페이지 번호, more_horiz 말줄임표, 다음 chevron_right (모두 01 — Icons 인스턴스)

정보 포함 변형:
- "전체 128개 중 21–30번째" 텍스트 좌측
- 페이지네이션 우측

네이밍: Pagination / Default, Pagination / With Info
```
