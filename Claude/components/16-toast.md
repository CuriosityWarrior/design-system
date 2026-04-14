# 컴포넌트: 토스트 / 스낵바 (Toast)

## 개요
자동으로 나타났다가 사라지는 임시 플로팅 알림.

---

## 디자인 토큰

| 토큰 | 값 |
|---|---|
| 배경 | `color/text/primary` (반전) |
| 텍스트 | `color/surface/1` (반전) |
| 보더 반경 | `radius/L` = 12px |
| 패딩 | `spacing/12` `spacing/16` |
| 그림자 | `shadow/toast` |
| 최대 너비 | 360px |
| 자동 닫힘 | 3초 |
| 등장 모션 | `motion/scale` = 200ms spring |
| 퇴장 모션 | `motion/fade` = 200ms ease-out |
| 아이콘 크기 | `size/XS` (16px) |

---

> 📐 사이즈 기본 원칙은 [파운데이션: 사이즈](../foundations/07-size.md) 참조.

## 구조
- **아이콘** (16px, `size/XS`) — 좌측. `01 — Icons` 페이지 인스턴스
- **메시지 텍스트** (`text/label-sm` 13px / SemiBold) — flex-1
- **선택적 액션 버튼** (`text/label-xs` 12px / Medium, `color/primary/tint`)
- **닫기 버튼** — 우측. `close` 아이콘 인스턴스 (`size/XS` 16px), `01 — Icons` 페이지

> 좌측 아이콘과 우측 닫기 버튼 모두 텍스트 기호가 아닌 **01 — Icons 인스턴스**를 사용한다.

---

## 위치
- 고정: 우측 하단, 가장자리에서 `spacing/24`
- 여러 토스트 스택: `spacing/8` 간격으로 세로 쌓기

---

## 사이즈 동작

| 속성 | 값 |
|---|---|
| layoutSizingHorizontal | `HUG` (max-width 360px) |
| layoutSizingVertical | `HUG` |

---

### Variants 구성
- 모든 변형은 Figma의 **Combine as Variants** 기능을 사용하여 하나의 Component Set으로 통합한다.

---

### 아이콘 사용 규칙
- 좌측 알림 아이콘과 우측 닫기(`close`) 아이콘 모두 `01 — Icons` 페이지에 정의된 아이콘 컴포넌트 인스턴스를 사용한다.
- 유니코드 문자, 특수 기호 텍스트(✓, ✕, ⚠ 등)로 아이콘을 대체하는 것을 금지한다.
- 아이콘 크기는 `size/XS` (16px)로 통일한다.

---

## Figma Make 프롬프트

```
다음 스펙으로 토스트(Toast) 알림 컴포넌트를 만들어줘:

배경: 어두운 색상 (#1A1916) — 반전 서피스
텍스트: 흰색 (13px SemiBold)
보더 반경: 12px
엘리베이션 드롭 섀도우
최대 너비: 360px

구조:
- 좌측: 아이콘 인스턴스 (01 — Icons, 16px) — 텍스트 기호 금지
- 중앙: 메시지 텍스트 (flex-1)
- 선택적: 액션 텍스트 버튼 (오렌지 틴트)
- 우측: close 아이콘 인스턴스 (01 — Icons, 16px) — 텍스트 기호 금지

변형:
- Default (아이콘 + 메시지 + 닫기)
- With Action (아이콘 + 메시지 + 액션 버튼 + 닫기)

위치: 우측 하단 고정
애니메이션: 스프링 팝인, 페이드 아웃

Combine as Variants 적용.
네이밍: Toast / Default, Toast / With Action
```
