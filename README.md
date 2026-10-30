# hackton_kit

준비 기준일: 2026-10-31. Codex를 활용한 해커톤의 목표 설정, 구현, 검증, 인수인계를 돕는 Markdown 준비 키트다. 공식 평가 기준이나 특정 시험 환경의 도구 지원을 보장하지 않는다. 참가하는 행사의 안내와 제출 형식이 우선한다.

기본 구성은 **Ponytail + frontend-design + web-design-guidelines + Exa**다. 사전 체험 환경에는 기본 웹 검색이 없어 **Exa 검색 연결을 필수로 준비**한다. 플러그인을 사용할 수 없으면 체험에서 사용한 MCP 경로로 연결한다. 차트가 필요한 React 과제에는 **Mono Charts**를 우선 검토한다. 루프는 `요구사항 선택 → 작은 구현 → 기능 확인 → 회귀 확인 → 근거 기록 → 다음 작업`으로 운영한다. 문서는 루프를 돕는 장치이며, 작성만으로 작업이 자동 실행되지는 않는다.

## 기본 개발 스택

| 구분 | 기본 선택 |
| --- | --- |
| 프론트엔드 | **React + Vite** |
| 백엔드 | **Python** |

별도 스택 지정이 없으면 이 구성으로 시작한다. 과제에서 스택을 명시적으로 요구하면 해당 제약을 반영한다. Python 웹 프레임워크와 데이터베이스는 과제 요구사항을 확인한 뒤 필요한 것만 선택한다. 현재 키트는 문서 템플릿이며 앱 코드나 실행 환경이 구성된 상태는 아니다.

## 사전 체험 결과

2026-10-31 사용자 보고 기준이다. 본 과제에서도 같은 설정·가용량이 유지된다는 뜻은 아니다.

| 항목 | 체험 결과와 반영 |
| --- | --- |
| GitHub 다운로드 | git clone 성공 |
| Ponytail | 설치 성공 |
| 프론트 관련 스킬 | 설치 성공. 설치 수가 많아 기본 구성을 아래 두 스킬로 축소 |
| 기본 웹 검색 | 제공되지 않음. Exa 검색 연결을 필수 준비 |
| Exa 플러그인 / MCP | 플러그인 목록에서 찾지 못해 MCP로 연결·사용 |
| Fast 모드 | 동작 확인 |

스킬별 정확한 설치 방식·첫 호출 결과는 따로 확인한다. 위 결과를 본 과제 기능·시연이 검증된 상태로 기록하지 않는다.

## 빠르게 가져오기

```sh
git clone https://github.com/uamcode/hackton_kit.git
cd hackton_kit
```

이 저장소의 Markdown 템플릿을 과제에 맞게 적용하고, 기존 파일이 있으면 필요한 부분만 병합한다.

## 1. 가져갈 파일과 채점 기준

```text
프로젝트 루트/
├── AGENTS.md       # 에이전트의 작업 순서, 검증·중단 조건
├── PRODUCT.md      # 사용자, 문제, 제약, 요구사항과 수용 기준
├── DESIGN.md       # 화면 흐름, 디자인 토큰, UI 상태
├── TASKS.md        # 현재 작업, 우선순위, 짧은 반복 기록
├── VERIFY.md       # 요구사항별 실제 검증 결과와 증거
├── DECISIONS.md    # 구조, 데이터 흐름, 선택 근거와 위험
├── HANDOFF.md      # 실행·시연·남은 문제·이어할 일
└── README.md       # 환경 설정과 실행 안내
```

