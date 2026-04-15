# 컴포넌트: 데이터 케이스 (Data Case)

## 개요
데이터 조회 결과가 비어 있거나 특수한 상태일 때 표시하는 상태 컴포넌트.
Empty, Error, Loading, No Results, No Permission, Offline 등 공통 데이터 상태를 포함한다.

---

## 디자인 토큰

| 토큰 | 값 |
|---|---|
| 패딩 | `spacing/48` `spacing/24` |
| 아이콘 크기 | `size/L` (40px) |
| 아이콘 색상 | `color/text/tertiary` (opacity 0.5) |
| 제목 | `text/heading-lg` (18px / SemiBold) |
| 설명 | `text/body-md` (16px / Regular), `color/text/secondary` |
| 설명 최대 너비 | 320px |
| 보더 반경 | `radius/L` (12px) — 카드형 컨테이너 (선택적, 부모 카드가 처리할 수 있음) |
| CTA 버튼 | `02 — Button` 페이지의 Button 컴포넌트 인스턴스 |

> 아이콘은 `01 — Icons` 페이지의 인스턴스를 사용한다. (이모지·직접 그린 벡터 금지)

---

## 구조 (중앙 정렬, 세로 쌓기)
1. 아이콘 인스턴스 (`size/L` 40px, `color/text/tertiary`)
2. 간격: `spacing/16`
3. 제목 (`text/heading-lg`)
4. 간격: `spacing/8`
5. 설명 텍스트 (중앙 정렬, 최대 너비 320px)
6. 간격: `spacing/20`
7. CTA 버튼 — Button 컴포넌트 인스턴스 (선택)

---

## 변형 (Variant)

### Empty (데이터 없음)
- **아이콘**: `folder_open` (`01 — Icons`)
- **제목**: "아직 [항목]이 없어요"
- **설명**: 첫 항목을 추가하는 방법 안내
- **CTA**: Primary 버튼 (예: "+ 새로 만들기")

### No Results (검색 결과 없음)
- **아이콘**: `search` (`01 — Icons`)
- **제목**: "검색 결과가 없어요"
- **설명**: 다른 검색어 또는 필터 조정 제안
- **CTA**: Secondary 버튼 (예: "검색 초기화")

### Error (오류)
- **아이콘**: `error` (`01 — Icons`), `color/error/default`
- **제목**: "오류가 발생했어요"
- **설명**: 잠시 후 다시 시도하거나 지원팀에 문의 안내
- **CTA**: Secondary 버튼 (예: "다시 시도")

### Loading (로딩 중)
- **아이콘**: Spinner 컴포넌트 (`06 — Spinner` 페이지 인스턴스, `size/L`)
- **제목**: "불러오는 중이에요"
- **설명**: (선택) 잠시 기다려 달라는 안내
- **CTA**: 없음

### No Permission (권한 없음)
- **아이콘**: `lock` (`01 — Icons`)
- **제목**: "접근 권한이 없어요"
- **설명**: 관리자에게 권한을 요청하거나 로그인 필요 안내
- **CTA**: Secondary 버튼 (예: "관리자에게 요청")

### Offline (오프라인)
- **아이콘**: `cloud_off` (추후 Icons 추가) 또는 `language` (`01 — Icons`)
- **제목**: "인터넷 연결을 확인해 주세요"
- **설명**: 네트워크 연결 후 다시 시도 안내
- **CTA**: Secondary 버튼 (예: "다시 시도")

---

## 사이즈 동작

| 속성 | 값 |
|---|---|
| layoutSizingHorizontal | `FILL` 또는 `HUG` |
| layoutSizingVertical | `HUG` |

---

### Variants 구성
- 모든 변형은 Figma의 **Combine as Variants** 기능을 사용하여 하나의 Component Set으로 통합한다.

---

### 아이콘 사용 규칙
- 모든 상태 아이콘(`folder_open`, `search`, `error`, `lock`, `cloud_off`/`language`)은 `01 — Icons` 페이지에 정의된 아이콘 컴포넌트 인스턴스를 사용한다.
- Loading 변형의 Spinner는 `06 — Spinner` 페이지의 Spinner 컴포넌트 인스턴스를 사용한다.
- 유니코드 문자, 특수 기호 텍스트(✓, ✕, ⚠ 등)나 이모지, 직접 그린 벡터로 아이콘을 대체하는 것을 금지한다.
- 아이콘 크기는 `size/L` (40px)로 통일한다.

---

---

## 사용 원칙

| 원칙 | 설명 |
|---|---|
| 모든 데이터 상태 처리 | 데이터를 표시하는 모든 화면에서 Empty, Error, Loading, No Results 상태를 반드시 처리한다. 처리되지 않은 빈 화면은 사용자에게 혼란을 준다. |
| 맥락에 맞는 변형 선택 | 상황에 정확히 대응하는 변형을 선택한다. "검색 결과 없음"에 일반 Empty를 사용하거나, "권한 없음"에 Error를 사용하지 않는다. |
| CTA로 다음 행동 안내 | 가능한 경우 CTA 버튼을 포함하여 사용자가 막힌 상태에서 벗어날 수 있는 명확한 다음 행동을 제시한다. |
| Loading 변형에 CTA 금지 | 로딩 중 상태에서는 사용자가 취할 수 있는 액션이 없으므로 CTA 버튼을 포함하지 않는다. |
| 메시지 구체성 | 제목과 설명 텍스트는 항목의 종류와 상황에 맞게 구체적으로 작성한다. 범용적인 "오류가 발생했습니다"보다 상황을 설명하는 메시지를 우선한다. |

## Figma Make 프롬프트

```
다음 스펙으로 데이터 케이스(Data Case) 컴포넌트를 만들어줘:

레이아웃: 세로 중앙 정렬, 모든 요소 가운데 정렬
패딩: 상하 48px, 좌우 24px

구조:
1. 아이콘 인스턴스 (01 — Icons, 40px, 연한 회색)
2. 제목 (18px SemiBold, 아이콘 아래 16px 간격)
3. 설명 텍스트 (16px Regular, 회색, 최대 너비 320px, 제목 아래 8px)
4. CTA 버튼 인스턴스 (02 — Button, 설명 아래 20px, 선택)

6가지 변형:
- Empty: folder_open 아이콘, "아직 항목이 없어요", Primary 버튼
- No Results: search 아이콘, "검색 결과가 없어요", Secondary 버튼
- Error: error 아이콘(빨간색), "오류가 발생했어요", Secondary 버튼
- Loading: Spinner 인스턴스(크기 L), "불러오는 중이에요", 버튼 없음
- No Permission: lock 아이콘, "접근 권한이 없어요", Secondary 버튼
- Offline: language 아이콘, "인터넷 연결을 확인해 주세요", Secondary 버튼

모든 아이콘은 01 — Icons 페이지 인스턴스 사용 (이모지 금지).
CTA 버튼은 02 — Button 페이지의 Button 컴포넌트 인스턴스 사용.

Combine as Variants 적용.
네이밍: Data Case / Empty, Data Case / No Results, Data Case / Error, Data Case / Loading, Data Case / No Permission, Data Case / Offline
```
