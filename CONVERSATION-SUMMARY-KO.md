# 💬 andrej-karpathy-skills 대화 정리 (한국어)

> Claude Code 세션에서 진행한 레포 전수조사 및 Q&A 대화를 정리한 문서입니다.
> 작성일: 2026-10-01

## 🔗 GitHub 주소

| 구분 | URL |
|---|---|
| 이 레포 (포크) | https://github.com/bmshin94/andrej-karpathy-skills |
| 원본 레포 (upstream) | https://github.com/forrestchang/andrej-karpathy-skills |
| 근거 출처 (Andrej Karpathy X 포스트) | https://x.com/karpathy/status/2015883857489522876 |
| 원작자 관련 프로젝트 (Multica) | https://github.com/multica-ai/multica |

---

## 1. 레포 분석 — 뭐 하는 건지

**"AI 코딩 도우미(Claude Code, Cursor)가 자주 하는 실수 4가지를 막는 행동 규칙서"**

- 실행 코드 0줄, Markdown + JSON 파일로만 구성 → "AI에게 주는 업무 매뉴얼"
- Andrej Karpathy가 X에 쓴 LLM 코딩 실수 관찰을 forrestchang이 규칙 파일로 정리, `bmshin94`가 포크

### 폴더 구조

```
andrej-karpathy-skills/
├── .claude-plugin/
│   ├── marketplace.json   (29줄)  플러그인 마켓 카탈로그
│   └── plugin.json        (11줄)  플러그인 정의 → skills/karpathy-guidelines
├── skills/karpathy-guidelines/
│   └── SKILL.md           (67줄)  플러그인 설치 시 쓰이는 스킬 본문
├── .cursor/rules/
│   └── karpathy-guidelines.mdc (70줄)  Cursor용 규칙 (alwaysApply: true)
├── CLAUDE.md              (90줄)  프로젝트 자동 적용 규칙 + 카리나 페르소나(포크에서 추가)
├── EXAMPLES.md           (522줄)  잘못한 예 / 잘한 예 실전 사례집
├── README.md / README.zh.md (171줄씩)  영어 / 중국어 설명서
├── CURSOR.md              (28줄)  Cursor 연동 가이드
├── ANALYSIS-KO.md        (634줄)  이전 세션의 한국어 분석 리포트
└── CONVERSATION-SUMMARY-KO.md      이 문서
```

- 같은 4원칙이 `CLAUDE.md` / `SKILL.md` / `.mdc` 세 곳에 복사되어 있음 (도구마다 읽는 파일이 다름)
- 포크의 **CLAUDE.md에만** 카리나 페르소나가 있음 → 플러그인 설치 시(SKILL.md)에는 페르소나 미포함

### 해결하려는 문제 (Karpathy 지적)
1. 멋대로 가정하고 확인하지 않음
2. 과하게 복잡하게 만듦 (100줄이면 될 걸 1000줄)
3. 요청과 무관한 코드·주석까지 수정

### 4대 원칙

| 원칙 | 요약 | 예시 (EXAMPLES.md) |
|---|---|---|
| Think Before Coding | 모르면 묻고, 가정은 명시 | "유저 데이터 내보내기" → 범위·필드·포맷 먼저 질문 |
| Simplicity First | 요청한 것만, 최소 코드 | 할인 계산에 클래스 5개 대신 함수 1개 |
| Surgical Changes | 필요한 줄만 수정 | 버그 수정 중 따옴표·타입힌트 변경 금지 |
| Goal-Driven Execution | 검증 가능한 목표로 변환 | "버그 고쳐" → "재현 테스트 작성 → 통과" |

### 언제 쓰나 / 어떤 도움이 되나
- ✅ 기존 프로젝트 유지보수, 버그 수정, 팀 PR 관리, 요구사항이 모호할 때
- ➖ 오타 수정, 일회용 스크립트, 빠른 프로토타입 (속도보다 신중함 쪽 규칙이라)
- 도움: diff가 작고 깔끔해짐 / AI 활용 학습 교재(EXAMPLES.md) / 나만의 규칙 파일 템플릿
- 단점: 질문이 늘어 약간 느려짐, CLAUDE.md만큼 컨텍스트 토큰 소량 사용

## 2. 쉽게 다시 설명

**AI = 똑똑하지만 의욕 과잉인 신입 인턴, 이 레포 = 인턴 책상에 붙이는 업무 수칙 포스트잇**

| 인턴의 실수 | 처방 |
|---|---|
| 묻지도 않고 보고서를 맘대로 정리 | Think Before Coding |
| 커피 한 잔 부탁했는데 카페를 차림 | Simplicity First |
| 창문 닫아달랬더니 가구 재배치 | Surgical Changes |
| "잘 해봐"만 듣고 헤맴 | Goal-Driven ("오타 0개, 3페이지 이내") |

파일 비유: `CLAUDE.md` = 벽 포스터(항상 적용), `SKILL.md` = 서랍 속 매뉴얼(필요할 때 적용), `.mdc` = Cursor용 번역본, `plugin.json`/`marketplace.json` = 표지·목차, `EXAMPLES.md` = 사례집, `README.md` = 사용설명서

## 3. Q&A

### 설치 및 사용법
- **플러그인 (추천)** — Claude Code 안에서:
  ```
  /plugin marketplace add forrestchang/andrej-karpathy-skills
  /plugin install andrej-karpathy-skills@karpathy-skills
  ```
  포크 버전은 첫 줄을 `/plugin marketplace add bmshin94/andrej-karpathy-skills`로 변경
