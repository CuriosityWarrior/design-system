# 컴포넌트: 드로어 / 시트 (Drawer)

## 개요
보조 콘텐츠나 액션을 위해 화면 가장자리에서 슬라이드 인하는 사이드 패널.

---

## 디자인 토큰

| 토큰 | 값 |
|---|---|
| 배경 | `color/surface/1` |
| 그림자 | `shadow/modal` |
| 너비 | 360px (최대 90vw) |
| 오버레이 | `color/surface/overlay` |
| 보더 반경 (바텀 시트) | `radius/XL` (16px) — 상단 모서리만 적용 (topLeftRadius/topRightRadius = `radius/XL`, bottomLeftRadius/bottomRightRadius = `radius/0`) |
| 모션 | `motion/page` = 300ms ease-out (translateX) |

---

> 📐 사이즈 기본 원칙은 [파운데이션: 사이즈](../foundations/07-size.md) 참조. 내부 버튼/인풋은 해당 컴포넌트의 Semantic 토큰을 따른다.

## 구조
- **헤더**: 제목 (18px / SemiBold) + 닫기 버튼
  - 패딩: 20px 24px
  - 하단 보더: `color/border/subtle`
  - flex-shrink: 0
- **본문**: 스크롤 가능한 콘텐츠 영역
  - 패딩: 20px 24px
  - flex: 1, overflow-y: auto
- **푸터**: 액션 버튼 — `02 — Button` 페이지의 Button 컴포넌트 인스턴스 (전체 너비 또는 우측 정렬)
  - 패딩: 16px 24px
  - 상단 보더: `color/border/subtle`
  - flex-shrink: 0

---

### Size/Spacing 토큰 바인딩

| 속성 | 토큰 | 값 |
|---|---|---|
| 기본 너비 | 360px (레이아웃 고정 — 토큰 미적용) |
| 헤더 패딩 상하 | `spacing/20` | 20px |
| 헤더 패딩 좌우 | `spacing/24` | 24px |
| 본문 패딩 상하 | `spacing/20` | 20px |
| 본문 패딩 좌우 | `spacing/24` | 24px |
| 푸터 패딩 상하 | `spacing/16` | 16px |
| 푸터 패딩 좌우 | `spacing/24` | 24px |
| 헤더–본문 구분 보더 | 1px |

> Figma에서 해당 속성에 Variables를 직접 바인딩한다. 임의 px 고정값 사용 금지.

---

## 위치
- **우측** (기본): 우측 가장자리에서 슬라이드 인
- **하단** (모바일): 하단에서 슬라이드 업 (바텀 시트)

---

## 사이즈 동작

| 속성 | 값 |
|---|---|
| layoutSizingHorizontal | `FIXED` (크기 변형별 고정 너비) |
| layoutSizingVertical | `FILL` (뷰포트 전체 높이) |

> 좌/우 드로어는 너비만 고정하고 높이는 뷰포트에 맞춘다. 내부 콘텐츠는 스크롤.

---

## 아이콘 사용 규칙

> 컴포넌트 내 아이콘은 반드시 `01 — Icons` 페이지의 아이콘 컴포넌트 인스턴스를 사용한다.
> 텍스트 특수 문자(✓, ✕, →, ⋯ 등), 이모지, 직접 그린 벡터 도형으로 아이콘을 대체하는 것을 금지한다.
> 필요한 아이콘이 없는 경우, 먼저 `01 — Icons` 페이지에 추가한 후 인스턴스를 참조한다.

---

## Figma Make 프롬프트

```
다음 스펙으로 드로어/사이드 패널(Drawer) 컴포넌트를 만들어줘:

너비: 360px, 전체 뷰포트 높이
위치: 우측 가장자리 고정
배경: 흰색 / 다크 서피스
좌측 가장자리에 강한 그림자

구조 (전체 높이 flex 컬럼):
- 헤더: 제목 (18px SemiBold) + ✕ 닫기 버튼, 하단 보더
- 본문: 스크롤 가능한 콘텐츠, 패딩 20px 24px
- 푸터: 나란한 두 Button 컴포넌트 인스턴스 (Secondary 취소 + Primary 저장), 상단 보더

슬라이드인 애니메이션: 우측에서 300ms ease-out

모바일 변형: 바텀 시트
- 전체 너비, 하단 고정
- 상단 모서리 둥글게 (24px)
- 하단에서 슬라이드 업

네이밍: Drawer / Right, Drawer / Bottom Sheet
```
