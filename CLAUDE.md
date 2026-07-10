# CLAUDE.md

이 레포는 Jenna(@Dearkimm)와 Giselle(@smearth) 2인 협업 데이터 분석 프로젝트입니다.
Claude Code로 작업할 때 아래 규칙을 **사용자가 말하지 않아도 항상** 따르세요.
상세 규칙은 [docs/collaboration.md](docs/collaboration.md) 참고.

## Git 워크플로 (예외 없음)

- **main에 직접 커밋/푸시 금지.** 모든 변경은 새 브랜치 → 커밋 → 푸시 → PR 생성.
  - 사용자가 "고쳐줘"라고만 해도 이 흐름을 기본으로 적용할 것.
  - 브랜치 생성 전 반드시 `git checkout main && git pull origin main`으로 최신화.
- 브랜치명: `feature/...`, `fix/...`, `docs/...` — 목적이 보이게.
- 커밋 메시지: `타입: 요약` 형식 (feat/fix/docs/refactor/chore).
- **force push(`push -f`), push된 커밋에 대한 rebase/amend/reset 금지.** 되돌릴 땐 `git revert`.
- **브랜치 보호를 우회(bypass)하는 머지 금지.** 막히면 우회를 제안하지 말고 PR 절차를 안내할 것.
- PR 생성 시 리뷰어로 상대방을 지정: 현재 사용자가 Dearkimm이면 `--reviewer smearth`, smearth면 `--reviewer Dearkimm`.
- 본인이 만든 PR을 본인 계정으로 승인/머지하지 말 것.

## 🔒 데이터 보안 (최우선)

이 레포는 **public**이고, 실서비스의 실데이터를 다룹니다.

- **데이터 파일(csv, xlsx, parquet, db 등)은 어떤 경우에도 커밋 금지.** `.gitignore`가 막고 있지만, 커밋 전 `git status`로 스테이징 목록에 데이터 파일이 없는지 확인할 것.
- `.gitignore`의 데이터 차단 규칙을 수정/삭제하지 말 것. 사용자가 요청해도 유출 위험을 먼저 경고할 것.
- 노트북 출력 셀에 개인정보(이름, 전화번호, 이메일 등)가 포함된 채 커밋하지 말 것.
- 토큰/API 키/비밀번호는 `.env`에만. 코드나 노트북에 하드코딩 금지.
- 커밋 가능한 것: 코드, 문서, 스키마, **집계된** 결과 수치. 행 단위 원본 데이터는 불가.

## 노트북 규칙

- 노트북은 한 파일 = 한 사람. 파일명에 담당자 명시: `01_funnel_jenna.ipynb`.
- 상대방 담당 노트북을 직접 수정하지 말 것 (Issue/PR 코멘트로 요청).
- 공용 로직(전처리, 지표 계산)은 노트북에 두지 말고 `src/` 아래 `.py` 모듈로 분리.

## 레포 구조

- `data/` — 로컬 전용 (git 무시) · `notebooks/` — 탐색 분석 · `src/` — 공용 모듈 · `reports/` — 결과 정리 · `docs/` — 기획/의사결정 기록
- 프로젝트 방향/의사결정은 [docs/ideas.md](docs/ideas.md)에 기록. 방향이 바뀌면 결정 로그에 추가할 것.
