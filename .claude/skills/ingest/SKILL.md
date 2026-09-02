---
name: ingest
description: raw/ 에 추가된 원본 자료(PDF, MD)를 KGAI 위키의 canonical 문서에 net-new only 원칙으로 통합한다. "ingest 해줘", "raw에 새로 넣은 거 반영해줘", "/ingest <파일>" 처럼 새 원본 자료를 위키에 반영해 달라는 요청에 사용한다.
---

# Ingest — 새 source를 통합본에 반영

이 스킬은 `AGENT.md` 의 스키마와 원칙을 실행 절차로 옮긴 것이다. 원칙에 이견이 생기면 `AGENT.md` 가 기준이다.

## 핵심 원칙

목표는 출처별 문서를 쌓는 것이 아니라, **하나의 완성된 체크리스트와 하나의 완성된 가이드라인**을 계속 다듬는 것이다.

- `wiki/checklists.md` 와 `wiki/guidelines.md` 는 각각 canonical 단일본으로 유지한다.
- source가 여러 개여도 canonical 문서 안에 출처별 섹션을 병렬 적재하지 않는다.
- 새 source는 기존 canonical 문서와 비교해 **net-new만** 추가한다.
- provenance는 `wiki/sources/*.md` 에 남기고, canonical 본문은 실사용성을 우선한다.
- `raw/` 는 절대 수정·삭제하지 않는다.

## 절차

### 0. 대상 확인

파일이 지정되지 않았으면 `git status --short raw/` 와 `find raw -type f` 로 새로 들어온 항목을 찾는다. 여러 건이면 모두 처리하고, 서로 영역이 겹치는지 먼저 판단한다.

### 1. 원본 읽기

PDF는 레이아웃을 살려 추출한다. 스크래치패드에서 작업한다.

```bash
pdftotext -layout "raw/reports/<파일>.pdf" sv.txt
sed 's/^[[:space:]]*//; s/[[:space:]]*$//' sv.txt | grep -v '^$' > sv2.txt
grep -n "^0[0-9] \|^[ⅠⅡⅢⅣ]\|체크리스트\|목차\|CONTENTS" sv2.txt   # 섹션 지도 만들기
```

한 번에 다 읽지 말고 섹션 지도를 먼저 뽑은 뒤 구간별로 읽는다. 머리말·꼬리말이 반복되면 `grep -v` 로 걸러야 읽을 만해진다.

문서 목적, 적용 대상, 매체 범위, 발행 기관, 발행 연도를 파악한다. 발행 연도는 판권지나 집필진 명단에 있는 경우가 많다.

### 2. 기존 통합본 읽기

**반드시 순서대로 먼저 읽는다.** 이걸 건너뛰면 중복 판단이 불가능하다.

1. `wiki/checklists.md`
2. `wiki/guidelines.md`
3. `wiki/meta/index.md` (기존 term 목록 확인)
4. 관련 있어 보이는 `wiki/terms/*.md`
5. 형식 참고용으로 기존 `wiki/sources/*.md` 하나

### 3. diff 판단

| 판단 | 조건 | 처리 |
|------|------|------|
| **중복** | 표현만 다르고 금지·권장 취지가 같다 | 추가하지 않음 |
| **중복** | 더 큰 범주의 기존 항목에 이미 포함된다 | 추가하지 않음 |
| **중복** | 기존 FAQ의 판단 논리를 반복한다 | 추가하지 않음 |
| **보강** | 같은 취지인데 새 source가 더 구체적이다 | 기존 문장을 강화 (새 항목 만들지 않음) |
| **순증** | 기존에 없는 매체 전용 기준이 있다 | 새 항목·새 섹션 추가 |
| **순증** | 더 구체적인 화면 구성·용어·제작 절차 기준이 있다 | 새 항목 추가 |
| **순증** | 기존에 없던 집단·상황을 다룬다 | 새 섹션 추가 |

source가 2건 이상이고 영역이 겹치면, 더 구체적인 쪽 기준으로 **한 번만** 적재하고 나머지는 순증분만 가져온다.

### 4. `wiki/sources/<이름>.md` 작성

