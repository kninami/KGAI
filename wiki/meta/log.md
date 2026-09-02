# KGAI Wiki Log

## [2026-09-02] deletion | `guidelines/민주화운동_홍보물_제작가이드라인.md` 삭제
- 삭제: `wiki/guidelines/민주화운동_홍보물_제작가이드라인.md` (149줄, status: draft, 작성 2026-07-27)
- 사유: 이 위키의 scope는 성인지 감수성 기준(성평등 홍보물·사건 보도 표현)이다. 해당 문서는 KGAI의 제작 프로세스·체크리스트·FAQ **구성 형식만 빌려** 민주화운동 기념·전시·교육자료 제작 기준을 새로 쓴 응용 초안이었고, 근거 source(`raw/`)가 없는 자체 생성물이었다. canonical 문서와 연결되지 않는 별도 주제 문서가 legacy 폴더에 남아 있으면 질의응답 시 근거 우선순위를 흐린다.
- 영향 범위: 없음. `checklists.md`, `guidelines.md`, `sources/*`, `terms/*`, `meta/index.md` 어디에서도 이 문서를 참조하지 않았다(전체 grep 확인). 문서가 참조하던 `[[guidelines]]`, `[[checklists]]`, `[[guidelines/성평등_홍보물_제작프로세스_및_FAQ]]` 는 단방향 링크였으므로 남은 페이지에 깨진 링크가 생기지 않는다.
- canonical 반영분: 없음. 이 문서의 내용은 애초에 `checklists.md`·`guidelines.md` 에 병합된 적이 없다. 성평등 관점의 폭력·피해 재현 기준은 `guidelines.md` 4장(폭력·범죄 사건의 표현과 보도)에 이미 독립적으로 정리되어 있다.
- 커밋 상태 메모: 이 파일은 git에 커밋된 적이 없는 untracked 문서였다. 필요하면 이 로그의 사유를 근거로 재작성해야 하며, 그 경우 위키 scope 확장 여부를 먼저 결정한다.

## [2026-09-02] tooling | /ingest, /review 를 실제 스킬로 등록
- 사유: AGENT.md 본문에 `/ingest`, `/review` 를 적어 둔 것만으로는 어떤 도구도 명령어로 인식하지 못함. 실행 가능한 정의 파일이 없었다.
- 생성: `.claude/skills/ingest/SKILL.md` — AGENT.md의 Ingest Workflow와 중복 판단 기준을 실행 절차로 이전. PDF 추출 방법, source summary 필수 4개 절, terms 묶음 페이지 컨벤션, stale 링크 주의 등 실제 ingest에서 필요한 사항 포함.
- 생성: `.claude/skills/review/SKILL.md` + `TEMPLATE.md` — 검토 절차와 **고정 출력 서식**. 모든 review는 TEMPLATE 서식(검토 개요 / 종합 판정 / 지적 사항 / 용어 교정 / 수정본 / 판단 보류 / 근거 추적)으로 산출한다. 심각도는 필수 수정·권장 수정·참고 3단계.
- 생성: `CLAUDE.md` — 자동 로딩되는 진입점. AGENT.md를 import하고 작업 종류별 스킬 진입점, 질의응답 우선순위, 불변 규칙을 명시. (Claude Code가 자동으로 읽는 파일명은 CLAUDE.md이며 AGENT.md는 자동 로딩되지 않는다.)
- 갱신: `AGENT.md` Ingest/Review Workflow 절에 스킬 파일 위치 명시. 정책 기준은 AGENT.md, 실행 절차는 스킬로 역할 분리.
- 메모: AGENT.md는 삭제하거나 이름을 바꾸지 않고 스키마 정의 문서로 유지.

