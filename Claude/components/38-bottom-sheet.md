# 컴포넌트: 바텀 시트 (Bottom Sheet)

## 개요
화면 하단에서 위로 슬라이드 올라오는 보조 패널. Drawer의 하단 변형이지만, 모바일에서 콘텐츠 선택/액션 시트/필터 등의 맥락에 특화된 UX를 가진다. 드래그 핸들과 스냅 높이(peek / half / full)가 특징.

---

## 디자인 토큰

| 토큰 | 값 |
|---|---|
| 배경 | `color/surface/1` |
| 상단 보더 반경 | `radius/XL` (20px) (상단 모서리만 라운드) |
| 그림자 | `shadow/sheet` = 0 -4px 16px rgba(0,0,0,0.08) |
| 드래그 핸들 | 36 × 4px, `color/border/strong`, 9999px 반경 |
| 핸들 영역 상하 패딩 | 8px / 12px |
| 패딩 (본문) | 16px 20px |
| 스크림(배경 오버레이) | rgba(26,25,22,0.40) |
| 등장 모션 | `motion/slide-up` = 300ms cubic-bezier(0.32, 0.72, 0, 1) |
| 퇴장 모션 | 200ms ease-in |

---

### Size/Spacing 토큰 바인딩

| 속성 | 토큰 | 값 |
|---|---|---|
| 상단 보더 반경 | `radius/XL` | 20px |
| 드래그 핸들 너비 | `size/36` | 36px |
| 드래그 핸들 높이 | `size/4` | 4px |
| 핸들 영역 패딩 상 | `spacing/8` | 8px |
| 핸들 영역 패딩 하 | `spacing/12` | 12px |
| 본문 패딩 상하 | `spacing/16` | 16px |
| 본문 패딩 좌우 | `spacing/20` | 20px |
| Peek 높이 | 120px (레이아웃 고정 — 토큰 미적용) |

> Figma에서 해당 속성에 Variables를 직접 바인딩한다. 임의 px 고정값 사용 금지.

---

## 변형 (Variant)

### Modal Bottom Sheet
- 스크림과 함께 표시. 다른 콘텐츠 상호작용 차단
- 예: 공유 시트, 선택 시트, 폼

### Standard Bottom Sheet
- 스크림 없이 하단에 고정. 콘텐츠와 함께 스크롤
- 예: 지도 앱의 장소 정보 패널

### Expandable (스냅)
- 3단계 스냅 포인트: Peek (120px) → Half (50vh) → Full (90vh)
- 드래그로 높이 조절, 제스처로 닫기

---

## 구성 요소

### Drag Handle (상단)
- 36 × 4px 둥근 막대
- 중앙 정렬, `color/border/strong`
- 드래그 가능 영역 (탭 영역은 상하 12px 포함)

### Header (옵션)
- 제목 (17px SemiBold) + 선택 Close 버튼
- 제목 없이 Drag Handle만 있는 단순 버전도 가능

### Content
- 리스트, 폼, 설명, 이미지 등 자유 배치

### Action Bar (하단, 옵션)
- 주요 CTA 1~2개 (Button 인스턴스)
- 배경: `color/surface/1`, 상단 보더

---

## 스냅 포인트 (Expandable)

| 단계 | 높이 | 사용 |
|---|---|---|
| Peek | 120px | 초기 요약 표시 |
| Half | 50vh | 주요 콘텐츠 노출 |
| Full | 90vh | 세부 내용 전체 표시 |

---

## 상태 (State)

| 상태 | 스크림 | 시트 위치 |
|---|---|---|
| Closed | opacity 0 | translateY(100%) |
| Opening | opacity 0→0.4 | translateY(100% → 0) |
| Open | opacity 0.4 | 지정 스냅 포인트 |
| Closing | opacity 0.4→0 | translateY(0 → 100%) |
| Dragging | opacity 0.4 | 드래그 위치 추적 |

---

## 사이즈 동작

| 속성 | 값 |
|---|---|
| layoutSizingHorizontal | `FILL` (뷰포트 너비) |
| layoutSizingVertical | `FIXED` (스냅 포인트별 지정) 또는 `HUG` (콘텐츠 기반 단일 높이) |

> 스냅 변형은 Peek/Half/Full 각각 고정 높이. 단일 높이 변형은 콘텐츠 기반 HUG. 임의 px 값 금지.

---

## 접근성
- `role="dialog"` + `aria-modal="true"` (Modal 변형)
- `aria-labelledby`로 헤더 제목과 연결
- 키보드: Esc로 닫기, Tab 순환은 시트 내부로 트랩
- 드래그 핸들: 스크린리더에서는 "닫기" 버튼으로 대체 노출

---

### Variants 구성
- 모든 변형은 Figma의 **Combine as Variants** 기능을 사용하여 하나의 Component Set으로 통합한다.

---

### 아이콘 사용 규칙
- 헤더의 닫기 아이콘(`close`)은 반드시 `01 — Icons` 페이지에 정의된 아이콘 컴포넌트 인스턴스를 사용한다.
- 유니코드 문자, 특수 기호 텍스트(✕ 등)로 닫기 아이콘을 대체하는 것을 금지한다.
- 아이콘 크기는 컴포넌트의 사이즈 변형에 맞춰 조정한다.

---

## Figma Make 프롬프트

```
다음 스펙으로 바텀 시트(Bottom Sheet) 컴포넌트를 만들어줘:

변형: Modal Bottom Sheet, Standard Bottom Sheet, Expandable (스냅)

공통:
- 배경 흰색, 상단 보더 반경 20px (상단 좌우만)
- 그림자: 0 -4px 16px rgba(0,0,0,0.08)
- 너비 Fill (뷰포트), 화면 하단 고정

상단 드래그 핸들:
- 36×4px, 9999 보더 반경, 회색 (color/border/strong)
- 상하 여백 8px/12px

Header (옵션):
- 제목 17px SemiBold + 우측 close 아이콘 버튼 (Icons 페이지 인스턴스, 텍스트 기호 금지)

Content:
- 패딩 16px 20px

Action Bar (옵션, 하단):
- Button 인스턴스 1~2개
- 상단 1px 보더

Modal 변형: 배경 스크림 rgba(26,25,22,0.40)

Expandable 스냅 포인트: Peek 120px, Half 50vh, Full 90vh

네이밍: Bottom Sheet / {Modal|Standard|Expandable} / {스냅 상태}
```
