# hackton_kit

준비 기준일: 2026-10-31. Codex를 활용한 해커톤의 목표 설정, 구현, 검증, 인수인계를 돕는 Markdown 준비 키트다. 공식 평가 기준이나 특정 시험 환경의 도구 지원을 보장하지 않는다. 참가하는 행사의 안내와 제출 형식이 우선한다.

추천 조합은 **Ponytail + Impeccable + 기본 웹 검색**, Exa는 검색 대안이다. 차트가 필요한 React 과제에는 **Mono Charts**를 우선 검토한다. 루프는 `요구사항 선택 → 작은 구현 → 기능 확인 → 회귀 확인 → 근거 기록 → 다음 작업`으로 운영한다. 문서는 루프를 돕는 장치이며, 작성만으로 작업이 자동 실행되지는 않는다.

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
4. 제공된 스택과 잠금 파일을 유지하고 앱을 먼저 실행한다. 현재 동작과 기존 실패를 VERIFY에 기록한다.
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
git --version
codex --version
codex plugin --help
codex mcp --help
```

현재 로컬에서는 Codex CLI 0.165.0의 `plugin add`, `plugin marketplace add`, `mcp add --url`, `--search` 도움말을 확인했다. 설치나 시험 환경에서의 실행은 검증하지 않았다. `skills` CLI의 현재 문서는 Node.js 22.20 이상을 요구하므로 사전 체험에서 버전을 확인한다. [Skills CLI 공식 저장소](https://github.com/vercel-labs/skills)

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

### 디자인 기본: Impeccable

디자인 구현부터 검토·수정까지 같은 도구로 이어가기 좋아 기본 후보로 선정했다. **현재 버전은 `impeccable`이라는 스킬과 `$impeccable 하위명령` 형식**을 사용한다. 예전 노트의 개별 슬래시 명령을 그대로 가정하지 않는다. [공식 사용 안내](https://impeccable.style/docs/)

```sh
npx impeccable install --providers=codex --scope=project
```

설치 후 도구를 다시 로드한다. 디자인 훅을 사용하는 설치라면 `/hooks`에서 검토·허용한다. 현재 배포는 보조 실행 파일을 포함하거나 첫 실행 시 내려받을 수 있으므로 **설치 성공뿐 아니라 첫 호출까지 사전 체험**한다. [공식 설치 옵션](https://github.com/pbakaus/impeccable#installation)

스킬만 설치하는 대안 — 위 설치와 둘 중 하나를 선택한다. 전용 설치 프로그램의 훅·통합 구성과는 차이가 있다.

```sh
npx skills add pbakaus/impeccable --skill impeccable --agent codex --copy -y
```

Codex 대화창에서 필요한 단계만 호출한다.

```text
$impeccable init
기존 PRODUCT.md의 사용자·필수 요구사항을 유지하고 빠진 디자인 맥락만 보완해라.
이번에는 이미지를 생성하는 시안 단계 없이 코드로 구현한다.

$impeccable shape
PRODUCT.md와 DESIGN.md를 읽고 핵심 화면과 사용자 흐름 하나를 설계해라.

$impeccable audit
실행 중인 핵심 화면의 접근성, 반응형, 오류·로딩·빈 상태를 점검해라.
실제 화면을 확인하지 못한 항목은 미검증으로 구분해라.

