# 컴포넌트: 모달 / 다이얼로그 (Modal)

## 개요
특정 작업이나 확인에 사용자 집중을 유도하는 오버레이 패널.

---

## 디자인 토큰

| 토큰 | 값 |
|---|---|
| 배경 | `color/surface/1` |
| 보더 반경 | `radius/modal` = 16px |
| 그림자 | `shadow/modal` |
| 최대 너비 | 480px |
| 여백 | 16px (뷰포트 가장자리) |
| 오버레이 | `color/surface/overlay` = rgba(26,25,22,0.48) |
| 등장 모션 | `motion/scale` = 200ms spring, scale(0.95)+translateY(8px) → scale(1) |
| 퇴장 모션 | `motion/fade` = 200ms ease-out |

---

> 📐 사이즈 기본 원칙은 [파운데이션: 사이즈](../foundations/07-size.md) 참조. 내부 버튼/인풋은 해당 컴포넌트의 Semantic 토큰을 따른다.

## 구조
- **헤더**: 제목 (18px / SemiBold) + 닫기 아이콘 (우측 상단)
  - 닫기 아이콘은 `01 — Icons` 페이지의 `close` 아이콘 인스턴스(24×24)를 사용한다
  - 패딩: 20px 24px 16px
- **본문**: 콘텐츠, 16px / Regular, `color/text/secondary`
  - 패딩: 20px 24px
  - 최소 높이: 100px
  - 최대 높이: 200px (초과 시 본문 영역 내 스크롤)
- **푸터**: 액션 버튼 (`02 — Button` 페이지의 Button 컴포넌트 인스턴스), 우측 정렬, 간격 8px
  - Secondary (취소) + Primary (확인)
  - 패딩: 16px 24px 20px

---

## 동작
- 오버레이 클릭으로 모달 닫기
- Escape 키로 닫기
- 모달이 열린 동안 포커스 트랩
- 모달 열릴 때 본문 스크롤 잠금

---

## 사이즈 동작

| 속성 | 값 |
|---|---|
| layoutSizingHorizontal | `FIXED` (크기 변형별 고정 너비) |
| layoutSizingVertical | `HUG` (max-height 90vh) |

> 너비는 크기 변형(sm/md/lg 등)에서 고정. Height는 콘텐츠에 맞춰 hug하되 뷰포트 90% 제한. 임의 px 값으로 Fixed 지정 금지.

---

## Figma Make 프롬프트

```
다음 스펙으로 모달/다이얼로그(Modal) 컴포넌트를 만들어줘:

크기: 최대 너비 480px, 뷰포트 중앙 정렬
배경: 흰색 / 다크 서피스
보더 반경: 16px
강한 드롭 섀도우
모달 뒤 반투명 어두운 오버레이

구조:
- 헤더: 제목 (18px SemiBold) + close 아이콘 인스턴스 (01 — Icons 페이지, 24×24), 보더 없음
- 본문: 콘텐츠 영역 (16px 회색 텍스트), 패딩 20px 24px, 최소 높이 100px, 최대 높이 200px (초과 시 본문 내 스크롤), 보더 없음
- 푸터: 우측 정렬 액션 버튼 (02 — Button 페이지의 Button 인스턴스 사용 — Secondary 취소 + Primary 확인), 보더 없음

동작:
- 팝인 애니메이션: 0.95에서 스케일 + 약간 위로 슬라이드
- 오버레이 동시 페이드인

네이밍: Modal / Default
```
