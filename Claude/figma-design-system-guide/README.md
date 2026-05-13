# Figma Design System Guide

Vetching 디자인 시스템을 Figma에서 작성·유지보수하기 위한 규칙 모음.

**문서 의도**: 페이지 구분, 정렬, 배치 등을 사람이 보기 좋게 정돈하는 것을 핵심으로 하되, 이를 뒷받침하는 컴포넌트 작성·토큰 바인딩·문서 작성 메타 규칙도 함께 정리한다.

## 파일 구성

| 파일 | 다루는 내용 |
|---|---|
| [01-page-structure.md](01-page-structure.md) | 페이지 네이밍, 전체 페이지 구조, Cover · Change Log 페이지 양식, 페이지 내 메타 박스 금지 정책 |
| [02-frame-and-layout.md](02-frame-and-layout.md) | 흰색 카드 프레임 스펙, 페이지 내 배치 간격, 변형 그리드 배치 규칙 (계층 기반 배치, 페이지 레이아웃 좌표, 패딩 검증) |
| [03-component-authoring.md](03-component-authoring.md) | 컴포넌트 Sizing (HUG/FILL/FIXED), Variants 구성 (Component Set), Variants 네이밍, T-Shirt 사이즈 표기 |
| [04-token-binding.md](04-token-binding.md) | Size · Spacing · Radius 토큰 바인딩 원칙, 타이포그래피 Text Style 적용 규칙 |
| [05-doc-conventions.md](05-doc-conventions.md) | md 문서 국문 작성 규칙, 아이콘 사용 공통 규칙 (기호 텍스트 금지) |
| [06-figma-mcp-snippets.md](06-figma-mcp-snippets.md) | Figma MCP(`use_figma`)로 일괄 적용하는 자동화 스크립트 모음 |
| [CHANGELOG.md](CHANGELOG.md) | 버전 이력 + SemVer 기반 버전 부여 정책 + Figma `Change Log` 페이지 동기화 정책 |

## 문서 수정 시 유의사항

- 가이드 문서를 수정하면 [CHANGELOG.md](CHANGELOG.md)에 항목을 추가하고, 같은 내용을 Figma `Change Log` 페이지에도 동기화한다.
- 페이지·카드 프레임에는 정책·노트·버전 콜아웃 등 메타 텍스트를 두지 않는다. ([01-page-structure.md#페이지-내-메타-박스-금지](01-page-structure.md#페이지-내-메타-박스-금지))
- 가이드 외에 단일 컴포넌트별 세부 사양은 [`../design-system/components/{NN}-{name}.md`](../design-system/components/) 파일을, 파운데이션 토큰 정의는 [`../design-system/foundations/`](../design-system/foundations/) 파일을 참조한다.
