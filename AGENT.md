# Korea Gender AI for Public Official (KGAI) 지식 체계화
# Schema & Workflow Guide

이 파일은 KGAI Wiki의 구조, 컨벤션, 워크플로를 정의한다. 목표는 출처별 문서를 많이 쌓는 것이 아니라, 공무원이 실무에서 바로 사용할 수 있는 **하나의 완성된 체크리스트와 하나의 완성된 가이드라인**을 계속 다듬어 가는 것이다.

---

## 아키텍처 개요

```text
KGAI/
├── raw/
│   └── reports/                # 원본 PDF (source of truth)
│
├── wiki/
│   ├── checklists.md           # 중복 제거된 단일 canonical 체크리스트
│   ├── guidelines.md           # 중복 제거된 단일 canonical 가이드라인
│   ├── sources/                # 원본 문서별 요약 + "무엇이 새로 추가됐는지" 기록
│   ├── terms/                  # 성평등 언어사전 — 단어 하나 = 페이지 하나
│   └── meta/
│       ├── index.md
│       └── log.md
│
└── AGENT.md
```

## 핵심 원칙

- `checklists.md` 와 `guidelines.md` 는 각각 **문서 1개만** canonical 로 유지한다.
- source가 여러 개여도 canonical 문서 안에서는 출처별 섹션으로 병렬 적재하지 않는다.
- 같은 뜻의 체크포인트, 같은 원칙, 같은 FAQ는 하나만 남긴다.
- 새 source를 ingest 할 때는 기존 canonical 문서와 비교해 **net-new 정보만 추가**한다.
- source provenance는 `sources/*.md` 에 남기고, canonical 문서 본문은 실사용성을 우선한다.
- `terms/` 도 동일한 원칙을 따른다. 이미 있는 단어면 새 페이지를 만들지 않고 출처나 설명만 보강한다.
- `raw/reports/` 는 수정하지 않는다.

---

## 문서 타입

### 1. Canonical Checklist (`wiki/checklists.md`)

이 위키의 실행형 점검표 단일본이다.

**역할**

- 공통 체크리스트를 제공한다.
- 매체별 추가 체크포인트를 제공한다.
- 출처별 버전을 병렬 보관하지 않는다.

**작성 규칙**

- 같은 취지의 항목은 문장을 합쳐 하나의 더 강한 항목으로 만든다.
- 새 source가 기존 항목보다 더 구체적이면:
  - 새 항목을 추가하는 대신 기존 항목을 보강한다.
- 새 source가 진짜로 다른 판단 기준을 제시하면:
  - 그때만 새 항목 또는 새 매체별 섹션을 추가한다.

**예시 frontmatter**

```yaml
---
document: KGAI Unified Checklist
status: canonical
merge_policy:
  - dedupe_equivalent_items
  - append_only_net_new_points
source_pages:
  - sources/2026년_성별영향평가_지침
  - sources/서울교육_성평등_한_뼘_더하기
---
```

### 2. Canonical Guideline (`wiki/guidelines.md`)

이 위키의 설명형 판단 기준 단일본이다.

**역할**

- 왜 문제가 되는지 설명한다.
- 좋은 적용 방식, FAQ, 제작 프로세스를 정리한다.
- checklist를 실무적으로 해석할 수 있도록 돕는다.

**작성 규칙**

- 출처별 문단을 나열하는 방식보다, 공통 원칙을 먼저 통합한다.
- 출처가 추가될 때는:
  - 기존 원칙과 같은 말이면 추가하지 않는다.
  - 더 구체적인 예시, 더 좁은 매체 기준, 더 강한 금지 기준이면 기존 문단을 보강한다.
  - 완전히 새로운 판단 영역이면 새 섹션을 만든다.

### 3. Source Summary (`wiki/sources/*.md`)

원본 PDF 1개당 `.md` 1개를 둔다. 이 문서의 역할은 **원문 요약**이면서 동시에 **이번 source가 canonical 문서에 무엇을 새로 기여했는지 기록하는 것**이다.

**반드시 포함할 내용**

- 문서 개요
- 통합본에 새로 반영한 내용
- 중복이라 별도 추가하지 않은 내용
- 연결된 canonical 문서

**예시 frontmatter**

```yaml
---
source_title: 경기도 성평등 홍보물 길라잡이
issuing_body: 경기도 · 경기도여성가족재단
raw_file: raw/reports/경기도성평등홍보물길라잡이.pdf
document_type:
  - checklist
  - guideline
  - term
updated: 2026-07-15
---
```

