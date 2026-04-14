# 컴포넌트: 폼 레이블 (Form Label)

## 개요
폼 인풋과 연결된 텍스트 레이블. 선택적 필수 표시와 힌트 텍스트 포함.

---

## 디자인 토큰

| 토큰 | 값 |
|---|---|
| 폰트 | `text/label-md` = 13px / Medium 500 |
| 색상 | `color/text/secondary` |
| 필수 표시 | `*` → `color/error/default` |
| 인풋과의 간격 | 5px |
| 힌트 폰트 | 12px / Regular |
| 힌트 색상 | `color/text/tertiary` |
| 오류 색상 | `color/text/error` |
| 보더 반경 | `radius/XS` (4px) |
| 성공 색상 | `color/text/success` |

---

> 📐 사이즈 기본 원칙은 [파운데이션: 사이즈](../foundations/07-size.md) 참조. 연결된 인풋의 Semantic 사이즈 토큰에 맞춰 사용한다.

### Size/Spacing 토큰 바인딩

| 속성 | 토큰 | 값 |
|---|---|---|
| 레이블–인풋 간격 | `spacing/5` | 5px |
| 인풋–보조 텍스트 간격 | `spacing/4` | 4px |
| 필수 표시(*) 좌측 간격 | `spacing/2` | 2px |

> Figma에서 해당 속성에 Variables를 직접 바인딩한다. 임의 px 고정값 사용 금지.

---

## 구조
- 레이블 텍스트 + 선택적 필수 표시 (*)
- 인풋 아래 (선택): 힌트/오류/성공 메시지

---

## 사이즈 동작

| 속성 | 값 |
|---|---|
| layoutSizingHorizontal | `HUG` |
| layoutSizingVertical | `HUG` |

> 텍스트(+필수 표시) 기준으로 가로·세로 자동 조정. 임의 px 값으로 Fixed 지정 금지.

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
다음 스펙으로 폼 레이블(Form Label) 컴포넌트를 만들어줘:

레이블 텍스트: 13px Medium, 회색 (#66635B)
필수 표시: 레이블 텍스트 바로 뒤에 * (빨간색 #E8321E)

보조 텍스트 변형 (인풋 아래):
- 힌트: 12px Regular, 연한 회색
- 오류: 12px Regular, 빨간색 (#C0220F)
- 성공: 12px Regular, 초록색 (#077235)

간격: 레이블과 인풋 사이 5px, 인풋과 보조 텍스트 사이 4px

네이밍: Label / Default, Label / Required, Label / With Hint, Label / With Error, Label / With Success
```
