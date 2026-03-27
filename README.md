# ZELVIA GLSI 2.0
## 수업 중 교사 관찰을 자동으로 데이터화 — 학원만을 위한 AI 학습관리 시스템

> **개발자·외주 업체 인수인계용 기술 기준 문서**
> 새 개발자가 합류하거나 외주를 줄 때 이 문서를 기준으로 삼으세요.

---

## 핵심 기술 철학

교육 현장의 비정형 데이터를 AI로 정량화하여 학습 상태 지수를 산출하는 에듀테크 데이터 플랫폼.
단순 학원 관리 앱이 아닙니다.

---

## 핵심 알고리즘

### 1. GLSI 6축 알고리즘 (특허 청구항 1·2번)
비정형 교육 관찰 데이터의 정량적 지수화 엔진

- 이론: Zimmerman(2000) 자기조절학습 + Black & Wiliam(1998) 형성평가
- 6축: HABIT · COGNITIVE · TIME · ACHIEVEMENT · GROWTH + EI 보정
- 파이프라인: 음성 STT → 키워드 매핑 → 6축 점수 산출
- DB 키: glsi_students_v2, glsi_records_v2, glsi_cfg_v2

### 2. MLL 수학 문해력 손실 지수 (특허 청구항 6번)
다차원 오답 패턴 분석을 통한 학습 장애 요인 자동 탐지

공식: (독해실패 오답 수 / 전체 오답 수) × (문장 평균 길이 / 기준값 20)

오답 5분류: 계산실수 · 개념부족 · 독해실패 · 응용실패 · 단순실수
독해실패 30% 이상 → 문해력 병목 경고 자동 발동
Phase 2 목표: 문제 텍스트 길이 + 풀이 시간 교차 → 독해실패 자동 추정
DB 키: glsi_omr_bridge_v1

### 3. ICMM 역설 교수법 자동화 (특허 청구항 7번)
인지 부하 이론(Cognitive Load Theory) 기반 수학 문장제 해체 알고리즘

Interactive Context-Math Mapping:
수학 오답 → AI가 국어 3단계로 변환
1단계: 정보 추출 / 2단계: 사실 확인 / 3단계: 논리 추론
→ 이해 후 수학 재도전 → 독해 완료 로그 → GLSI 연동
저작권 안전: 문제 원본 저장 없음, 질문 구조만 변환
DB 키: glsi_paradox_log_v1

### 4. 끊어 읽기 자동 가이드
문장을 조건 / 변화 / 질문 단위로 자동 분절
AI 없이도 규칙 기반으로 작동 (폴백 구조)

---

## 앱 구성

| 파일 | 역할 | 핵심 기능 |
|------|------|---------|
| index.html | 메인 포털 | 역할 선택(원장·교사·학생)·연동 상태 확인 |
| glsi.html | GLSI v9 허브 | 6축 측정·대시보드·이탈 위험 감지·MLL 리포트 |
| attendance.html | 출석관찰부 v3 | 음성 STT 관찰 기록·GLSI 자동 연동 |
| omr.html | OMR v2 | 숙제모드·5분류·역설교수법·끊어읽기 |
| diagnosis.html | 수학진단 v2 | 단원별 진단·끊어읽기·25개 단원 |
| intake.html | 입회테스트 v12 | 학습유형 분류·GLSI 초기값 설정 |
| report.html | 상담리포트 | 월간 자동생성·MLL 지수 포함 |

---

## localStorage 연동 키 (앱 간 데이터 공유 구조)

| 키 | 공유 앱 | 설명 |
|---|---|---|
| glsi_students_v2 | 전체 | 학생 마스터 데이터 |
| glsi_records_v2 | GLSI·리포트 | GLSI 측정 기록 |
| glsi_cfg_v2 | 전체 | API 키·설정 |
| glsi_omr_bridge_v1 | GLSI·OMR | OMR 성적→GLSI 연동 |
| zelvia_att_bridge_v1 | GLSI·출석 | 관찰→GLSI 연동 |
| zelvia_omr_books | OMR | 문제집·정답 |
| zelvia_admission_test | GLSI·입회 | 입회테스트 결과 |
| glsi_paradox_log_v1 | OMR | 역설교수법 완료 로그 |

⚠️ 반드시 같은 브라우저에서 모든 앱 실행 (크롬 또는 삼성 인터넷)

---

## Phase 2 개발 목표 (클라우드 SaaS 전환)

현재: localStorage 기반 로컬 HTML (TRL 4~5)
목표: Supabase(PostgreSQL) + React/Next.js + Anthropic API (TRL 7)

핵심 과제:
- localStorage → 클라우드 DB 마이그레이션
- 역할별 JWT 인증 (원장·교사·학생·학부모)
- 다기기 실시간 동기화
- 독해실패 자동 탐지 알고리즘 (문장 길이 + 풀이 시간)
- 시계열 통합 대시보드 (입회→졸업 성장 곡선)

---

## 배포 (GitHub Pages)

1. github.com → New repository → 이름: zelvia → Public
2. 파일 7개 업로드 → Commit
3. Settings → Pages → Branch: main → Save
4. URL: https://[계정명].github.io/zelvia/

---

## IP 현황

특허 청구항 7개 출원 예정 (IP나래 프로그램 연계)
⚠️ 외부 개발자 합류 시 반드시 NDA 체결 후 코드 공개

개발: 조남실 / 주식회사 젤비아 (설립 준비 중) / 파일럿: 남실학원
