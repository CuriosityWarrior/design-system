# 컴포넌트: 툴팁 (Tooltip)

## 개요
호버 또는 포커스 시 나타나 요소에 대한 추가 맥락을 제공하는 작은 플로팅 레이블.

---

## 디자인 토큰

| 토큰 | 값 |
|---|---|
| 배경 | `color/text/primary` (반전 색상) |
| 텍스트 색상 | `color/surface/1` (반전) |
| 폰트 | 12px / Regular 400 |
| 패딩 | 6px 10px |
| 보더 반경 | `radius/tooltip` = 6px |
| 그림자 | `shadow/dropdown` |
| 트리거와의 간격 | 8px |
| 모션 | `motion/fade` = 200ms ease-out |

---

> 📐 사이즈 기본 원칙은 [파운데이션: 사이즈](../foundations/07-size.md) 참조. 툴팁은 콘텐츠 기반으로 크기가 결정되므로 Semantic 토큰 미적용.

### Size/Spacing 토큰 바인딩

| 속성 | 토큰 | 값 |
|---|---|---|
| 내부 패딩 상하 | `spacing/6` | 6px |
| 내부 패딩 좌우 | `spacing/10` | 10px |
| 트리거와의 간격 | `spacing/8` | 8px |
| Tail 높이 | `size/6` | 6px |
| 최대 너비 | 240px (레이아웃 고정 — 토큰 미적용) |

> Figma에서 해당 속성에 Variables를 직접 바인딩한다. 임의 px 고정값 사용 금지.

---

## 위치

### Top (툴팁이 위에 위치 — 기본)
- 트리거 요소 위에 나타남
- 툴팁 좌우 정중앙 기준으로, 툴팁 최하단에 Tail의 최상단이 맞닿도록 배치
- Tail은 아래를 향하는 삼각형 (▼)
- 등장: opacity 0→1, translateY(4px)→0, 200ms ease-out

### Bottom (툴팁이 아래에 위치)
- 트리거 요소 아래에 나타남
- 툴팁 좌우 정중앙 기준으로, 툴팁 최상단에 Tail의 최하단이 맞닿도록 배치
- Tail은 위를 향하는 삼각형 (▲)

---

## Tail (꼬리)
- 높이: 6px
- 형태: 이등변 삼각형 (밑변 10px, 높이 6px)
- 색상: 툴팁 배경색과 동일
- 위치: 툴팁 좌우 정중앙에 정렬
- Top 변형: 툴팁 하단에 Tail 상단이 맞닿음 (Tail이 아래로 향함)
- Bottom 변형: 툴팁 상단에 Tail 하단이 맞닿음 (Tail이 위로 향함)

---

## 접근성
- 툴팁 요소에 `role="tooltip"` 사용
- 트리거는 `aria-describedby`로 툴팁 ID 참조
- 키보드 접근성 필수 (포커스 시 표시)

---

## 사이즈 동작

| 속성 | 값 |
|---|---|
| layoutSizingHorizontal | `HUG` (max-width 240px) |
| layoutSizingVertical | `HUG` |

> 콘텐츠(텍스트) 기반으로 자동 조정. 최대 너비는 240px로 제한. 임의 px 값으로 Fixed 지정 금지.

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
다음 스펙으로 툴팁(Tooltip) 컴포넌트를 만들어줘:

외형:
- 배경: 어두운 색상(#1A1916 라이트 / #FAFAF8 다크) — 페이지 배경 반전
- 텍스트: 흰색/밝은 색상 (12px Regular)
- 패딩: 6px 10px, 보더 반경: 6px
- 엘리베이션용 드롭 섀도우

위치: 상단(기본), 하단
- 트리거를 향하는 5px 삼각형 화살표
- 툴팁과 트리거 사이 8px 간격

동작:
- 호버/포커스 시 표시
- 페이드 인: opacity 0→1 + 약간의 translateY, 200ms
- 최대 너비 240px

네이밍: Tooltip / Top, Tooltip / Bottom
```