## [2026-09-01] ingest | 여성폭력 사건보도 자료 2건 → 사건 보도 영역 신설
- 신규 source: `sources/성희롱_성폭력_스토킹_사건보도_참고수첩` ← `raw/reports/sexual violence.pdf` (여성가족부, 2024)
- 신규 source: `sources/여성폭력_사건보도_권고기준` ← `raw/「여성폭력 사건보도 권고기준 1.0」 5대 원칙 및 행동강령.md`
- `checklists.md`: 매체별 섹션 「여성폭력 사건 보도 및 사건 관련 콘텐츠」 신설 (취재·인터뷰 / 신원 노출 방지 / 기사 작성·편집 / 삽화·사진·영상 / 정확성과 사후 조치 / 디지털 성범죄 보도 / 구조적 접근과 지원 정보 7개 항목군).
- `checklists.md`: 공통 5절(폭력·범죄·피해 재현) 기존 항목 보강 — 피해자 책임 전가 범위 확대, 가해 방법 묘사, 피해자다움 편견 삽화, 가해자 악마화, 심각성 희석 표현 추가. 방송 섹션 '데이트 폭력' → '교제폭력(데이트 폭력), 스토킹'.
- `guidelines.md`: 4장을 「폭력·범죄 사건의 표현과 보도」로 확장 — 5대 원칙, 피해자 신원 보호(노출 위험 정보 표), 피해자다움 편견, 가해자 타자화 금지, 선정성·재현, 따옴표 저널리즘과 사후 조치, 디지털 성범죄 관리 책임, 지원기관 안내.
- `guidelines.md`: 8장 「폭력 유형 개념 구분」 신설(성희롱/성폭력, 디지털 성폭력, 스토킹, 교제폭력, 가정폭력, 2차 피해). 기존 8장 판단 메모 → 9장으로 이동, 잘못된 법률상식 기반 메모 6건 추가.
- `terms/` 13건 신설: OO녀_OO남, 꽃뱀, 몹쓸짓_검은손_나쁜입, 음란물, 딥페이크, 짐승_늑대_악마, 발바리_발정난개, 성관계_성추문, 성폭행, 더듬는, 더러운욕망, 사랑싸움, 데이트폭력.
- `terms/` 2건 보강: 몰래카메라('몰카' 줄임말과 시정권고 사례 추가), 리벤지포르노(권장어 '불법 촬영물/불법 유포물' 병기, 촬영 동의와 유포 책임 구분). 두 페이지의 stale 링크(`checklists#서울교육 성평등 자가진단표`)도 현행 앵커로 교체.
- 중복 처리: 피해자 비난 금지, 성별 자동 배정 금지, 선정적 재현 금지 등 기존 공통 항목과 겹치는 내용은 새 항목을 만들지 않고 기존 문장을 더 구체적으로 보강하는 선에서 처리. 두 source가 겹치는 원칙(구조적 원인, 선정성, 피해자 보호)은 더 구체적인 수첩 기준으로 한 번만 적재.
- 미반영: 수첩 부록(한국기자협회 인권보도준칙, 성폭력 범죄보도 세부 권고 기준, 기자협회 윤리강령, 언론중재위 시정권고 심의기준, 방통심의위 방송심의 규정)은 외부 규범 원문 전재라 옮기지 않음. 성희롱 행위유형 예시, 성폭력 죄명별 구성요건, 가정폭력 사건 처리절차 흐름도 등 법률 실무 상세는 위키 범위(산출물 제작 시 점검) 밖이라 개념 수준으로만 요약.
- 범위 확장 메모: 위키 scope에 '여성폭력 사건 보도'가 추가됨. 대상은 언론사만이 아니라 폭력 사건을 다루는 공공 보도자료·브리핑·카드뉴스·영상·캠페인 전반으로 잡았다.
- 모순 없음

## [2026-07-15] consolidation update | source별 정리 → 통합 canonical 문서
- 재작성: `wiki/checklists.md` 를 출처별 섹션 모음이 아니라 중복 제거된 단일 체크리스트로 전환.
- 재작성: `wiki/guidelines.md` 를 출처별 설명 모음이 아니라 단일 가이드라인으로 전환.
- 재작성: `wiki/sources/*.md` 를 "원문 요약 + 통합본에 새로 추가된 내용 + 중복 처리 내용" 중심으로 전환.
- 재작성: `AGENT.md` 를 net-new only ingest 정책 기준으로 갱신.
- 재작성: `wiki/meta/index.md` 를 canonical 문서 중심 index로 단순화.