`agent.md` 대신 **`AGENTS.md`**를 사용한다. Codex의 기본 프로젝트 지침 파일명이다. 다른 문서는 자동으로 모두 읽힌다고 가정하지 않고 AGENTS.md에서 읽는 시점을 지정했다. [OpenAI 지침 문서](https://learn.chatgpt.com/docs/agent-configuration/agents-md)

| 채점 관점 | 문서에서 남길 내용 | 실제로 연결할 증거 |
| --- | --- | --- |
| 기술 관리 | PRODUCT의 수용 기준, VERIFY의 결과 | 구현 파일·함수, 테스트, 브라우저 동작 |
| 의도 관리 | TASKS의 작업 분해와 실패 후 방향 수정 | 지시·대화 로그, 변경 내역 |
| 인지 관리 | DECISIONS의 이유·실패 조건·보완 방법 | 해당 코드 위치와 재현 사례 |
| 소통 / FDE | HANDOFF의 현재 상태와 다음 행동 | 재현 가능한 실행·시연 순서 |

`VISION.md`와 별도 `RULES.md`는 PRODUCT와 AGENTS로, `ARCHITECTURE.md`는 DECISIONS의 구조 설명으로 묶었다. 별도 메모리 플러그인 없이 TASKS와 HANDOFF에 현재 맥락을 남긴다.

## 2. 시험 시작 시 사용 순서

1. 제공된 README와 코드를 먼저 읽고 필수 파일명, 제출 방식, 허용 도구를 확인한다.
2. 기존 AGENTS.md가 있으면 필요한 규칙을 병합한다. 이 폴더의 나머지 템플릿도 기존 파일을 덮어쓰지 않고 적용한다. 이 README의 설치 안내는 준비용이고, 제출 README에는 실제 실행·검증·한계만 반영한다.
3. PRODUCT에 요구사항 ID와 관찰 가능한 수용 기준을 적는다. 초기 계획·문서 정리는 10~15분 안에 끝낸다.
4. 별도 스택 지정이 없으면 React + Vite와 Python으로 시작한다. 기존 컴포넌트·잠금 파일을 활용하고 앱을 먼저 실행한다. 현재 동작과 기존 실패를 VERIFY에 기록한다.
5. 핵심 사용자 동작 하나를 끝까지 연결한 뒤 다음 기능으로 간다. 문서 갱신은 반복마다 몇 줄로 제한한다.

첫 지시 예시 — 아래 내용은 **Codex 대화창**에 입력한다.

```text
AGENTS.md와 제공된 과제 안내를 읽어라.
필수 요구사항을 PRODUCT.md의 R-ID와 수용 기준으로 정리하고,
현재 코드와 실행 환경을 확인해 TASKS.md에 우선순위를 적어라.
첫 핵심 사용자 흐름 하나를 구현하고 VERIFY와 GUARD를 실제 수행하라.
실행하지 못한 검증은 미실행으로 남기고, 결과와 다음 행동을 기록하라.
```

## 3. 설치 명령 모음

아래 셸 명령은 **시험 프로젝트 루트의 터미널**에서 실행한다. `$스킬명`은 터미널 명령이 아니라 **Codex 대화창**에서 쓰는 호출이다. 시험 환경에 RTK가 없을 수 있어 표준 명령으로 적었다. RTK가 설치된 개인 환경에서는 `rtk proxy`를 앞에 붙일 수 있다.

### 환경 확인

```sh
node --version
npm --version
python --version
git --version
codex --version
codex plugin --help
codex mcp --help
```

Python 명령은 환경에 따라 python3를 사용한다. 프론트와 백엔드의 실제 버전·실행 명령·포트는 VERIFY와 HANDOFF에 기록한다. 로컬에서는 Codex CLI 0.165.0의 `plugin add`, `plugin marketplace add`, `mcp add --url` 도움말을 확인했다. 사전 체험의 설치·사용 성공은 위 사용자 보고로 구분해 기록했으며, 새 Exa Git marketplace 경로와 축소한 두 스킬의 개별 호출은 시험 환경에서 재확인이 필요하다. `skills` CLI의 현재 문서는 Node.js 22.20 이상을 요구하므로 사전 체험에서 버전을 확인한다. [Skills CLI 공식 저장소](https://github.com/vercel-labs/skills)

### Fast 모드와 사용량 확인

아래는 셸 명령이 아니라 **실행 중인 Codex 대화창**에 입력하는 명령이다.

| 명령 | 용도 |
| --- | --- |
| `/fast` | Fast 모드 설정 확인·변경. 사전 체험에서 동작 확인 |
| `/status` | 현재 세션의 모델·토큰/컨텍스트 사용 상태와 제공되는 사용 한도 확인 |
| `/statusline` | 지원되는 CLI에서 컨텍스트 잔량·사용 한도·토큰 카운터를 하단에 표시하도록 설정 |
| `/usage` | 지원되는 CLI와 인증 방식에서 계정 사용량 조회. 일/주/누적 조회는 `/usage daily`, `/usage weekly`, `/usage cumulative` |

**대화에 남은 컨텍스트와 계정·시험의 사용 예산은 서로 다르다.** 컨텍스트 잔여 비율을 전체 계정 잔여 토큰으로 해석하지 않는다. 시험 전용 인증이나 게이트웨이에서는 계정 한도가 표시되지 않을 수 있다. `/status`에 예산이 없거나 명령이 지원되지 않으면 플랫폼의 사용량 표시 또는 Helper로 확인한다. 표시되지 않은 잔여량을 추정하지 않는다. [OpenAI 명령 안내](https://learn.chatgpt.com/docs/developer-commands)

### 코딩: Ponytail

플러그인 설치가 지원되면:

```sh
codex plugin marketplace add DietrichGebert/ponytail
codex plugin add ponytail@ponytail
```

공식 설치 안내에 따라 Codex의 `/hooks`에서 해당 훅을 검토·허용하고 새 세션에서 로딩을 확인한다. **시험 중에는 플랫폼이 허용하는 세션 전환·기록 방식을 따른다.** 플러그인으로 설치했다면 스킬 선택기에 표시되는 이름으로 호출한다. 공식 예시는 `$ponytail:ponytail-review` 형식이다. [Ponytail 공식 안내](https://github.com/DietrichGebert/ponytail)

플러그인·훅이 지원되지 않으면 아래처럼 스킬만 설치하는 방법을 사용할 수 있다. 위 방법과 중복 설치할 필요는 없다.

```sh
npx skills add DietrichGebert/ponytail --skill ponytail --skill ponytail-review --agent codex --copy -y
```

스킬만 설치한 경우의 대화창 예시:

```text
$ponytail full
PRODUCT.md의 필수 요구사항을 만족하는 가장 작은 변경으로 구현해라.
검증, 오류 처리, 접근성은 유지하라.
```

### 프론트 스킬: 구현·검토용 두 개만 설치

| 스킬 | 역할 | 범용성 |
| --- | --- | --- |
| Anthropic `frontend-design` | 레이아웃·타이포그래피·시각 방향을 정하고 UI 구현 | 특정 프레임워크에 묶이지 않는 웹 UI 설계 |
| Vercel `web-design-guidelines` | UI 코드의 접근성·상호작용·사용성 검토 | 웹 인터페이스 기준 검토 |

저장소 전체를 설치하지 않고 **`--skill`로 각각 하나만 선택**한다. 아래 두 설치 명령을 기본으로 사용한다.

```sh
npx skills add anthropics/skills --skill frontend-design --agent codex --copy -y
npx skills add vercel-labs/agent-skills --skill web-design-guidelines --agent codex --copy -y
npx skills list --agent codex
```

설치 후 `/skills` 또는 스킬 선택기에 두 이름이 보이는지 확인하고 환경이 허용하는 방식으로 다시 로드한다. 이미 설치한 다른 스킬을 자동으로 삭제하지 않는다. 여러 개가 설치돼 있다면 목록과 설치 범위를 확인하고 이번 작업에서는 위 두 스킬만 호출한다.

Codex 대화창 예시:

```text
$frontend-design
PRODUCT.md와 DESIGN.md를 읽고 핵심 화면을 구현해라.
기본 스택은 React + Vite이며 기존 컴포넌트를 활용하고 기능·데이터 흐름은 유지해라.

$web-design-guidelines
변경한 UI 코드를 검토하고 접근성·입력·포커스·오류 상태의 문제를 찾아라.
필요한 최신 공식 가이드는 Exa로 읽고 확인하지 못한 기준은 미검증으로 남겨라.
실제 화면에서 확인할 항목을 구분해라.
```

`web-design-guidelines`는 검토할 때 최신 가이드를 가져온다. 가이드를 읽지 못하면 그 사실을 기록하고 코드 검토와 실제 브라우저 검증을 구분한다. 기능 검증은 별도로 수행한다. [frontend-design 원본](https://github.com/anthropics/skills/tree/main/skills/frontend-design) · [web-design-guidelines 원본](https://github.com/vercel-labs/agent-skills/tree/main/skills/web-design-guidelines)

### 프론트 차트: Mono Charts — 필요한 경우 선택

[Mono Charts](https://amicro.dev/mono-charts)는 차트가 필요한 React 과제에서 검토할 컴포넌트 모음이다. Amicro의 React 컴포넌트를 필요한 것만 프로젝트에 추가해 사용한다. 대시보드·통계 화면이 과제에 필요할 때 우선 검토하고, 기존 차트로 충분하거나 React를 쓰지 않는 과제에서는 도입을 위해 스택을 바꾸지 않는다. [프로젝트 저장소](https://github.com/Subhan-code/Monocharts)

```sh
# Amicro 설정이 없는 프로젝트에서 최초 1회
npx @subhanhq/amicro@latest init

# 필요한 차트만 선택해 추가 — 아래 세 개를 모두 설치할 필요는 없음
npx @subhanhq/amicro@latest add mono-rounded-line
npx @subhanhq/amicro@latest add mono-rounded-bar
npx @subhanhq/amicro@latest add mono-rounded-kpi
```

추세는 선 차트, 항목 비교는 막대 차트, 요약 지표는 KPI 카드부터 검토한다. 위 개별 추가 명령은 공개된 [Mono Charts 페이지 소스](https://github.com/Subhan-code/Monocharts/blob/main/src/components/MonoChartsPage.tsx)에서 확인했다. 실제 설치·렌더링은 미검증이다. 기존 설정과 생성 파일을 확인하고 필요한 의존성만 반영한다.

Codex 대화창 예시:

```text
차트가 필요한 화면에는 Mono Charts에서 목적에 맞는 컴포넌트만 사용해라.
기존 DESIGN.md의 토큰과 한글 표기·숫자 단위를 적용해라.
컴포넌트의 데이터 입력 방식을 확인하고 샘플 데이터를 실제 입력에 연결해라.
빈 데이터와 값 0을 구분하고, 핵심 수치를 텍스트로도 제공해라.
데이터 변경 시 그래프 갱신과 좁은 화면 표시를 실제 검증해라.
```

### 웹 검색: Exa 필수 — 플러그인 확인 후 MCP 연결

사전 체험에는 기본 웹 검색이 없었고 Exa MCP로 검색했다. **필수인 것은 Exa 검색 도구의 실제 연결·호출 성공**이다. 플러그인과 MCP를 중복 설치할 필요는 없다.

#### 1. 공식 디렉터리에서 플러그인 설치

Codex 대화창의 `/plugins` 또는 제공되는 Plugins 메뉴에서 Exa를 찾는다. 직접 접근이 허용되면 [Exa 공식 플러그인 페이지](https://chatgpt.com/plugins/exa)에서 설치하고 안내되는 인증을 마친다. 설치 후 환경이 허용하는 새 세션에서 도구가 보이는지 확인한다. 플러그인은 MCP와 스킬을 함께 제공한다. 개인 ChatGPT에서의 설치가 시험 작업 공간에도 적용된다고 가정하지 않는다. [Exa 공식 설치 안내](https://exa.ai/docs/integrations/chatgpt-codex)

#### 2. 목록에 없으면 공식 Git 저장소의 marketplace 등록 시도

Codex CLI가 Git marketplace 설치를 지원하고 외부 marketplace 등록이 허용되는 경우에만 시도한다.

```sh
codex plugin marketplace add exa-labs/exa-mcp-server
codex plugin list --marketplace exa --available --json
```

등록이 성공하고 목록에 `exa`가 보일 때 설치한다.

```sh
codex plugin add exa@exa
```

이 명령은 [Exa 저장소의 marketplace](https://github.com/exa-labs/exa-mcp-server/blob/main/.claude-plugin/marketplace.json)에 정의된 marketplace 이름 `exa`, plugin 이름 `exa`와 [Codex의 Git marketplace 등록 방식](https://developers.openai.com/plugins/build/plugins)을 조합한 경로다. **시험 환경에서 이 경로의 설치·호출은 미검증**이다. 공식 디렉터리의 Exa 앱과 동일한 인증·도구 구성을 보장하지 않는다. 등록·호환성 오류, 설치 후 도구 미표시가 있으면 한 번만 확인하고 아래 MCP 경로로 전환한다.

#### 3. 플러그인 설치가 안 되면 MCP로 연결 — 체험에서 사용한 경로

시험 프로젝트의 일반 터미널에서 실행한다.

```sh
codex mcp add exa --url https://mcp.exa.ai/mcp
codex mcp list
```

CLI 명령을 지원하지 않지만 MCP 설정 UI가 있으면 서버 이름은 `exa`, 원격 HTTP URL은 `https://mcp.exa.ai/mcp`로 추가한다. 이미 같은 서버가 연결돼 있으면 다시 등록하지 않는다.

이후 Codex 대화창의 `/mcp`에서 Exa의 검색·페이지 읽기 도구가 보이는지 확인한다. 필요하면 환경이 허용하는 방식으로 세션을 다시 로드한다. 인증이 필요하다고 안내될 때만 터미널에서 다음을 실행한다.

```sh
codex mcp login exa
```

검색·페이지 읽기는 제한된 익명 사용량으로 시험할 수 있다. 인증·사용량 제한이 나오면 안내되는 연결 절차를 따르며 인증값을 README나 과제 코드에 넣지 않는다. [Exa MCP 공식 문서](https://exa.ai/docs/get-started/exa-mcp)

연결 후에는 아래 요청을 **실제로 한 번 실행**한다.

```text
Exa로 Node.js 공식 문서를 검색하고 결과 한 페이지의 본문을 읽어라.
확인한 내용 한 가지와 출처 URL을 보고해라.
도구가 없거나 호출이 실패하면 실패 내용을 명시해라.
```

검색 대상은 라이브러리 공식 문서, 공개 API 명세, 일반적인 오류 해결 자료로 좁힌다. 비공개 과제 원문·코드·입력 데이터·로그를 외부 검색 서비스에 보내지 않는다. 검색이나 도구가 금지된 환경에서는 추가 연결로 우회하지 않는다.

## 4. 프론트 구성 선택

**구현은 frontend-design, 검토는 web-design-guidelines**로 나눈다. 특정 프레임워크의 추가 스킬이나 Impeccable 같은 디자인 묶음은 기본 설치에서 제외한다. Mono Charts는 차트가 필요한 React 과제에서만 추가하는 컴포넌트이며 프론트 스킬 두 개에 포함되지 않는다.

코딩은 Ponytail, 검색은 Exa를 사용한다. 과제를 보기 전에 다른 도구를 더 설치하지 않고 React + Vite·Python과 기본 도구 구성으로 시작한다.

## 5. 180분 작업 운영 예시

| 경과 시간 | 할 일 |
| --- | --- |
| 0~15분 | 안내 읽기, 앱 실행, 수용 기준과 첫 작업 결정 |
| 15~95분 | 핵심 동작을 끝까지 연결하며 작은 검증 반복 |
| 95~135분 | 나머지 필수 기능, 오류·경계값·회귀 확인 |
| 135~150분 | 화면 검토와 중요한 결함 수정 |
| 150~180분 | 새 기능 동결, 최종 검증·시연·인수인계·제출 |

반복 하나는 10~20분을 목표로 한다. 같은 실패를 두 번 반복하거나 15분 동안 진전이 없으면 가설·작업 크기·접근법을 바꾼다. 검증을 통과하면 다음 요구사항으로 이동한다. 자동 반복 스케줄러나 별도 Autoresearch 시스템은 이 준비안에 추가하지 않았다.

## 6. 본 과제 시작 전 재확인

체험 성공 항목도 본 과제 작업 공간에서는 실제로 다시 확인한다.

- [ ] kit을 가져오고 기존 AGENTS와 충돌 없이 필요한 지침을 적용했다.
- [ ] Ponytail이 로드되고 요청에 적용된다.
- [ ] frontend-design과 web-design-guidelines 두 스킬을 선택해 호출할 수 있다.
- [ ] Exa 플러그인 또는 MCP 중 하나로 검색과 페이지 읽기를 실제 실행했다.
- [ ] `/fast` 상태와 `/status`의 컨텍스트·사용 한도 표시를 확인했다.
- [ ] 앱 서버·포트·브라우저 미리보기와 파일 저장이 된다.
- [ ] 제출 방식과 세션 전환·인증·커밋의 허용 범위를 확인했다.
- [ ] 직접 답할 서술형 두 문항의 실제 근거를 HANDOFF와 DECISIONS에 남길 준비가 됐다.

실패한 플러그인 설치를 반복 복구하느라 시간을 쓰지 않는다. Exa는 MCP 경로로 전환하고 사용할 수 없는 도구는 VERIFY에 기록한다.

## 7. 제출 README에 채울 내용

아래 항목을 제공된 README의 적절한 위치에 병합한다. 예시 명령을 실제 명령처럼 남기지 않는다.

| 항목 | 실제 값 |
| --- | --- |
| 필요한 런타임·버전 | 미확인 |
| 의존성 설치 명령 | 미확인 — 잠금 파일과 제공 안내를 확인 |
| 개발/실행 명령·접속 주소 | 미확인 |
| 빌드·테스트 명령 | 미확인 |
| 입력·샘플 데이터·환경 설정 | 미확인 — 인증값 자체는 기록하지 않음 |
| 핵심 기능·시연 순서 | HANDOFF를 바탕으로 작성 |
| 검증 결과·남은 한계 | VERIFY와 DECISIONS의 실제 결과를 요약 |

후속 서술형은 HANDOFF와 DECISIONS를 보고 **내 코드의 위치 → 실패하는 조건 → 사용자 영향 → 다음 검증·개선** 순서로 설명한다. 구현하지 않은 개선안을 이미 구현한 것처럼 쓰지 않는다.

## 8. 본인이 직접 답할 서술형 준비

사전 체험에서 나온 질문의 요지다. 답변은 본인이 작성한다. 작업 중에는 답변을 대신 생성하기보다 아래 실제 근거를 짧게 기록하고 제출 전에 본인이 코드·실행 결과와 대조한다.

| 질문 | 작업 중 남길 근거 | 기록 위치 |
| --- | --- | --- |
| 서비스의 핵심 동작은 무엇이고 어떻게 확인했는가? | 사용자 입력/행동 → 처리 → 결과, 구현 파일·함수, 실제 입력·조작, 기대 결과와 관찰 결과, 확인하지 못한 범위 | HANDOFF의 직접 답변 준비 + VERIFY의 증거 ID |
| AI 에이전트의 제안을 바꿨다면 왜 바꿨는가? | AI의 원래 제안 → 본인이 바꾼 내용 → 바꾼 이유와 제약 → 변경 후 실제 확인 결과 | DECISIONS의 D-ID + TASKS의 해당 반복 |

AI 제안을 수정한 사례가 없으면 없다고 답한다. 답변을 위해 없었던 판단·대화·검증을 만들어 넣지 않는다. 핵심 동작은 구현한 서비스의 구체적인 흐름으로 설명하고 「잘 작동했다」 대신 실제로 무엇을 입력하고 어떤 결과를 봤는지 적는다.
