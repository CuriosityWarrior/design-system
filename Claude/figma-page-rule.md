# Figma Page Naming Convention

## 개요

디자인 시스템 Figma 파일 내 페이지 네이밍 규칙을 정의한다.
일관된 네이밍 구조를 통해 협업 효율을 높이고, 신규 페이지 추가 시 기준으로 활용한다.

---

## 규칙

### 1. 섹션 구분자

- 대괄호 `[ ]` 로 섹션 이름을 감싼다.
- 섹션 이름은 **모두 대문자(UPPERCASE)** 로 작성한다.
- 섹션 구분자 페이지는 실제 작업 내용을 포함하지 않는다. 구분 목적으로만 사용한다.

```
[ FOUNDATIONS ]
[ COMPONENTS ]
```

### 2. 컴포넌트 / 파운데이션 페이지

- `{두 자리 번호} — {이름}` 형식으로 작성한다.
- 번호는 `01`부터 시작하는 두 자리 숫자로 패딩한다.
- 구분자는 **em dash(`—`)** 를 사용한다. (하이픈 `-` 사용 금지)
- 이름은 영문 Title Case로 작성한다.

```
01 — Color
02 — Typography
01 — Icons
02 — Button
```

### 3. 특수 페이지

- `Cover`, `Changelog` 는 번호 없이 이름만 작성한다.
- 섹션 구분자 없이 파일 최상단에 위치한다.

---

## 전체 페이지 구조

```
Cover
Changelog

[ FOUNDATIONS ]
01 — Color
02 — Typography
03 — Spacing
04 — Shadow
05 — Border Radius
06 — Motion

[ COMPONENTS ]
01 — Icons
02 — Button
03 — Icon Button
04 — Badge & Tag
05 — Avatar
06 — Spinner
07 — Divider
08 — Tooltip
09 — Input
10 — Textarea
11 — Select
12 — Checkbox
13 — Radio
14 — Toggle
15 — Alert
16 — Toast
17 — Progress Bar
18 — Skeleton
19 — Empty State
20 — Card
21 — Modal
22 — Drawer
23 — Tabs
24 — Breadcrumb
25 — Pagination
26 — Table
27 — List Item
28 — Stat Card
29 — Chip
30 — Label
```

---

## 신규 페이지 추가 시 기준

| 유형 | 위치 | 네이밍 형식 |
|---|---|---|
| 파운데이션 추가 | `[ FOUNDATIONS ]` 섹션 하단 | `{다음 번호} — {이름}` |
| 컴포넌트 추가 | `[ COMPONENTS ]` 섹션 하단 | `{다음 번호} — {이름}` |
| 특수 페이지 추가 | 파일 최상단 | 이름만 작성 |

---

## 금지 사항

- 하이픈(`-`) 사용 금지 → em dash(`—`) 사용
- 한글 페이지 이름 사용 금지 → 영문 작성
- 번호 없이 컴포넌트/파운데이션 페이지 추가 금지
- 섹션 구분자 소문자 사용 금지 → 항상 UPPERCASE

---

## 버전 히스토리

- 수정 시 테이블 Row를 추가하여 버전, 날짜, 변경 내용을 기록한다.
- 버저닝 규칙은 통상적인 규칙을 따른다.

| 버전 | 날짜 | 변경 내용 |
|---|---|---|
| v1.0 | 2026.04.07 | 최초 작성 |
