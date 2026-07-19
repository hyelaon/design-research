# design-research — 디자인 레퍼런스 리서치 자동화

AI 뉴스레터 브랜드의 매일 디자인 자료 조사 플로우를 자동화한 프로젝트다.

## 플로우
탐색(discover) → 수집(collect) → 분류(classify) → 무드보드(board) → 제작 참고(handoff)

## 구성요소
- **스킬** `design-research` — 방법론·소스·키워드·택소노미·브랜드 컨텍스트 (`.claude/skills/design-research/SKILL.md`)
- **서브에이전트** `design-scout` — 브라우저 자동화로 레퍼런스 후보 탐색 (`.claude/agents/design-scout.md`)
- **서브에이전트** `design-classifier` — inbox 이미지 분석·분류 (`.claude/agents/design-classifier.md`)
- **슬래시 명령** `/daily-research` — 하루치 전체 플로우 오케스트레이션 (`.claude/commands/daily-research.md`)
- **MCP** — 브라우저 자동화는 `claude-in-chrome` MCP(사용자의 로그인된 Chrome 세션) 사용. 별도 서버 설치 불필요.

## 폴더
- `references/inbox/` — 큐레이션한 최종 이미지를 여기에 저장(드롭)
- `references/brand-context.md` — 브랜드 톤·목적 (확인 후 채움)
- `references/benchmark-brands.md` — 벤치마크 타브랜드 목록
- `data/` — candidates / analysis JSON (날짜별)
- `boards/` — 생성된 HTML 무드보드

## 사용법
1. 이 폴더에서 Claude Code 실행
2. `/daily-research [오늘의 테마]` 입력
3. 후보가 모이면 마음에 드는 이미지를 `references/inbox/`에 저장 → "분류" 입력
4. 무드보드 아티팩트 확인

## 주의
- 로그인 필요한 소스(Pinterest/COSMOS/Instagram)는 Chrome에 미리 로그인해 둘 것
- 레퍼런스는 "참고"용 — 출처를 항상 기록하고 무단 복제 금지
- 민감정보/계정정보는 산출물에 넣지 않음
