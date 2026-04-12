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
| 간격 | 버튼 사이 4px |
| 모션 | `motion/hover` = 100ms |

---

> 📐 버튼 크기는 [파운데이션: 사이즈](../foundations/07-size.md)의 `size/icon-button/md`(32px) Semantic 토큰을 참조한다.

## 요소
- 이전 버튼 (‹): 첫 번째 페이지에서 비활성
- 페이지 번호 버튼: 클릭 가능
- 활성 페이지: Primary 색상 배경
- 말줄임표 (···): 건너뛴 페이지 표시
- 다음 버튼 (›): 마지막 페이지에서 비활성

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

요소: ‹ 이전, 페이지 번호, ··· 말줄임표, 다음 ›

정보 포함 변형:
- "전체 128개 중 21–30번째" 텍스트 좌측
- 페이지네이션 우측

네이밍: Pagination / Default, Pagination / With Info
```
