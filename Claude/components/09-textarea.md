# 컴포넌트: 텍스트에어리어 (Textarea)

## 개요
설명, 댓글, 메시지 등 긴 내용 입력을 위한 여러 행 텍스트 입력.

---

## 디자인 토큰

인풋과 동일한 기본 토큰에 아래 항목 추가:

| 토큰 | 값 |
|---|---|
| 높이 | 120px (Fixed) |
| 크기 조정 | 세로 방향만 허용 |
| 줄 높이 | `line-height/relaxed` = 1.6 |
| 패딩 | 10px 12px |

## 레이아웃 규칙

| 항목 | 값 |
|---|---|
| layoutSizingVertical | `FIXED` (120px) |

> Textarea는 Hug Contents가 아닌 Fixed Height로 설정한다. 사용자가 입력할 수 있는 영역의 최소 높이를 보장하기 위함.

---

## 스타일 변형

### Border 스타일 (기본)
- Input의 Border 스타일과 동일. 배경 투명, 보더로 영역 표현.
- 보더: 1px solid `color/border/default`
- 배경: `color/surface/1`

### Surface 스타일
- Input의 Surface 스타일과 동일. 보더 없이 면(Fill)으로 영역 표현.
- 배경: `color/background/subtle`
- 보더: 없음 (포커스 상태에서만 `color/primary/default` 보더 표시)

> Input과 스타일 일관성을 유지한다 (보더 두께, radius, 색상 등 동일).

---

## 상태
인풋과 동일: 기본, 호버, 포커스, 오류, 비활성

---

## 글자수 카운터
- 위치: 텍스트에어리어 아래 우측
- 형식: `{현재} / {최대}`
- 폰트: 11px / Regular, `color/text/tertiary`
- 초과 시: 색상 → `color/error/text`

---

## Figma Make 프롬프트

```
다음 스펙으로 텍스트에어리어(Textarea) 컴포넌트를 만들어줘:

인풋 스타일 기반의 여러 행 입력:
- 최소 높이: 80px, 세로 방향으로만 크기 조정 가능
- 패딩: 10px 12px
- 줄 높이: 1.6
- 보더 반경: 8px (인풋과 동일)

상태: 기본, 호버, 포커스 (오렌지 링), 오류 (빨간 보더), 비활성

선택적 글자수 카운터:
- 우측 하단 정렬: "0 / 200"
- 11px 회색 텍스트, 초과 시 빨간색으로 변경

네이밍: Textarea / {상태}
```
