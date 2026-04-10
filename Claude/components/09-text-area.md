# 컴포넌트: 텍스트 에어리어 (Text Area)

## 개요
설명, 댓글, 메시지 등 긴 내용 입력을 위한 여러 행 텍스트 입력.
Input과 동일한 스타일 변형 및 상태를 공유한다.

---

## 디자인 토큰

Input과 동일한 기본 토큰에 아래 항목 추가.

| 토큰 | 값 |
|---|---|
| 크기 조정 | 세로 방향만 허용 |
| 줄 높이 | `lineHeight/relaxed` = 1.6 |
| 패딩 | 10px 12px |
| 보더 반경 | `radius/M` = 8px |

---

## 크기 (Size)

> 📐 Radius는 [파운데이션: 레디우스](../foundations/05-radius.md) 참조. Input과 동일한 크기 체계를 사용한다.

| 크기 | Height (Fixed) | Radius 토큰 | 폰트 | 패딩 |
|---|---|---|---|---|
| L | 120px | `radius/M` (8px) | 16px / Regular | 14px 14px |
| M | 80px | `radius/M` (8px) | 14px / Regular | 11px 12px |
| S | 60px | `radius/S` (6px) | 13px / Regular | 8px 10px |

> Text Area는 HUG가 아닌 Fixed Height를 사용한다. 사용자가 입력할 수 있는 최소 영역 확보를 위함.

---

## 스타일 변형

### Border 스타일 (기본)
- Input의 Border 스타일과 동일. 배경 투명, 보더로 영역 표현.
- 배경: `color/surface/1`
- 보더: 1px solid `color/border/default`

### Surface 스타일
- Input의 Surface 스타일과 동일. 보더 없이 면(Fill)으로 영역 표현.
- 배경: `color/background/subtle`
- 보더: 없음 (포커스 상태에서만 `color/primary/default` 보더 표시)

---

## 상태
Input과 동일: Default, Hover, Focus, Error, Disabled

---

## 글자수 카운터
- 위치: Text Area 아래 우측
- 형식: `{현재} / {최대}`
- 폰트: `text/caption` (12px / Regular), `color/text/tertiary`
- 초과 시: 색상 → `color/error/text`

---

## 사이즈 동작

| 속성 | 값 |
|---|---|
| layoutSizingHorizontal | `FILL` 또는 `HUG` |
| layoutSizingVertical | `FIXED` |

---

## Figma Make 프롬프트

```
다음 스펙으로 텍스트 에어리어(Text Area) 컴포넌트를 만들어줘:

스타일 변형: Border (기본), Surface (채움 배경)
크기:
- L: height 120px Fixed, 폰트 16px, 패딩 14px 14px, radius 8px
- M: height 80px Fixed, 폰트 14px, 패딩 11px 12px, radius 8px
- S: height 60px Fixed, 폰트 13px, 패딩 8px 10px, radius 6px

세로 방향으로만 크기 조정 가능 (resize: vertical)
줄 높이: 1.6

상태: Default, Hover, Focus(오렌지 보더 + 링), Error(빨간 보더), Disabled

선택적 글자수 카운터 (우측 하단): "{현재} / {최대}", 12px 회색, 초과 시 빨간색

Combine as Variants 적용.
네이밍: Text Area / {스타일} / {크기} / {상태}
```
