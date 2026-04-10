# 파운데이션: 레디우스 (Radius)

## 개요

컴포넌트 모서리 반경 시스템. Primitive(실제 값) → Semantic(T-Shirt 사이즈) 2레이어 구조.
컴포넌트는 Semantic T-Shirt 토큰을 참조하며, 컴포넌트 사이즈 변형에 따라 적절한 Radius를 매핑한다.

| 항목 | 값 |
|---|---|
| 최소 | 0px |
| 최대 | 9999px (완전한 pill 형태) |
| 라이트/다크 | 동일 |

---

## 디자인 토큰 — Primitive

| 토큰 | 값 |
|---|---|
| `radius/0` | 0px |
| `radius/2` | 2px |
| `radius/4` | 4px |
| `radius/6` | 6px |
| `radius/8` | 8px |
| `radius/10` | 10px |
| `radius/12` | 12px |
| `radius/16` | 16px |
| `radius/24` | 24px |
| `radius/full` | 9999px |

---

## 디자인 토큰 — Semantic (T-Shirt)

Primitive를 Alias로 참조. 컴포넌트는 이 토큰을 사용한다.

| 토큰 | Primitive 참조 | 값 | 적용 대상 |
|---|---|---|---|
| `radius/XS` | `radius/4` | 4px | XS 크기 버튼·인풋, 소형 이미지 |
| `radius/S` | `radius/6` | 6px | S 크기 버튼·인풋, 툴팁 |
| `radius/M` | `radius/8` | 8px | M·L·XL 크기 버튼·인풋 (기본) |
| `radius/L` | `radius/12` | 12px | 카드, 패널, 드롭다운 |
| `radius/XL` | `radius/16` | 16px | 모달, 드로어 상단, 대형 이미지 |
| `radius/FULL` | `radius/full` | 9999px | 뱃지, 태그, 칩, Pill 버튼 |

---

## 컴포넌트 사이즈별 Radius 매핑

동일한 컴포넌트라도 사이즈 변형에 따라 다른 Radius를 적용한다.

| 컴포넌트 | XS | S | M | L | XL |
|---|---|---|---|---|---|
| 버튼 | `radius/XS` (4px) | `radius/S` (6px) | `radius/M` (8px) | `radius/M` (8px) | `radius/M` (8px) |
| 인풋 / 셀렉트 / 텍스트에어리어 | — | `radius/S` (6px) | `radius/M` (8px) | `radius/M` (8px) | — |
| 아이콘 버튼 | `radius/XS` (4px) | `radius/S` (6px) | `radius/M` (8px) | `radius/M` (8px) | `radius/M` (8px) |
| 카드 | — | — | `radius/L` (12px) | `radius/L` (12px) | — |
| 모달 / 드로어 | — | — | — | `radius/XL` (16px) | — |
| 툴팁 | — | `radius/S` (6px) | — | — | — |
| 뱃지 / 태그 / 칩 | — | `radius/FULL` | `radius/FULL` | — | — |

---

## 사용 원칙

- 컴포넌트는 위 매핑 표의 Semantic 토큰만 사용한다.
- 정의되지 않은 임의 값 사용 금지.
- 아바타 원형은 `border-radius: 50%` 사용 — 별도 토큰 불필요.
- 드로어 바텀 시트: 상단 모서리만 `radius/XL` (16px), 하단은 0.

---

## Figma Variables 구성 방법

Number 타입으로 등록.

### Primitive

```
radius/0    = 0
radius/2    = 2
radius/4    = 4
radius/6    = 6
radius/8    = 8
radius/10   = 10
radius/12   = 12
radius/16   = 16
radius/24   = 24
radius/full = 9999
```

### Semantic (T-Shirt, Primitive를 Alias로 연결)

```
radius/XS   → radius/4
radius/S    → radius/6
radius/M    → radius/8
radius/L    → radius/12
radius/XL   → radius/16
radius/FULL → radius/full
```

---

## Change Log

| 버전 | 날짜 | 변경 내용 |
|---|---|---|
| v1.0 | 2026.04.08 | 최초 작성 — Primitive + 컴포넌트별 Semantic |
| v1.1 | 2026.04.10 | 파일명·페이지명 "Border Radius" → "Radius" 변경. Semantic을 컴포넌트별 토큰에서 T-Shirt 사이즈(XS~FULL)로 변경. 컴포넌트 사이즈별 Radius 매핑 추가 |
