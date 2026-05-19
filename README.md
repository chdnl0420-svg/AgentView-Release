# AgentView — 배포 저장소

> Claude Code 의 백그라운드 에이전트를 한글이 깨지지 않는 데스크톱 UI 로 관리하는 Electron 앱.
> 이 저장소는 **배포(installer) 전용** 입니다. 소스 코드는 [chdnl0420-svg/AgentView](https://github.com/chdnl0420-svg/AgentView) 에 있습니다.

## 다운로드

언제나 **최신 버전 하나만** 유지됩니다. 아래 링크에서 받으세요.

- **최신 인스톨러 (자동 리다이렉트)**: [Releases / latest](https://github.com/chdnl0420-svg/AgentView-Release/releases/latest)
- **직링크 (변경 없음)**: `https://github.com/chdnl0420-svg/AgentView-Release/releases/latest/download/AgentView-Setup.exe`

> `releases/latest/download/<asset>` URL 은 GitHub 이 항상 최신 release 의 asset 으로 redirect 합니다. 스크립트·자동 업데이트도 이 URL 을 사용하세요.

## 주요 기능

- **CLI 와 1:1 동기화** — `~/.claude/jobs/<short>/state.json` 을 직접 읽어 `claude agents` 의 목록과 정확히 일치
- **새 작업 dispatch** — daemon 채널로 새 `kind:"bg"` 워커 생성 (1.5–5 초)
- **AskUserQuestion 응답 UI** — 입력창 위 sticky 패널로 옵션 클릭 → 즉시 전송
- **inline 권한 prompt** — TUI 의 "Do you want to ...?" 를 모달로 surfacing
- **컨텍스트 사용량 도넛** — 헤더 도넛 클릭 시 현재 토큰 / max context / 모델 표시
- **권한 모드 선택** — `default / acceptEdits / bypassPermissions / plan` (Max 계정만 bypassPermissions)
- **자동 업데이트** — GitHub Releases 폴링, 1-클릭 설치 + 재시작
- **마우스 뒤로/앞으로** — XButton1 / XButton2 로 dashboard ↔ detail 이동
- **세션 이름 변경** — AgentView 에서 변경하면 `claude agents` CLI 에서도 동일하게 표시
- **상태 색 구분** — 실행 중(초록) / 대기(파랑) / 완료(청록) / 종료(회색)

## 빠른 시작

1. 위 다운로드 링크에서 `AgentView Setup x.y.z.exe` 받기 → 실행.
2. 설치가 끝나면 바탕화면 바로가기가 자동 생성됩니다.
3. 앱을 처음 실행하면 6 단계 튜토리얼이 표시됩니다.
4. 하단 입력창에 작업 입력 → 권한 모드 선택 → **Ctrl + Enter** 로 새 작업 시작.
5. 카드를 클릭해 detail 진입, 추가 메시지 전송 / 권한 prompt 응답.

## 단축키

| 조작 | 동작 |
|---|---|
| Ctrl + Enter | 메시지 전송 (또는 새 작업 시작) |
| Esc | detail view 닫기 (dashboard 로) |
| 마우스 XButton1 (뒤로) | dashboard 복귀 |
| 마우스 XButton2 (앞으로) | 마지막 detail view 복귀 |
| ↑ / ↓ (입력창에서) | 이전 전송 히스토리 탐색 |
| 우클릭 (입력창) | 잘라내기 / 복사 / 붙여넣기 / 모두 선택 |

## 권한 모드

| 라벨 | claude flag | 설명 |
|---|---|---|
| 기본 확인 | `default` | 매 도구마다 사용자 확인 |
| 편집만 자동 | `acceptEdits` | 파일 편집은 자동, 그 외 도구는 확인 |
| 전체 허용 (Max 전용) | `bypassPermissions` | 모든 도구 자동 실행 — Max 계정 필요 |
| 계획 모드 | `plan` | 읽기 전용, 변경 없음 |

## 시스템 요구사항

- Windows 10/11 (x64)
- `claude` CLI ≥ 2.1.141, daemon 실행 중 (`~/.claude` 사용)
- 디스크 약 200MB

## 배포 정책 — 최신만 유지

이 저장소는 **항상 1개의 release 만** 유지합니다.

- 새 버전이 publish 되면 `.github/workflows/keep-latest.yml` 이 자동으로
  - 이전 release 전부 삭제
  - 이전 git tag 전부 삭제
  - 새 release 만 `latest` 로 남김
- 따라서 사용자는 **항상 최신 인스톨러만** 받게 됩니다 (구버전 노출 0).

배포자 절차는 [PUBLISH.md](PUBLISH.md) 참조.

## 라이선스

MIT — 소스 저장소와 동일.
