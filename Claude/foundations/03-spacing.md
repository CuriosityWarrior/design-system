# 파운데이션: 스페이싱 (Spacing)

## 개요

4px를 최소 단위로 하는 간격 시스템. 모든 값은 4의 배수.
토큰명은 실제 px 수치를 그대로 사용한다 (`spacing/24` = 24px).
Semantic 토큰 없이 Primitive 토큰만 사용한다.

| 항목 | 값 |
|---|---|
| 기준 단위 | 4px |
| 규칙 | 모든 간격은 4의 배수 |
| 토큰 구조 | Primitive만 사용 (Semantic 없음) |
| 라이트/다크 | 동일 |

---

## 디자인 토큰 — Primitive

토큰명은 실제 px 수치. 예: `spacing/24` = 24px.

| 토큰 | 값 |
|---|---|
| `spacing/0` | 0px |
| `spacing/2` | 2px |
| `spacing/4` | 4px |
| `spacing/6` | 6px |
| `spacing/8` | 8px |
| `spacing/10` | 10px |
| `spacing/12` | 12px |
| `spacing/16` | 16px |
| `spacing/20` | 20px |
| `spacing/24` | 24px |
| `spacing/32` | 32px |
| `spacing/40` | 40px |
| `spacing/48` | 48px |
| `spacing/64` | 64px |
| `spacing/80` | 80px |
| `spacing/96` | 96px |

---

## 사용 원칙

- 컴포넌트 패딩, 아이콘-텍스트 간격, 레이아웃 간격 모두 Primitive 토큰을 직접 사용한다.
- Semantic 토큰(`component/sm`, `layout/md` 등) 사용 금지.
- 4px 미만의 값(2px, 3px)은 예외적으로만 허용하며 `spacing/2`를 사용한다.
- 임의 값(매직 넘버) 사용 금지.

### 참고: 일반적인 사용 패턴

| 사용 맥락 | 권장 토큰 |
|---|---|
| 아이콘 내부 패딩 | `spacing/4` |
| 버튼/인풋 요소 간 인라인 간격 | `spacing/8` |
| 버튼·인풋 수직 패딩 | `spacing/8` ~ `spacing/12` |
| 카드 내부 패딩 | `spacing/16` ~ `spacing/20` |
| 컴포넌트 간 간격 | `spacing/16` ~ `spacing/24` |
| 섹션 간 간격 | `spacing/32` ~ `spacing/48` |
| 페이지 섹션 간격 | `spacing/64` ~ `spacing/80` |

---

## Figma Variables 구성 방법

Number 타입으로 등록. Mode 없음 (라이트/다크 동일).

```
spacing/0  = 0
spacing/2  = 2
spacing/4  = 4
spacing/6  = 6
spacing/8  = 8
spacing/10 = 10
spacing/12 = 12
spacing/16 = 16
spacing/20 = 20
spacing/24 = 24
spacing/32 = 32
spacing/40 = 40
spacing/48 = 48
spacing/64 = 64
spacing/80 = 80
spacing/96 = 96
```

---

## Change Log

| 버전 | 날짜 | 변경 내용 |
|---|---|---|
| v1.0 | 2026.04.08 | 최초 작성 — Primitive + Semantic 2레이어 구조 |
| v1.1 | 2026.04.10 | Semantic 토큰 제거. Primitive 토큰명을 실제 px 값 기반으로 변경 (spacing/1→spacing/4 등). 모든 컴포넌트·레이아웃에서 Primitive 직접 사용 |
