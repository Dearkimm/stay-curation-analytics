# 협업 규칙 (GitHub Flow)

2인 협업 기준의 최소 규칙. 복잡한 Git Flow 대신 GitHub Flow 하나만 씁니다.

## 기본 원칙

1. **`main`에 직접 커밋 금지.** 항상 브랜치 → PR → 상대방 리뷰 → 머지.
2. **작업 시작 전 항상 최신화.** 충돌의 90%는 이걸 안 해서 생김.
   ```bash
   git checkout main
   git pull origin main
   git checkout -b feature/작업내용
   ```
3. **브랜치명 규칙**: 목적이 보이게.
   - 분석/기능: `feature/funnel-analysis`
   - 수정: `fix/date-parsing`
   - 문서: `docs/update-schema`
4. **PR은 작게, 자주.** 일주일치 작업을 한 PR에 몰지 말 것. 리뷰 가능한 크기(노트북 1개, 모듈 1개 수준)로.
5. **머지는 리뷰어(상대방)가.** 본인 PR을 본인이 머지하지 않기 — 리뷰 문화 연습.

## 노트북 충돌 방지 (가장 중요)

주피터 노트북은 JSON이라 충돌이 나면 수동 해결이 매우 어렵습니다.

- **같은 노트북 파일을 두 명이 동시에 수정하지 않기.** 파일 단위로 담당을 나눔.
- 노트북 파일명에 담당자 이니셜 또는 주제를 명시: `01_funnel_kim.ipynb`
- 공용 로직(전처리, 지표 계산)은 노트북에 두지 말고 `src/` 아래 `.py` 모듈로 분리.
- (선택) `nbstripout`을 설치하면 출력 셀이 자동 제거되어 diff가 깨끗해짐:
  ```bash
  pip install nbstripout
  nbstripout --install   # 레포 클론 후 각자 1회 실행
  ```

## 이슈 연동

- 할 일은 GitHub Issues로 등록하고, PR 본문에 `closes #이슈번호`를 적으면 머지 시 자동으로 닫힘.
- 협업 이력이 레포에 그대로 남아 그 자체로 포트폴리오가 됨.

## 커밋 메시지

- 형식: `타입: 요약` — 예) `feat: 유입 채널별 전환율 집계 추가`, `docs: 스키마 문서 작성`
- 한 커밋 = 한 가지 변경. "이것저것 수정" 금지.

## 충돌이 났을 때

1. 당황하지 말 것. 충돌은 정상적인 과정.
2. `git status`로 충돌 파일 확인 → 파일 열어 `<<<<<<<` 마커 부분을 상의해서 정리 → `git add` → `git commit`.
3. 노트북에서 충돌이 났고 해결이 어렵다면, 어느 한쪽 버전을 통째로 채택:
   ```bash
   git checkout --ours 파일명    # 내 버전 채택
   git checkout --theirs 파일명  # 상대 버전 채택
   ```
