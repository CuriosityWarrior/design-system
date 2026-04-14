# 컴포넌트: 스피너 (Spinner)

## 개요
처리 중인 상태를 나타내는 로딩 인디케이터.

---

## 디자인 토큰

| 토큰 | 값 |
|---|---|
| 주요 색상 | `color/primary/default` |
| 트랙 색상 | `color/border/default` |
| 애니메이션 | spin 700ms linear infinite |

---

## 원형 스피너 크기

> 📐 Width와 Height 모두 [파운데이션: 사이즈](../foundations/07-size.md)의 Semantic 토큰을 참조한다 (정사각형).

| 크기 | Size 토큰 | 가로 × 세로 | 보더 두께 |
|---|---|---|---|
| Large (L) | `size/spinner/L` → `size/L` | 40 × 40px | 3px |
| Medium (M) | `size/spinner/M` → `size/M` | 32 × 32px | 3px |
| Small (S) | `size/spinner/S` → `size/S` | 24 × 24px | 2.5px |
| XS | `size/spinner/xs` → `size/xs` | 16 × 16px | 2px |

---

## 색상 변형

| 변형 | 호 색상 | 사용처 |
|---|---|---|
| Primary | `color/primary/default` (오렌지) | 기본 |
| 무채색 (Muted) | `color/text/secondary` (회색) | 저강조 |
| 흰색 (White) | `color/common/white` (#FFFFFF) | 어두운/컬러 배경 위 |

---

## 점 스피너
- 3개 점 가로 배열, 각 7×7px, `color/primary/default`
- 간격: 5px
- 순차적 바운스 애니메이션 (딜레이: -0.32s, -0.16s, 0s)

---

## 사용 지침
- 전체 페이지/섹션 로딩 → 원형 스피너
- 인라인/최소 로딩 → 점 스피너
- 버튼 로딩 상태 내부 → 흰색 변형
- `aria-busy="true"`, `aria-label="로딩 중"` 함께 사용

---

## 사이즈 동작

| 속성 | 값 |
|---|---|
| layoutSizingHorizontal | `FIXED` |
| layoutSizingVertical | `FIXED` |

> 정사각형 고정 크기. Size 토큰(`size/spinner/*`)을 통해서만 크기를 지정한다. HUG 사용 금지.

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
다음 스펙으로 스피너(Spinner) 로딩 인디케이터 컴포넌트를 만들어줘:

원형 스피너:
크기: Large(40px), Medium(32px), Small(24px), XS(16px)
Width/Height에는 Size/Semantic Variables (size/spinner/L, M, S, xs)를 바인딩
구조: 회색 트랙 + 오렌지 활성 호(상단), 700ms linear 무한 회전

색상 변형:
- Primary: 오렌지 호(#F26A00 라이트 / #FF8A1E 다크)
- 무채색: 회색 호
- 흰색: 흰색 호(어두운 배경 위)

점 스피너:
오렌지 7px 원형 3개, 5px 간격, 순차적 바운스 애니메이션

네이밍: Spinner / Circle / {크기}, Spinner / Dots
```