- **CLAUDE.md (프로젝트별, 항상 적용)**:
  ```bash
  curl -o CLAUDE.md https://raw.githubusercontent.com/forrestchang/andrej-karpathy-skills/main/CLAUDE.md
  ```
- **개인 스킬**: `SKILL.md` → `~/.claude/skills/karpathy-guidelines/SKILL.md`
- **Cursor**: `.mdc` → 프로젝트의 `.cursor/rules/`
- **기타 도구**: CLAUDE.md 내용을 `AGENTS.md`, `.github/copilot-instructions.md` 등에 붙여넣기
- 사용: 설치 후 평소처럼 요청. 스킬은 AI가 필요하다고 판단할 때, CLAUDE.md는 항상 적용

### 플러그인? 스킬? MCP?
**스킬을 담은 플러그인 + 규칙 파일. MCP 아님.**

| 종류 | 정체 | 이 레포 |
|---|---|---|
| Skill | AI가 읽는 지침서 | ✅ |
| Plugin | 스킬·명령·훅·MCP 배포 묶음 | ✅ |
| CLAUDE.md / Cursor Rule | 항상 적용되는 프로젝트 지시문 | ✅ |
| MCP | 외부 도구를 연결하는 실행 서버 | ❌ |

### API 토큰 필요?
- 레포 자체는 텍스트 파일 → **API 키 불필요**
- 단, 도구 계정은 필요 (Claude Code: Claude 구독 또는 Anthropic API 키 / Cursor: Cursor 계정)
- CLAUDE.md는 매 요청 컨텍스트에 포함되어 수백~천 토큰 정도 사용
- 직접 만든 앱에서 API로 쓰면 그때는 API 키 필요

### AI 에이전트 구축에 도움?
- 도움 됨, 단 "부품"이지 프레임워크는 아님
- ① 에이전트 코드를 짤 때 품질 향상 ② 직접 만드는 에이전트의 시스템 프롬프트로 활용 ③ "성공 기준을 주고 루프를 돌려라"는 에이전트 설계 원칙
- 도구 연결·메모리·오케스트레이션 기능은 없음 (원작자의 Multica가 그 영역)

### React / PHP로 만들 수 있나?
- A. 레포 자체 → 문서라서 언어와 무관
- B. 활용 서비스 → 가능 (CLAUDE.md 생성기 웹앱: React 프론트 + PHP/Laravel 백엔드)
- C. React/PHP 프로젝트에 적용 → 가능, 프로젝트 전용 규칙 추가:
  ```markdown
  ## Project-Specific Guidelines (React)
  - 함수형 컴포넌트 + Hooks만 사용
  - 기존 상태관리/스타일 방식 유지 (새 라이브러리 추가 금지)

  ## Project-Specific Guidelines (PHP)
  - 기존 PHP 버전 문법 유지
  - DB 쿼리는 PDO prepared statement만 사용
  ```

### 유튜브 강의 가능?
- 가능 (MIT, 출처 표기)
- 5편 구성: ① AI가 코드를 망치는 4가지 습관 ② 5분 설치 ③ 규칙 없음 vs 있음 실전 diff 비교 ④ React/PHP 맞춤 규칙 ⑤ 나만의 규칙·페르소나 설계
- 주의: Karpathy 공식/보증처럼 보이지 않게, 실제 연예인 페르소나는 초상권·퍼블리시티권 문제가 있으니 가상 캐릭터로 대체

## 4. 수익화 아이디어

**전제:** MIT라 원본 판매는 무의미 → "원본 + 한국어화·특화·검증·시간 절약"을 판매

| # | 아이디어 | 수익 구조 | 난이도 |
|---|---|---|---|
| 1 | 한국어 유튜브 / 온라인 강의 | 광고, 강의 판매 | 중 |
| 2 | 스택별 규칙팩 (React/Next.js, Laravel, 그누보드/워드프레스) | 크몽·Gumroad 판매 | 하 |
| 3 | 팀/기업 AI 코딩 도입 컨설팅·워크숍 | 건당 계약 | 중상 |
| 4 | CLAUDE.md 생성기 SaaS (React + PHP) | 프리미엄 구독 | 상 |
| 5 | 외주 개발 생산성 무기로 활용 | 외주 대금 | 하 |
| 6 | 블로그 / 뉴스레터 | 광고, 제휴, 유료 구독 | 중 |
| 7 | 유료 커뮤니티 (디스코드 멤버십) | 월 구독 | 중 |
| 8 | 전자책 | 판매 | 하 |

- 가장 현실적: **#5 외주 생산성** (별도 상품 없이 바로 수익)
- 규칙팩은 before/after 증거가 핵심, MIT 고지 포함
- SaaS는 Claude Code `/init` 기능과 경쟁 → 수요 검증 후 진행

**로드맵:**
1. 0~1개월: 내 프로젝트에 적용 → before/after 기록 → 비교 콘텐츠 (지표: 조회수·반응)
2. 1~3개월: 한국어 React/PHP 규칙팩 GitHub 무료 공개 + 구독자 모으기 (지표: 스타·구독자)
3. 3~6개월: 유료 강의·프리미엄 규칙팩·워크숍 (지표: 첫 유료 고객)
4. 이후: 수요가 확인되면 SaaS

**피해야 할 함정:** 원본 재판매, Karpathy 공식 제품처럼 홍보, 실제 연예인 페르소나 상업 이용, 근거 없는 효과 과장
