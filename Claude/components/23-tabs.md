# 컴포넌트: 탭 (Tabs)

## 개요
관련 콘텐츠 섹션 간 전환을 위한 네비게이션 컴포넌트.

---

## 디자인 토큰

| 토큰 | 값 |
|---|---|
| 활성 인디케이터 | 2px solid `color/primary/default` |
| 활성 텍스트 | `color/text/primary` |
| 비활성 텍스트 | `color/text/tertiary` |
| 호버 텍스트 | `color/text/secondary` |
| 폰트 | 14px / Medium 500 |
| 패딩 | 탭당 10px 16px |
| 하단 보더 | 1px solid `color/border/default` |
| 모션 | 150ms ease-out |

> 탭 아이템 자체는 직각(`radius/0`)이다. 필(Pills) 변형의 컨테이너에만 `radius/M` (8px), 활성 필에 `radius/S` (6px)를 적용한다.

---

> 📐 사이즈 기본 원칙은 [파운데이션: 사이즈](../foundations/07-size.md) 참조. 인디케이터는 `size/border/medium`(2px) 적용.

## 변형

### 언더라인 (기본)
- 콘텐츠 위 가로 탭 배열
- 활성 탭: 2px 하단 보더 인디케이터 (Primary 색상)
- 하단 보더가 전체 너비에 걸쳐 있음

### 필 (Pills)
- 둥근 컨테이너 안의 탭
- 컨테이너: `color/surface/3`, 보더 반경 8px, 패딩 4px
- 활성 필: `color/surface/1` 배경, 박스 섀도우, 보더 반경 6px
- 폰트: 13px / Medium

---

## 사이즈 동작

| 속성 | 값 |
|---|---|
| layoutSizingHorizontal | `FILL` 또는 `HUG` (배치 컨텍스트) |
| layoutSizingVertical | `HUG` |

> Tab 바 Height는 각 탭 아이템의 콘텐츠 + 패딩으로 자동 결정된다. 임의 px 값으로 Fixed 지정 금지.

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
다음 스펙으로 탭(Tabs) 네비게이션 컴포넌트를 만들어줘:

언더라인 변형 (기본):
- 탭 항목들을 가로로 배열
- 활성: Primary 텍스트 색상, 2px 오렌지 하단 보더 인디케이터
- 비활성: 회색 텍스트, 인디케이터 없음
- 호버: 약간 진한 텍스트
- 연한 회색의 전체 너비 하단 보더
- 폰트: 14px Medium, 패딩 10px 16px

필 변형:
- 필 컨테이너: 둥근 회색 배경 (8px 반경), 4px 패딩
- 활성 필: 흰색 배경, 미세한 그림자, 6px 반경
- 비활성: 배경 없음
- 폰트: 13px Medium, 패딩 6px 14px

아래 탭 콘텐츠 영역 (빈 프레임)

네이밍: Tabs / Underline, Tabs / Pills
```
