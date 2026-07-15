# KGAI Wiki Log

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
