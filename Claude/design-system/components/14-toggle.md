# 컴포넌트: 토글 / 스위치 (Toggle)

## 개요
설정 및 기능 플래그를 위한 이진 ON/OFF 컨트롤.

---

## 디자인 토큰

| 토큰 | 값 |
|---|---|
| 트랙 (OFF) | `color/border/strong` |
| 트랙 (ON) | `color/primary/default` |
| 썸 | `color/common/white` (#FFFFFF) |
| 썸 그림자 | 0 1px 3px rgba(0,0,0,0.15) |
| 보더 반경 (트랙/썸) | `radius/FULL` (9999px — pill 형태) |
| 모션 | 100ms ease-out (썸 슬라이드) |

---

## 크기

> 📐 사이즈 기본 원칙은 [파운데이션: 사이즈](../foundations/07-size.md) 참조. 토글 전용 Semantic 토큰은 현재 미정의 — Semantic 토큰이 추가되면 참조로 전환한다.

| 크기 | 트랙 너비 | 트랙 높이 | 썸 크기 | 이동 거리 |
|---|---|---|---|---|
| Medium (기본) | 40px | 24px | 18×18px | 16px |
| Large | 52px | 30px | 24×24px | 22px |

### Size/Spacing 토큰 바인딩

| 속성 | 토큰 | 값 |
|---|---|---|
| 트랙 높이 (Medium) | `size/S` | 24px |
| 트랙 너비 (Medium) | `size/L` | 40px |
| 썸 크기 (Medium) | `size/18` | 18px |
| 트랙 높이 (Large) | `size/30` | 30px |
| 트랙 너비 (Large) | `size/52` | 52px |
| 썸 크기 (Large) | `size/S` | 24px |
| 트랙 내부 여백 (썸 패딩) | `spacing/3` | 3px |
| 토글–라벨 간격 | `spacing/10` | 10px |

> Figma에서 해당 속성에 Variables를 직접 바인딩한다. 임의 px 고정값 사용 금지.

---

## 상태

| 상태 | 트랙 | 썸 위치 |
|---|---|---|
| OFF | 회색 (`color/border/strong`) | 좌측 (3px 여백) |
| ON | 오렌지 (`color/primary/default`) | 우측 (3px 여백) |
| 비활성 OFF | 40% 불투명도, 회색 | 좌측 |
| 비활성 ON | 40% 불투명도, 오렌지 | 우측 |
| 포커스 | 트랙에 `shadow/focus` |

---

## 레이블 포함 패턴
- 토글 좌측, 레이블 우측, `spacing/10` (10px) 간격
- 레이블: 14px / Regular

## 설정 목록 패턴
- 전체 너비 행: 레이블+설명 좌측, 토글 우측
- 레이블: 14px / Medium
- 설명: 12px / Regular, `color/text/tertiary`
- 행 패딩: `spacing/14` (14px) `spacing/20` (20px)
- 하단 보더: 1px `color/border/subtle`

---

## 사이즈 동작

| 속성 | 값 |
|---|---|
| layoutSizingHorizontal | `FIXED` |
| layoutSizingVertical | `FIXED` |

> 트랙 너비·높이는 고정 값. 크기 변형(Medium/Large)에 따른 지정 외 임의 값 입력 금지.

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
| 즉시 반영 액션 | 토글은 저장 없이 즉시 적용되는 ON/OFF 설정에 사용. 폼 제출이 필요한 이진 선택에는 Checkbox를 사용한다. |
| 레이블 명확화 | 토글 레이블은 ON 상태에서 무엇이 활성화되는지를 명확하게 서술. "알림 허용"처럼 현재 상태를 직관적으로 표현한다. |
| 크기 선택 | 일반 설정 목록에는 Medium, 더 넓은 터치 영역이 필요한 모바일 환경에는 Large를 사용한다. |
| 비활성화 주의 | 비활성(Disabled) 토글은 왜 변경할 수 없는지 사용자가 이해할 수 있도록 근처에 설명을 제공한다. |
| 접근성 | `role="switch"` 및 `aria-checked` 속성으로 ON/OFF 상태를 스크린 리더에 전달한다. |
| 크기 고정 | 트랙·썸 크기는 FIXED 레이아웃으로 고정. Size 토큰 범위 내에서만 지정하며 임의 px 변경 금지. |

---

## Figma Make 프롬프트

```
다음 스펙으로 토글/스위치(Toggle) 컴포넌트를 만들어줘:

Medium 크기: 트랙 40×24px, 썸 18×18px
Large 크기: 트랙 52×30px, 썸 24×24px

트랙 색상:
- OFF: 회색 (#D4D1CA 라이트 / #47443E 다크)
- ON: 오렌지 (#F26A00 라이트 / #FF8A1E 다크)

썸: 흰색 원형, 미세한 그림자
썸이 좌측 (OFF)에서 우측 (ON)으로 슬라이드

상태: OFF, ON, 비활성 OFF, 비활성 ON
포커스: 트랙에 3px 오렌지 링

레이블 포함 변형: 토글 + 텍스트 레이블 나란히

설정 목록 패턴:
- 제목 + 설명 좌측, 토글 우측의 행
- 미세한 하단 보더로 구분

네이밍: Toggle / {크기} / {상태}
```
