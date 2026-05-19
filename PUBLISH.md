# Publishing a new AgentView release

> 이 저장소는 **항상 최신 1개 릴리즈만** 유지합니다. 새 버전을 publish 하면 `.github/workflows/keep-latest.yml` 이 이전 release / tag 를 자동 정리합니다.

## 절차 (source repo `AgentView` 에서)

1. `package.json` 의 `version` 을 새 버전으로 올린다 (예: `1.0.1`).
2. `npm run build:win` 으로 NSIS 인스톨러 빌드 → `dist/AgentView Setup <ver>.exe` 생성.
3. `RELEASE_NOTES.md` 를 새 버전 변경점으로 갱신.
4. release repo 에 새 릴리즈 publish (한 줄):

   ```bash
   VER=1.0.1
   gh release create "v$VER" \
     --repo chdnl0420-svg/AgentView-Release \
     --title "AgentView v$VER" \
     --notes-file RELEASE_NOTES.md \
     "dist/AgentView Setup $VER.exe" \
     "dist/AgentView Setup $VER.exe.blockmap"
   ```

5. `keep-latest` 워크플로우가 자동으로 이전 release/tag 를 삭제합니다.
6. 사용자는 `releases/latest/download/<asset>` 로 항상 최신본을 받습니다.

## 자동 업데이트 (앱 내부)

앱은 `repos/chdnl0420-svg/AgentView-Release/releases/latest` 를 폴링합니다. publish 후 1 시간 이내에 모든 사용자에게 업데이트 배너가 표시됩니다.

## 디버깅

- 워크플로우 로그: `Actions` 탭 > `Keep only latest release`
- 수동 실행: 새 release 를 publish 하면 자동 트리거. 임의 트리거가 필요하면 `workflow_dispatch` 추가 가능.
