# hackton_kit

대회용 Codex 작업 키트. 제공된 과제·평가·제출 규칙을 우선한다.

## 기본 구성

- 프론트엔드: **React + Vite**
- 백엔드: **Python** — 웹 프레임워크는 과제 요구사항에 맞춰 선택
- 데이터베이스: **PostgreSQL** — 실제 프론트·백엔드·DB 연동을 구현하고 PostgreSQL MCP로 개발 중 조회·검증
- 코딩: **Ponytail**
- 프론트 스킬: **Anthropic frontend-design**으로 구현, **Vercel web-design-guidelines**로 검토
- 검색: **Exa** — 플러그인 또는 MCP 중 하나로 연결
- 아키텍처 시각화: **Archify** — 실제 코드 기반 구조도를 필요할 때 생성

## 시작 순서

1. 제공된 과제 안내·README·코드를 읽고 필수 요구사항, 허용 도구, 제출 방식을 확인한다.
2. 이 키트의 템플릿을 프로젝트에 적용한다. 기존 파일이 있으면 필요한 내용만 병합한다.
3. [AGENTS.md](AGENTS.md)를 읽고 PRODUCT에 요구사항 ID·수용 기준, TASKS에 우선순위를 적는다. 초기 정리는 15분 안에 끝낸다.
4. 앱을 실행하고 검증 명령 하나를 정한 뒤, 핵심 사용자 흐름 하나를 끝까지 구현·검증하고 다음 요구사항으로 간다.

| 문서 | 읽거나 갱신할 때 |
| --- | --- |
| [AGENTS.md](AGENTS.md) | 작업 시작: 구현·검증·중단·서브에이전트 위임 규칙 |
| [PRODUCT.md](PRODUCT.md) | 요구사항과 완료 기준 확인 |
| [DESIGN.md](DESIGN.md) | UI 구현 전: 화면 흐름·토큰·상태 |
| [TASKS.md](TASKS.md) | 맥락 복원·현재 작업·담당·다음 행동 갱신 |
| [VERIFY.md](VERIFY.md) | 의미 있는 검증 단위로 명령과 실제 조작·관찰 결과를 한 줄씩 기록 |
| [EVALUATION.md](EVALUATION.md) | 사용자·관리자·채점자 및 AI Native 독립 평가 |
| [DECISIONS.md](DECISIONS.md) | 실제 흐름·중요한 선택·AI 제안을 바꾼 이유·한계 기록 |

작업 루프: `요구사항 선택 → 작은 구현 → VERIFY → GUARD → 근거 기록 → 다음 작업`.
VERIFY·GUARD의 기준과 실제 증거는 VERIFY.md에서 관리한다.

## Codex CLI 시작·worktree

`PROJECT_DIR`를 실제 과제 프로젝트의 루트 경로로 바꾸고 아래 명령 중 하나로 메인 세션을 시작한다.

기본 작업 폴더에서 시작:

```sh
codex -C "PROJECT_DIR"
```

원본과 분리한 새 worktree에서 시작:

```sh
codex -C "PROJECT_DIR" --worktree
```

