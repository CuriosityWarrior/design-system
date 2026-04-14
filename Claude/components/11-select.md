# 컴포넌트: 셀렉트 / 드롭다운 (Select)

## 개요
단일 옵션 선택기. 우측에 드롭다운 쉐브론이 있는 스타일 인풋으로 표시.
Input과 동일한 사이즈 체계 및 스타일 변형을 공유한다.

---

## 디자인 토큰

Input과 동일한 기본 토큰.

| 토큰 | 값 |
|---|---|
| 드롭다운 아이콘 | `01 — Icons` 페이지의 `expand_more` 아이콘 컴포넌트 인스턴스 |
| 아이콘 색상 | `color/text/tertiary` |
| 아이콘 위치 | 우측 정렬 |
| 포커스 링 | `shadow/focus` |

> 드롭다운 화살표는 텍스트(▼)가 아닌 **Icons 페이지의 아이콘 컴포넌트 인스턴스**를 사용한다.

---

## 크기 (Size)

> 📐 Height는 [파운데이션: 사이즈](../foundations/07-size.md) Semantic 토큰, Radius는 [파운데이션: 레디우스](../foundations/05-radius.md) 참조.

| 크기 | Height 토큰 | Height | Radius 토큰 | 폰트 | 패딩 (세로 × 가로) | 아이콘 크기 |
|---|---|---|---|---|---|---|
| L | `size/XL` | 48px | `radius/M` (8px) | 16px / Regular | 14px 14px (우측 40px) | 20px |
| M | `size/L` | 40px | `radius/M` (8px) | 14px / Regular | 11px 12px (우측 36px) | 16px |
| S | `size/S` | 24px | `radius/S` (6px) | 13px / Regular | 4px 10px (우측 30px) | 14px |

> 우측 패딩은 아이콘 크기 + 여백을 포함. 텍스트-아이콘 겹침 방지.

---

## 스타일 변형

### Border 스타일 (기본)
- 배경 투명, 보더로 영역을 표현하는 기본 스타일
- 배경: `color/surface/1`
- 보더: 1px solid `color/border/default`

### Surface 스타일
- 보더 없이 면(Fill)으로 영역을 표현하는 스타일
- 배경: `color/background/subtle`
- 보더: 없음 (포커스 상태에서만 `color/primary/default` 보더 표시)

> 두 스타일 모두 동일한 사이즈(L, M, S) 및 상태(Default, Hover, Focus, Disabled) 변형을 갖는다.

---

## 상태
기본, 호버, 포커스 (`shadow/focus`), 비활성 — Input과 동일.

---

## 사이즈 동작

| 속성 | 값 |
|---|---|
| layoutSizingHorizontal | `FILL` 또는 `HUG` (배치 컨텍스트) |
| layoutSizingVertical | `HUG` |

---

### 아이콘 사용 규칙
- 드롭다운 쉐브론(`expand_more`)은 반드시 `01 — Icons` 페이지에 정의된 아이콘 컴포넌트 인스턴스를 사용한다.
- 유니코드 문자, 특수 기호 텍스트(▼, ▾ 등)로 드롭다운 화살표를 대체하는 것을 금지한다.
- 아이콘 크기는 컴포넌트의 사이즈 변형에 맞춰 조정한다 (L: 20px, M: 16px, S: 14px).

---

## Figma Make 프롬프트

```
다음 스펙으로 셀렉트/드롭다운(Select) 컴포넌트를 만들어줘:

스타일 변형: Border (기본), Surface (채움 배경)
크기:
- L: height 48px, 폰트 16px, 패딩 14px 14px, 우측 패딩 40px, radius 8px, 아이콘 20px
- M: height 40px, 폰트 14px, 패딩 11px 12px, 우측 패딩 36px, radius 8px, 아이콘 16px
- S: height 24px, 폰트 13px, 패딩 4px 10px, 우측 패딩 30px, radius 6px, 아이콘 14px

Height에는 Size Semantic Variables 바인딩 (L→size/XL, M→size/L, S→size/S)
드롭다운 아이콘: 01 — Icons 페이지의 expand_more 인스턴스, 우측 정렬, 크기별 상이

상태: Default, Hover, Focus(오렌지 보더 + 링), Disabled

Combine as Variants 적용.
네이밍: Select / {스타일} / {크기} / {상태}
```
