# 파운데이션: 사이즈 (Size)

## 개요

모든 컴포넌트에 일관되게 적용되는 크기 토큰 시스템.
실제 px 값 기반의 Primitive 토큰을 정의하고, Semantic에서 T-Shirt 사이즈로 Alias하여 컴포넌트에 적용한다.

| 항목 | 값 |
|---|---|
| 단위 | px |
| 구조 | Primitive (실제 값) → Semantic (T-Shirt 사이즈) 2레이어 |
| 라이트/다크 | 동일 |

---

## 디자인 원칙

- **Primitive**는 실제 px 수치를 그대로 토큰명으로 사용한다. 의미를 부여하지 않는다.
- **Semantic**은 Primitive를 Alias하여 T-Shirt 사이즈(XXS~3XL)로 의미를 부여한다.
- 컴포넌트는 **Semantic T-Shirt 토큰**을 참조한다. Primitive를 직접 참조하지 않는다.
- 컴포넌트별로 별도 Semantic 토큰(예: `size/button/xl`)을 만들지 않는다. 동일한 T-Shirt 토큰을 공유한다.
- 짝수가 아닌 임의 값(예: 37px, 46px) 사용 금지.

---

## 디자인 토큰 — Primitive

실제 px 수치를 토큰명으로 사용. 의미 없이 크기만 정의한다.

| 토큰 | 값 |
|---|---|
| `size/1` | 1px |
| `size/2` | 2px |
| `size/4` | 4px |
| `size/6` | 6px |
| `size/8` | 8px |
| `size/10` | 10px |
| `size/12` | 12px |
| `size/14` | 14px |
| `size/16` | 16px |
| `size/20` | 20px |
| `size/24` | 24px |
| `size/28` | 28px |
| `size/32` | 32px |
| `size/36` | 36px |
| `size/40` | 40px |
| `size/44` | 44px |
| `size/48` | 48px |
| `size/56` | 56px |
| `size/64` | 64px |

---

## 디자인 토큰 — Semantic (T-Shirt)

Primitive를 Alias로 참조하여 T-Shirt 사이즈 체계로 의미를 부여한다.
컴포넌트는 이 토큰을 사용한다.

| 토큰 | Primitive 참조 | 값 |
|---|---|---|
| `size/XXS` | `size/12` | 12px |
| `size/XS` | `size/16` | 16px |
| `size/S` | `size/24` | 24px |
| `size/M` | `size/32` | 32px |
| `size/L` | `size/40` | 40px |
| `size/XL` | `size/48` | 48px |
| `size/XXL` | `size/56` | 56px |
| `size/3XL` | `size/64` | 64px |

---

## 컴포넌트별 적용 기준

### 사이즈 적용 방향

| 컴포넌트 | Width 적용 | Height 적용 | 비고 |
|---|---|---|---|
| 아이콘 | `size/*` | `size/*` | 정사각형 |
| 아이콘 버튼 | `size/*` | `size/*` | 정사각형 |
| 아바타 | `size/*` | `size/*` | 정사각형 |
| 스피너 | `size/*` | `size/*` | 정사각형 |
| 버튼 | 가변 (미적용) | `size/*` | 직사각형, Height만 토큰 |
| 인풋 / 셀렉트 | 가변 (미적용) | `size/*` | 직사각형, Height만 토큰 |
| 보더 두께 | — | — | Primitive 직접 참조 |

### 컴포넌트 사이즈 → T-Shirt 토큰 매핑

| 컴포넌트 | XS variant | S variant | M variant | L variant | XL variant |
|---|---|---|---|---|---|
| 버튼 Height | — | `size/S` (24px) | `size/M` (32px) | `size/L` (40px) | `size/XL` (48px) |
| 아이콘 버튼 W+H | `size/XS` (16px) | `size/S` (24px) | `size/M` (32px) | `size/L` (40px) | `size/XL` (48px) |
| 인풋 Height | — | `size/S` (24px) | `size/L` (40px) | `size/XL` (48px) | — |
| 아이콘 W+H | `size/XS` (16px) | `size/S` (24px) | `size/M` (32px) | `size/L` (40px) | — |
| 아바타 W+H | `size/XXS` (12px) | `size/S` (24px) | `size/M` (32px) | `size/L` (40px) | `size/XL` (48px) |
| 스피너 W+H | `size/XS` (16px) | `size/S` (24px) | `size/M` (32px) | `size/L` (40px) | — |

> 보더 두께(`size/1`, `size/2`, `size/4`)는 Primitive를 직접 참조한다. T-Shirt 체계에 포함하기 어색한 얇은 값이기 때문.

---

## Figma Variables 구성 방법

Number 타입으로 등록. Mode 없음 (라이트/다크 동일).

### Primitive Collection

```
size/1  = 1
size/2  = 2
size/4  = 4
size/6  = 6
size/8  = 8
size/10 = 10
size/12 = 12
size/14 = 14
size/16 = 16
size/20 = 20
size/24 = 24
size/28 = 28
size/32 = 32
size/36 = 36
size/40 = 40
size/44 = 44
size/48 = 48
size/56 = 56
size/64 = 64
```

### Semantic Collection (T-Shirt, Primitive를 Alias로 연결)

```
size/XXS → size/12
size/XS  → size/16
size/S   → size/24
size/M   → size/32
size/L   → size/40
size/XL  → size/48
size/XXL → size/56
size/3XL → size/64
```

---

## Change Log

| 버전 | 날짜 | 변경 내용 |
|---|---|---|
| v1.0 | 2026.04.10 | 최초 작성 — Primitive(T-shirt) + Semantic(컴포넌트별) 2레이어 구조 |
| v1.1 | 2026.04.10 | Primitive를 실제 px 값 기반으로 재정의, Semantic을 T-Shirt 공통 체계로 변경. 컴포넌트별 Semantic 토큰 제거 |