$impeccable polish
기능을 유지하며 발견된 문제와 간격·타이포그래피만 수정해라.
```

`PRODUCT.md`와 `DESIGN.md`는 Impeccable도 사용하는 맥락 파일이다. 문서가 이미 있으면 전체 재작성 대신 필요한 부분만 갱신한다. [공식 시작 가이드](https://impeccable.style/tutorials/getting-started/)

### 가벼운 디자인 대안과 선택 검토 도구

Impeccable의 실행 파일·통합 설정이 환경에 맞지 않으면 **Anthropic의 frontend-design**을 대안으로 쓴다. 스킬의 지침을 Codex가 읽는 방식이며 Claude 모델을 사용하는 것은 아니다. 생성용 디자인 스킬을 여러 개 동시에 적용할 필요는 없다. [원본 스킬](https://github.com/anthropics/skills/tree/main/skills/frontend-design)

```sh
npx skills add anthropics/skills --skill frontend-design --agent codex --copy -y
```

추가 검토 기준이 필요할 때만 **Vercel web-design-guidelines**를 설치한다. UI 코드 검토용이며 실행 화면 검증을 대신하지 않는다. 검토할 때 외부의 최신 가이드를 가져오므로 네트워크도 필요하다. [원본 스킬](https://github.com/vercel-labs/agent-skills/tree/main/skills/web-design-guidelines)

```sh
npx skills add vercel-labs/agent-skills --skill web-design-guidelines --agent codex --copy -y
npx skills list --agent codex
```

설치 수는 후보의 보급 정도를 보는 참고치다. 2026-10-31 조회 화면 기준 [Impeccable 약 37만](https://www.skills.sh/pbakaus/impeccable/impeccable), [frontend-design 약 110만](https://www.skills.sh/anthropics/skills/frontend-design), [web-design-guidelines 약 80만](https://www.skills.sh/vercel-labs/agent-skills/web-design-guidelines)이었다. 추천은 보급 수와 함께 원본 지침, 설치 의존성, 이번 작업 범위를 검토해 정했다.

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

### 웹 검색: 기본 검색 확인 후 Exa 준비

**웹 검색은 준비하되 기본 검색이 잘 되면 Exa를 추가할 필요는 없다.** 일반적인 로컬 Codex는 검색을 제공하고, CLI의 `--search`는 실시간 검색을 켠다. 시험 환경에서 제공하는 Codex의 권한·기능은 별도로 확인해야 한다. [OpenAI 웹 검색 문서](https://learn.chatgpt.com/docs/web-search)

표준 CLI 실행을 지원하는 환경에서 사용할 수 있는 명령:

```sh
codex --search
```

Exa **플러그인**으로 준비하려면 제공되는 Plugins 메뉴나 [공식 Exa 플러그인 페이지](https://chatgpt.com/plugins/exa)에서 설치하고 필요한 인증을 마친다. 플러그인은 MCP와 스킬을 함께 제공하므로 아래 MCP를 중복 등록하지 않는다. [Exa의 Codex 설치 안내](https://exa.ai/docs/integrations/chatgpt-codex)

플러그인 카탈로그가 없고 MCP 등록이 허용되면 **Exa MCP만 연결하는 대안**:

```sh
codex mcp add exa --url https://mcp.exa.ai/mcp
codex mcp list
```

이후 Codex의 `/mcp`에서 연결을 확인하고 공개 문서 검색을 한 번 실행한다. 원격 서버 인증이 필요하다고 안내될 때는 `codex mcp login exa`를 사용한다. Exa는 인증 없이 검색·페이지 읽기를 시험해 볼 수 있는 제한된 사용량도 제공하지만, 시험 중 가용량을 보장하는 것은 아니다. [Exa MCP 공식 문서](https://exa.ai/docs/get-started/exa-mcp) · [OpenAI MCP 문서](https://learn.chatgpt.com/docs/extend/mcp?surface=cli)

검색 대상은 라이브러리 공식 문서, 공개 API 명세, 일반적인 오류 해결 자료로 좁힌다. 비공개 과제 원문·코드·입력 데이터·로그를 외부 검색 서비스에 보내지 않는다. 검색이나 도구가 금지된 환경에서는 추가 연결로 우회하지 않는다.

## 4. 디자인 후보를 이렇게 골랐다

| 후보 | 이번 준비에서의 역할 | 판단 |
| --- | --- | --- |
| Impeccable | 기본 디자인 도구 | 구현→검토→수정을 연결하기 좋음 |
| Anthropic frontend-design | 설치가 간단한 대안 | 타이포그래피·레이아웃·시각 방향 지침이 필요할 때 |
| Vercel web-design-guidelines | 선택 검토 도구 | Impeccable audit만으로 부족할 때 추가 |
| Mono Charts | React 차트 컴포넌트 | 차트가 필요한 과제에서 필요한 종류만 추가 |
| awesome-design-md | 공개 디자인 참고 자료 | 필요하면 스타일 한 개만 DESIGN에 반영. [원본](https://github.com/VoltAgent/awesome-design-md) |

Stitch는 별도 생성 서비스 허용 여부와 인증을 확인해야 해서 기본 구성에서 보류했다. 주제가 정해지기 전에 여러 디자인 스킬을 모두 설치하기보다 과제에 필요한 도구부터 선택한다.

## 5. 180분 작업 운영 예시

| 경과 시간 | 할 일 |
| --- | --- |
| 0~15분 | 안내 읽기, 앱 실행, 수용 기준과 첫 작업 결정 |
| 15~95분 | 핵심 동작을 끝까지 연결하며 작은 검증 반복 |
| 95~135분 | 나머지 필수 기능, 오류·경계값·회귀 확인 |
| 135~150분 | 화면 검토와 중요한 결함 수정 |
| 150~180분 | 새 기능 동결, 최종 검증·시연·인수인계·제출 |

반복 하나는 10~20분을 목표로 한다. 같은 실패를 두 번 반복하거나 15분 동안 진전이 없으면 가설·작업 크기·접근법을 바꾼다. 검증을 통과하면 다음 요구사항으로 이동한다. 자동 반복 스케줄러나 별도 Autoresearch 시스템은 이 준비안에 추가하지 않았다.

## 6. 사전 체험에서 확인할 것

- [ ] 제공된 Codex가 프로젝트 AGENTS와 설치한 스킬을 인식하는가
- [ ] Ponytail 호출과 Impeccable 첫 실행까지 성공하는가
- [ ] 기본 검색이 되는가. 필요하면 Exa 검색과 페이지 읽기가 되는가
- [ ] 앱 서버·포트·브라우저 미리보기와 파일 저장이 되는가
- [ ] 훅, 외부 인증, 세션 전환, 커밋의 허용 범위는 무엇인가
- [ ] 설치 실패 시 README의 대안만으로 작업을 시작할 수 있는가

실패한 설치를 본 시험에서 계속 복구하느라 시간을 쓰지 않는다. AGENTS의 루프와 DESIGN의 기준으로 진행하고, 사용할 수 없는 도구는 VERIFY에 기록한다.

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
