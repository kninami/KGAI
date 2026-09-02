# KGAI Wiki

공무원이 실무에서 바로 쓸 수 있는 **하나의 완성된 체크리스트와 하나의 완성된 가이드라인**을 계속 다듬어 가는 위키다. 출처별 문서를 많이 쌓는 것이 목표가 아니다.

스키마와 컨벤션 전문은 `AGENT.md` 에 있다.

@AGENT.md

## 작업 종류별 진입점

| 요청 | 사용할 스킬 |
|------|-------------|
| `raw/` 의 새 자료를 위키에 반영 | `ingest` (`.claude/skills/ingest/`) |
| 산출물 성인지 감수성 검토 | `review` (`.claude/skills/review/`) — 출력은 반드시 `TEMPLATE.md` 서식 |

슬래시로 `/ingest`, `/review` 를 쳐도 되고, "raw에 넣은 거 ingest 해줘" / "이 카드뉴스 검토해줘" 처럼 자연어로 말해도 걸린다.

## 질의응답 우선순위

근거를 찾을 때는 이 순서로 내려간다.

1. `wiki/checklists.md`
2. `wiki/guidelines.md`
3. `wiki/terms/*.md`
4. 필요할 때만 `wiki/sources/*.md`

먼저 canonical 답을 주고, 사용자가 근거를 원할 때 source summary로 provenance를 덧붙인다. 출처가 여러 개여도 답변은 통합된 실무 기준 하나로 제시한다.

## 불변 규칙

- `raw/` 는 읽기 전용이다. 수정·삭제하지 않는다.
- `checklists.md`, `guidelines.md` 는 각각 canonical 단일본이다. 출처별 섹션을 병렬 적재하지 않는다.
- 새 source는 기존 통합본과 diff 해서 **net-new만** 추가한다. 같은 취지면 새 항목을 만들지 말고 기존 문장을 보강한다.
- 이미 있는 term은 새 파일을 만들지 않고 기존 페이지를 보강한다.
- `wiki/checklists/`, `wiki/guidelines/` 폴더는 legacy reference다. 새 작업은 `checklists.md`, `guidelines.md`, `sources/` 에 반영한다.