### 4. Terms (`wiki/terms/*.md`)

성차별 표현 하나 = 페이지 하나.

**작성 규칙**

- 이미 존재하는 term이면 새 파일을 만들지 않는다.
- 새 source가 더 나은 권장 표현, 더 정확한 이유, 추가 출처를 제공하면 기존 file을 보강한다.

---

## Ingest Workflow

사용자가 할 일:

```text
/ingest raw/reports/새문서.pdf
```

AI가 할 일:

1. 원본 PDF를 읽고 문서 목적, 적용 대상, 매체 범위를 파악한다.
2. 기존 `checklists.md`, `guidelines.md`, 관련 `terms/` 를 먼저 읽는다.
3. 새 source 내용과 기존 canonical 문서를 비교한다.
4. `sources/*.md` 를 만들고 아래처럼 정리한다.
   - canonical 에 새로 추가한 것
   - 기존과 중복이라 추가하지 않은 것
5. `checklists.md` 는 다음 규칙으로 갱신한다.
   - 같은 항목이면 추가하지 않음
   - 더 구체적이면 기존 항목 문장 보강
   - 완전히 새로운 기준이면 새 항목 추가
6. `guidelines.md` 도 같은 규칙으로 갱신한다.
7. `terms/` 도 기존 term과 diff 해서 새 term 또는 보강 여부를 결정한다.
8. `wiki/meta/index.md` 와 `wiki/meta/log.md` 를 갱신한다.

---

## 중복 판단 기준

다음 중 하나면 **중복**으로 본다.

- 표현만 다르고 금지 또는 권장 취지가 같다.
- 더 큰 범주의 기존 항목 안에 이미 포함된다.
- 기존 FAQ의 판단 논리를 반복한다.

다음 중 하나면 **순증**으로 본다.

- 기존 문서에 없는 매체 전용 기준이 있다.
- 기존보다 더 구체적인 화면 구성, 용어, 제작 절차 기준이 있다.
- 기존에 없던 집단 또는 상황(예: 방송 전용 폭력 재현 기준, 픽토그램 규칙)을 다룬다.

---

## Query Workflow

질의응답 시 우선순위:

1. `checklists.md`
2. `guidelines.md`
3. 관련 `terms/*.md`
4. 필요한 경우에만 `sources/*.md`

답변 원칙:

- 먼저 canonical 답을 준다.
- 사용자가 근거를 원하면 source summary로 provenance를 덧붙인다.
- 출처가 여러 개라도 답변은 통합된 실무 기준으로 제시한다.

---

## Review Workflow

`/review` 요청 시:

1. 산출물 유형에 맞는 canonical checklist 항목을 대조한다.
2. 위반 가능성이 있으면 canonical guideline 원칙으로 설명한다.
3. 용어 문제는 `terms/`에서 교정한다.
4. 사용자가 원하면 어떤 source가 그 판단을 강화했는지 `sources/`까지 추적해 보여준다.

---

## index.md 구조

```markdown
# KGAI Wiki Index

## Canonical Docs
| 문서 | 설명 |
|------|------|
| [[checklists]] | 중복 제거된 단일 체크리스트 |
| [[guidelines]] | 중복 제거된 단일 가이드라인 |

## Sources
| 페이지 | 원본 PDF | 통합본에 새로 반영한 핵심 |
|--------|----------|----------------------------|
| [[sources/경기도_성평등_홍보물_길라잡이]] | 경기도성평등홍보물길라잡이.pdf | 시각 배치, 픽토그램, 캐릭터 기준 |
```

## log.md 구조

```markdown
## [2026-07-15] merge policy update
- 변경: source별 섹션 병렬 적재 방식 폐기
- 변경: canonical checklist/guideline 단일본 유지
- 원칙: 새 source는 net-new만 추가
```

---

## 절대 하지 말 것

- source별 checklist/guideline을 canonical 문서 안에 그대로 병렬 복붙하기
- 표현만 다른 중복 항목을 계속 늘리기
- 이미 있는 term을 새 파일로 중복 생성하기
- 새 source가 들어올 때 diff 없이 전부 추가하기
- provenance를 canonical 본문에 과도하게 밀어 넣어 실사용성을 해치기
- `raw/reports/` 파일을 수정하거나 삭제하기
