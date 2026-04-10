# 컴포넌트: 알림 / 배너 (Alert / Banner)

## 개요
사용자에게 상태, 피드백 또는 중요 정보를 전달하는 인라인 메시지.

---

## 디자인 토큰

| 토큰 | 값 |
|---|---|
| 보더 반경 | `radius/M` = 8px |
| 패딩 | `spacing/12` `spacing/16` |
| 폰트 | `text/body-xs` (13px / Regular) |
| 제목 폰트 | `text/heading-xs` (13px / SemiBold) |
| 보더 | `size/1` (1px) solid 틴트 색상 |
| 아이콘 크기 | `size/XS` (16px) |

---

> 📐 사이즈 기본 원칙은 [파운데이션: 사이즈](../foundations/07-size.md) 참조.

## 변형

| 변형 | 배경 | 보더 | 텍스트 | 아이콘 |
|---|---|---|---|---|
| 성공 | `color/success/subtle` | `color/success/tint` | `color/success/text` | `check_circle` |
| 경고 | `color/warning/subtle` | `color/warning/tint` | `color/warning/text` | `warning` |
| 오류 | `color/error/subtle` | `color/error/tint` | `color/error/text` | `cancel` |
| 정보 | `color/info/subtle` | `color/info/tint` | `color/info/text` | `info` |
| 중립 | `color/surface/2` | `color/border/default` | `color/text/secondary` | `more_horiz` |

> 모든 아이콘은 `01 — Icons` 페이지의 해당 아이콘 컴포넌트 인스턴스를 사용한다. (텍스트 기호 금지)

---

## 구조
- **아이콘** (`size/XS` 16px) — 좌측, 첫 줄 상단 정렬. `01 — Icons` 인스턴스
- **콘텐츠 영역** (flex-1) — 선택적 제목 + 본문 텍스트
- **닫기 버튼** (선택) — 우측, `close` 아이콘 인스턴스 (`size/XS` 16px)

---

## 사이즈 동작

| 속성 | 값 |
|---|---|
| layoutSizingHorizontal | `FILL` |
| layoutSizingVertical | `HUG` |

---

## Figma Make 프롬프트

```
다음 스펙으로 알림/배너(Alert/Banner) 컴포넌트를 만들어줘:

5가지 변형: 성공, 경고, 오류, 정보, 중립

성공: 초록 틴트 배경, 초록 보더, 초록 텍스트, check_circle 아이콘 (01 — Icons 인스턴스, 16px)
경고: 앰버 틴트 배경, 앰버 보더, 앰버 텍스트, warning 아이콘 (01 — Icons 인스턴스, 16px)
오류: 빨간 틴트 배경, 빨간 보더, 빨간 텍스트, cancel 아이콘 (01 — Icons 인스턴스, 16px)
정보: 파란 틴트 배경, 파란 보더, 파란 텍스트, info 아이콘 (01 — Icons 인스턴스, 16px)
중립: 회색 배경, 회색 보더, 보조 텍스트, more_horiz 아이콘 (01 — Icons 인스턴스, 16px)

구조: 좌측 아이콘 인스턴스 + 텍스트 콘텐츠 + 선택적 닫기 버튼(close 아이콘 인스턴스) 우측
선택적 굵은 제목(13px SemiBold) + 본문 텍스트(13px Regular)
패딩: 12px 16px, 보더 반경 8px

모든 아이콘은 텍스트 기호가 아닌 01 — Icons 페이지 인스턴스 사용.

Combine as Variants 적용.
네이밍: Alert / {변형}
```