## [2026-07-15] content migration | legacy checklists/guidelines → canonical singleton docs
- 이관: `wiki/checklists/` 4개 문서 본문을 `wiki/checklists.md` 섹션 4개로 병합.
- 이관: `wiki/guidelines/` 3개 문서 본문을 `wiki/guidelines.md` 섹션 3개로 병합.
- 생성: `wiki/sources/` 4개 source summary (`2026년_성별영향평가_지침`, `서울교육_성평등_한_뼘_더하기`, `경기도_성평등_홍보물_길라잡이`, `양성평등_방송프로그램_제작_안내서`).
- 갱신: `wiki/meta/index.md` canonical 상태 반영.
- 메모: legacy 문서는 삭제하지 않고 참조용으로 유지.

## [2026-07-14] schema revision | singleton checklists/guidelines + sources layer
- 사유: `checklists/`, `guidelines/`를 폴더형 페이지 컬렉션이 아니라 각각 단일 집계 문서(`checklists.md`, `guidelines.md`)로 관리하고, 원본 문서 요약은 `sources/`로 분리하는 구조가 더 적합하다고 판단.
- 변경: `AGENT.md`를 새 스키마 기준으로 전면 재작성.
- 생성: `wiki/checklists.md`, `wiki/guidelines.md` placeholder.
- 생성: `wiki/sources/` 디렉터리.
- 메모: 기존 `wiki/checklists/`, `wiki/guidelines/` 산출물은 legacy 상태로 간주하며, 이후 작업 시 canonical 문서로 순차 이관.

## [2026-07-14] 스키마 재설계 | checklists/guidelines/terms 3종 체계로 단순화
- 사유: topics/formats/precedents/drafts 5종 체계가 이 위키의 실제 목적(성인지 감수성 가이드라인 자료집)에 비해 과도하게 복잡함. raw 자료 4건이 모두 정책 지식이 아니라 "체크리스트 + 설명형 가이드 + 언어사전"으로만 구성되어 있었던 점도 확인.
- 삭제: wiki/topics/성별영향평가.md, wiki/formats/*.md(4개), wiki/precedents/, wiki/drafts/ (빈 폴더 포함), raw/laws · raw/stats · raw/precedents · raw/brand (빈 폴더, raw/는 평평한 구조로 유지)
- terms/ 재정의: 법적 정의·통계 페이지 → 성평등 언어사전의 개별 단어(성차별 표현 → 성평등 표현) 페이지로 전환. 기존 5개 페이지 삭제.
- guidelines/ 재정의: 6번째 페이지 타입에서 다시 분화 — 실행형 점검표는 `checklists/`로, 원칙·설명·FAQ는 `guidelines/`로 분리. 기관이 다른 체크리스트는 병합하지 않고 각각 별도 페이지 유지.
- AGENT.md 전면 재작성.

## [2026-07-14] ingest 재정리 | 4개 원본 문서 → checklists 4 + guidelines 3 + terms 20
- checklists/정부홍보사업_성별영향평가_점검표.md ← (최종) 2026년 성별영향평가 지침.pdf
- checklists/서울교육_성평등_자가진단표.md ← 서울교육+성평등+한+뼘+더하기(PDF배포용).pdf
- checklists/경기도_성평등_홍보물_사전체크리스트.md ← 경기도성평등홍보물길라잡이.pdf
- checklists/방송심의_양성평등_체크리스트.md ← 양성평등 방송 프로그램 제작 안내서 최종본.pdf
- guidelines/성평등_인물표현_가이드.md ← 경기도성평등홍보물길라잡이.pdf, 서울교육+성평등+한+뼘+더하기.pdf
- guidelines/성평등_홍보물_제작프로세스_및_FAQ.md ← 서울교육+성평등+한+뼘+더하기.pdf, 경기도성평등홍보물길라잡이.pdf
- guidelines/양성평등_방송프로그램_제작가이드.md ← 양성평등 방송 프로그램 제작 안내서 최종본.pdf
- terms/ 20개 ← 서울교육 12개 항목 + 경기도 12개 항목 (중복 5개 병합: 녹색어머니회, 맘카페, 유모차, 저출산, 미혼)
- 미반영: 「2026년 성별영향평가 지침」의 법령/계획/사업/자가진단형 성별영향평가 절차·서식(법적 정의, 작성 예시 등)은 이번 재설계에서 위키 범위를 "산출물 제작 시 성인지 감수성 점검"으로 좁히면서 제외. 필요 시 별도 스코프로 재검토.
- 모순 없음

