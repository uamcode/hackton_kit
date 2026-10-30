# hackton_kit

대회용 Codex 작업 키트. 제공된 과제·평가·제출 규칙을 우선한다.

## 확정 구성

- 프론트엔드: **React + Vite**
- 백엔드: **Python** — 웹 프레임워크와 DB는 과제 요구사항에 맞춰 필요한 것만 선택
- 코딩: **Ponytail**
- 프론트 스킬: **Anthropic frontend-design**으로 구현, **Vercel web-design-guidelines**로 검토
- 검색: **Exa** — 플러그인 또는 MCP 중 하나로 연결
- 차트가 필요하면 [Mono Charts](https://amicro.dev/mono-charts) 사용

## 시작 순서

1. 제공된 과제 안내·README·코드를 읽고 필수 요구사항, 허용 도구, 제출 방식을 확인한다.
2. 이 키트의 템플릿을 프로젝트에 적용한다. 기존 파일이 있으면 필요한 내용만 병합한다.
3. [AGENTS.md](AGENTS.md)를 읽고 PRODUCT에 요구사항 ID·수용 기준, TASKS에 우선순위를 적는다. 초기 정리는 15분 안에 끝낸다.
4. 앱을 실행하고 핵심 사용자 흐름 하나를 끝까지 구현·검증한 뒤 다음 요구사항으로 간다.

| 문서 | 읽거나 갱신할 때 |
| --- | --- |
| [AGENTS.md](AGENTS.md) | 작업 시작: 구현·검증·중단·서브에이전트 위임 규칙 |
| [PRODUCT.md](PRODUCT.md) | 요구사항과 완료 기준 확인 |
| [DESIGN.md](DESIGN.md) | UI 구현 전: 화면 흐름·토큰·상태 |
| [TASKS.md](TASKS.md) | 맥락 복원·현재 작업·담당·다음 행동 갱신 |
| [VERIFY.md](VERIFY.md) | 실제 명령·조작·예상·관찰 결과 기록 |
| [DECISIONS.md](DECISIONS.md) | 실제 흐름·중요한 선택·AI 제안을 바꾼 이유·한계 기록 |

작업 루프: `요구사항 선택 → 작은 구현 → VERIFY → GUARD → 근거 기록 → 다음 작업`.
VERIFY·GUARD의 기준과 실제 증거는 VERIFY.md에서 관리한다.

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

### Exa

플러그인 목록에 Exa가 있으면 설치해 사용한다. 목록에 없거나 설치가 안 되면 MCP로 연결한다.

```sh
codex mcp add exa --url https://mcp.exa.ai/mcp
codex mcp list
```

설정 UI로 연결할 때도 서버 이름은 `exa`, URL은 `https://mcp.exa.ai/mcp`다. 인증을 요청할 때만 `codex mcp login exa`를 실행한다.
연결 후 공식 문서를 검색하고 한 페이지를 읽어 출처 URL을 확인한다.

### 차트가 필요할 때

```sh
npx @subhanhq/amicro@latest init
npx @subhanhq/amicro@latest add mono-rounded-line
```

Amicro 설정이 있으면 `init`을 생략한다. 목적에 따라 `mono-rounded-line` 대신 `mono-rounded-bar` 또는 `mono-rounded-kpi` 중 필요한 것만 추가한다.

## Codex 대화창 명령

| 명령 | 용도 |
| --- | --- |
| `/fast` | Fast 모드 확인·변경 |
| `/status` | 세션의 모델·토큰/컨텍스트 상태와 제공되는 사용 한도 확인 |
| `/skills` | 설치된 스킬 선택 |
| `/mcp` | Exa 등 MCP 연결·도구 확인 |
| `/subagents` | 서브에이전트 상태 확인 |

컨텍스트 잔량과 계정·대회 사용 예산은 별개다. 표시되지 않는 사용 한도는 추정하지 않는다.

## 제출·시연 준비

과제 README에 아래 실제 값을 기록한다. 기존 제출 형식이 있으면 그 형식에 병합한다.

- 런타임·버전·의존성 설치·실행 명령·포트·접속 주소
- 핵심 흐름의 화면/경로·샘플 입력·기대 결과·연결 R-ID와 대표 오류 사례
- 빌드·테스트 명령·최종 검증 결과와 남은 한계 — 상세 증거는 VERIFY 참조
- 실제 사용한 공개 자료·스킬의 출처와 직접 구현·변경한 범위

아래 두 질문은 본인이 직접 답한다. 별도 답변 메모를 중복 작성하지 않고 기존 기록을 근거로 쓴다.

| 질문 | 근거와 기록 위치 |
| --- | --- |
| 서비스의 핵심 동작은 무엇이고 어떻게 확인했는가? | PRODUCT의 목적·R-ID → DECISIONS의 실제 입력/처리/결과·코드 위치 → VERIFY의 실제 조작·예상/관찰 결과·미검증 범위 |
| AI 에이전트의 제안을 바꿨다면 무엇을 왜 바꿨는가? | DECISIONS의 원래 제안·수정·사람이 밝힌 이유·VERIFY 증거 ID, 연결 TASKS 반복 |

미실행 검증과 없었던 판단을 만들어 적지 않는다. AI 제안을 바꾼 사례가 없으면 없다고 남긴다.