`-C`는 기준 프로젝트를 지정하고 `--worktree`는 새 세션용 Git 작업 공간을 자동 생성한다. 서브에이전트별 자동 분리를 전제로 운영하지 않으며, worktree의 변경은 제출 대상에 통합한 뒤 검증한다. [OpenAI 공식 CLI 문서](https://learn.chatgpt.com/docs/cli/reference)

위임 전에 `/permissions`로 메인의 권한을 확인한다. 서브에이전트는 메인의 sandbox·승인 설정을 상속한다. [권한 상속 안내](https://learn.chatgpt.com/docs/agent-configuration/subagents)

## 도구 설치

아래는 **프로젝트 루트의 터미널**에서 실행한다. 이미 설치·연결되어 있으면 생략한다.

### Ponytail

```sh
codex plugin marketplace add DietrichGebert/ponytail
codex plugin add ponytail@ponytail
```

설치 후 `/hooks`에서 훅을 검토·허용하고, 환경이 허용하는 방식으로 다시 로드한다. 호출은 스킬 선택기에 표시되는 이름을 사용한다.

### 프론트 스킬 두 개

```sh
npx skills add anthropics/skills --skill frontend-design --agent codex --copy -y
npx skills add vercel-labs/agent-skills --skill web-design-guidelines --agent codex --copy -y
```

Codex 대화창에서 `$frontend-design`으로 구현하고 `$web-design-guidelines`로 검토한다.

### Archify (선택)

[Archify](https://github.com/tt-a1i/archify)는 코드에 근거한 시스템 구조·데이터 흐름을 HTML로 시각화하는 스킬이다. 세션에서 공유할 수 있도록 전역 설치한다.

```sh
npx -y skills add tt-a1i/archify --skill archify --agent codex --global --copy --yes
```

핵심 구현 완료 후 또는 최종 통합 시에 사용한다. Codex에 “Archify로 실제 코드의 요청→처리→저장→응답 흐름을 그려줘. 확인한 연결과 추정을 구별해줘.”라고 요청한다. 구조도를 실제 코드와 실행 결과에 대조한다.

### Exa

플러그인 목록에 Exa가 있으면 설치해 사용한다. 목록에 없거나 설치가 안 되면 MCP로 연결한다.

```sh
codex mcp add exa --url https://mcp.exa.ai/mcp
codex mcp list
```

설정 UI로 연결할 때도 서버 이름은 `exa`, URL은 `https://mcp.exa.ai/mcp`다. 인증을 요청할 때만 `codex mcp login exa`를 실행한다.
연결 후 공식 문서를 검색하고 한 페이지를 읽어 출처 URL을 확인한다.

### PostgreSQL MCP

[Microsoft Postgres MCP](https://github.com/microsoft/postgres-mcp)로 Codex에서 DB 스키마·테이블·쿼리 결과를 확인한다. 현재 Preview이며 **Node.js 22 이상**과 접속 가능한 PostgreSQL DB가 필요하다. MCP는 개발 보조 도구이고 앱은 `프론트 → Python 백엔드 → PostgreSQL`로 연결한다. 이 키트는 설치 안내만 제공한다.

**1. 대회 전: MCP 등록**

```sh
node --version
codex mcp add postgres -- npx -y @microsoft/postgres-mcp run
codex mcp list
```

`npx`가 첫 실행 때 패키지를 내려받으므로 전역 설치는 필요 없다. 이미 `postgres` 서버가 등록되어 있으면 중복 추가하지 않는다. 등록만으로 DB 생성이나 연결 검증이 완료되는 것은 아니다.

**2. 과제·DB 공개 후: 연결 프로필 등록**

아래 `DB_HOST`·포트·`MCP_USER`·`DB_NAME`을 제공된 값으로 바꾼다. `MCP_USER`는 조회 전용 DB 계정을 사용하고 앱의 쓰기 계정과 구분한다. 원격 DB는 제공 업체 안내에 따라 `sslmode=verify-full` 등 TLS·인증서 설정을 연결 문자열에 추가한다.

```sh
npx -y @microsoft/postgres-mcp connection add hackathon "host=DB_HOST port=5432 user=MCP_USER dbname=DB_NAME" --access-mode ro
npx -y @microsoft/postgres-mcp connection set-password hackathon
npx -y @microsoft/postgres-mcp connection list
```

비밀번호는 `set-password`의 숨김 입력창에 직접 입력하며 OS 자격증명 저장소에 보관된다. 비밀번호를 연결 문자열·README·대화·Git에 넣지 않는다. `ro`는 MCP의 쓰기 도구를 제한하며 DB 계정의 조회 전용 권한도 함께 적용한다. 스키마 변경은 백엔드 마이그레이션으로 관리한다.

**3. Codex에서 연결 확인**

설정을 다시 로드하거나 새 세션을 열고 `/mcp`에서 `postgres`의 도구가 보이는지 확인한다. 이어서 “`hackathon` 프로필에 연결해 `SELECT 1 AS ok`를 실행하고 현재 DB 이름과 테이블 목록을 보여줘”라고 요청한다. `ok = 1`과 의도한 DB가 확인되면 연결 성공이며, 새 DB의 빈 테이블 목록은 정상이다. 실제 결과는 VERIFY.md에 기록한다.

설정·OS 키링 문제는 [Microsoft 사용 안내](https://github.com/microsoft/postgres-mcp/blob/main/USAGE.md), Codex 등록 형식은 [OpenAI 공식 MCP 문서](https://learn.chatgpt.com/docs/extend/mcp)를 확인한다.

## Codex 대화창 명령

| 명령 | 용도 |
| --- | --- |
| `/fast` | Fast 모드 확인·변경 |
| `/status` | 세션의 모델·토큰/컨텍스트 상태와 제공되는 사용 한도 확인 |
| `/permissions` | 현재 세션의 권한 확인·변경 |
| `/skills` | 설치된 스킬 선택 |
| `/mcp` | Exa 등 MCP 연결·도구 확인 |
| `/subagents` | 서브에이전트 상태 확인 |

컨텍스트 잔량과 계정·대회 사용 예산은 별개다. 표시되지 않는 사용 한도는 추정하지 않는다.

## 제출·시연 준비

과제 README에 아래 실제 값을 기록한다. 기존 제출 형식이 있으면 그 형식에 병합한다.

- 런타임·버전·의존성 설치·실행 명령·포트·접속 주소·필요한 환경변수 이름. 환경변수가 필요하면 실제 인증값 없이 `.env.example`에 예시를 제공
- 핵심 흐름의 화면/경로·샘플 입력·기대 결과·연결 R-ID와 대표 오류 사례
- 빌드·테스트 명령·최종 검증 결과와 남은 한계 — 상세 증거는 VERIFY 참조
- 실제 사용한 공개 자료·스킬의 출처와 직접 구현·변경한 범위

제출 대상만 별도 임시 폴더에 구성해 이 안내대로 설치·실행·핵심 시연을 재현하고 VERIFY에 남긴다. 빌드 결과 제출이 필수이면 `.gitignore`의 `dist/` 제외 규칙을 조정한다.

아래 두 질문은 본인이 직접 답한다. 별도 답변 메모를 중복 작성하지 않고 기존 기록을 근거로 쓴다.

| 질문 | 근거와 기록 위치 |
| --- | --- |
| 서비스의 핵심 동작은 무엇이고 어떻게 확인했는가? | PRODUCT의 목적·R-ID → DECISIONS의 실제 입력/처리/결과·코드 위치 → VERIFY의 실제 조작·관찰 결과·미검증 범위 |
| AI 에이전트의 제안을 바꿨다면 무엇을 왜 바꿨는가? | DECISIONS의 원래 제안·바꾼 것·사람이 밝힌 이유·VERIFY 증거 ID |

미실행 검증과 없었던 판단을 만들어 적지 않는다. AI 제안을 바꾼 사례가 없으면 없다고 남긴다.