```yaml
---
source_title: 문서 제목
issuing_body: 발행 기관
raw_file: raw/reports/원본.pdf
document_type: [checklist, guideline, term]
published: 2024
updated: <오늘 날짜>
---
```

본문 필수 4개 절:

- `## 문서 개요` — 구성과 성격. 이 위키에서 이 source를 어떤 용도로 쓰는지까지 명시
- `## 통합본에 새로 반영한 내용` — `### checklists.md` / `### guidelines.md` / `### terms/` 로 나눠 기술
- `## 중복이라 별도 추가하지 않은 내용` — **생략 금지.** 다음 ingest 때 판단 근거가 된다
- `## 연결 문서` — `[[checklists]]`, `[[guidelines]]`, 관련 source

원문에 있지만 위키 범위 밖이라 뺀 것도 여기 남긴다. 나중에 "왜 안 들어갔지"를 다시 조사하지 않게 된다.

### 5. canonical 문서 갱신

**`wiki/checklists.md`**
- 공통 체크리스트는 새 항목을 늘리기보다 기존 항목 보강을 우선한다
- 매체 전용 기준은 `## 2. 매체별 추가 체크포인트` 아래 새 `###` 섹션으로
- 각 섹션 머리에 `_근거 source: ..._` 표기
- 항목은 `- [ ] ~하고 있지 않은가` / `~했는가` 형태의 점검 질문으로 통일

**`wiki/guidelines.md`**
- 같은 원칙 반복 금지. 기존 장을 정교하게 만드는 쪽을 먼저 시도한다
- 완전히 새로운 판단 영역일 때만 새 장을 만들고, **뒤 장 번호를 모두 밀어야 한다**
- FAQ성 내용은 맨 뒤 `판단 메모` 장에 `### 질문형 제목` 으로 추가

두 파일 모두 frontmatter의 `updated`, `source_pages`, 필요하면 `scope` 를 갱신한다.

### 6. `wiki/terms/` 갱신

- 이미 있는 단어면 **새 파일을 만들지 않는다.** `official_source`, `source_pages`, `replacement` 병기, 본문 보강으로 처리
- 원문 표에서 하나의 행이 여러 표현을 묶고 사유가 같으면 한 페이지로 만든다 (`여학생_여교사_여직원.md`, `짐승_늑대_악마.md` 가 이 패턴)
- 권장어가 없는 경우 `replacement: 사용 자제 (대체 표현)` 로 적는다
- 파일 형식:

```yaml
---
term: 원 표현
replacement: 권장 표현
reason: 한 줄 사유
official_source: 발행처 「문서명」(연도)
source_pages: [sources/<source 이름>]
updated: <오늘 날짜>
---
```

본문은 `## 개선 이유` + `## 관련 페이지`. 관련 페이지 링크는 **실제 존재하는 앵커**여야 한다. 통합 과정에서 사라진 옛 섹션명을 가리키는 stale 링크가 남아 있으니, 건드리는 페이지에서 발견하면 함께 고친다.

### 7. `wiki/meta/` 갱신

- `index.md` — 상단 카운트(Sources, Terms), Sources 표, Terms 표. 보강만 한 term은 출처 열에 새 source를 덧붙인다
- `log.md` — 최상단에 새 항목 추가 (역순 정렬). 형식:

```markdown
## [YYYY-MM-DD] ingest | <한 줄 요약>
- 신규 source: ...
- `checklists.md`: ...
- `guidelines.md`: ...
- `terms/` N건 신설: ...
- `terms/` N건 보강: ...
- 중복 처리: ...
- 미반영: ...
- 모순 없음
```

## 절대 하지 말 것

- source별 checklist/guideline을 canonical 문서에 그대로 병렬 복붙
- 표현만 다른 중복 항목 늘리기
- 이미 있는 term을 새 파일로 중복 생성
- diff 없이 전부 추가
- provenance를 canonical 본문에 밀어 넣어 실사용성 해치기
- `raw/` 파일 수정·삭제

## 마무리 보고

무엇을 순증으로 넣고 무엇을 중복으로 뺐는지, 판단이 갈렸던 지점(위키 scope 확장 등)을 사용자에게 명시한다. 조용히 범위를 넓히지 않는다.
