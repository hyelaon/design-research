# design-research — 디자인 레퍼런스 리서치 자동화

한컴 AI 뉴스레터 브랜드의 **매일 디자인 자료 조사 플로우**를 Claude Code로 자동화한 스킬 패키지입니다.
탐색 → 수집 → 분류 → 무드보드 → 제작 참고까지 하루치 리서치를 반자동으로 진행합니다.

## 이게 뭔가요
매일 반복하던 "레퍼런스 찾기 → 정리 → 무드보드 만들기" 작업을 Claude Code 슬래시 명령 하나로 돌립니다.
브라우저 자동화로 후보를 모으고, **브랜드 톤 + 한글이 들어간** 레퍼런스를 자동으로 골라 저장·분류·무드보드까지 처리합니다(결과를 보고 직접 빼거나 더할 수 있음).

> 💬 **채팅 데모**: [`docs/chatbot.html`](docs/chatbot.html)을 브라우저로 열면 "디자인 리서치 봇"과 대화하는 사용 흐름을 미리 볼 수 있습니다(팀 온보딩용).

## 빠른 시작
1. [Claude Code](https://claude.com/claude-code) 설치
2. 이 저장소를 클론한 폴더에서 Claude Code 실행
3. 로그인 필요한 소스(Pinterest / COSMOS / Instagram)는 **Chrome에 미리 로그인**해 둡니다
4. 프롬프트에 입력:
   ```
   /daily-research [오늘의 테마]
   ```
5. 탐색 → 자동 큐레이션 → 분류 → 무드보드까지 대화형으로 진행됩니다 (원하면 `references/inbox/`에서 이미지를 빼거나 더해 조정)
6. 완성된 무드보드 아티팩트 확인

## 플로우
탐색(discover) → 수집(collect) → 분류(classify) → 무드보드(board) → 제작 참고(handoff)

- **한국어(한글 포함) 콘텐츠만** 수집·분류합니다. 영문 전용은 제외.
- 큐레이션까지 **Claude가 자동으로** 진행하고, 결과를 보여준 뒤 조정받습니다.

## 구성요소
| 종류 | 이름 | 역할 | 위치 |
|---|---|---|---|
| 슬래시 명령 | `/daily-research` | 하루치 전체 플로우 오케스트레이션 | `.claude/commands/daily-research.md` |
| 스킬 | `design-research` | 방법론·소스·키워드·택소노미·브랜드 컨텍스트 | `.claude/skills/design-research/SKILL.md` |
| 서브에이전트 | `design-scout` | 브라우저 자동화로 레퍼런스 후보 탐색 | `.claude/agents/design-scout.md` |
| 서브에이전트 | `design-classifier` | inbox 이미지 분석·분류 | `.claude/agents/design-classifier.md` |

브라우저 자동화는 `claude-in-chrome` MCP(로그인된 Chrome 세션)를 사용합니다 — 별도 서버 설치가 필요 없습니다.

## 폴더 구조
```
references/
  brand-context.md      # 브랜드 톤·목적 (팀에 맞게 수정해서 사용)
  benchmark-brands.md   # 벤치마크 타브랜드 목록
  inbox/                # 큐레이션한 최종 이미지를 여기에 저장 (git 미포함)
data/                   # candidates / analysis JSON — 날짜별 자동 생성 (git 미포함)
boards/                 # 생성된 HTML 무드보드 — 자동 생성 (git 미포함)
```

## 다른 브랜드에 적용하려면
`references/brand-context.md`와 `references/benchmark-brands.md`를 우리 브랜드에 맞게 바꾸면 그대로 재사용할 수 있습니다.

## 주의
- 레퍼런스는 **"참고"용** — 출처를 항상 기록하고 무단 복제 금지
- 민감정보·계정정보는 어떤 산출물에도 넣지 않습니다
- `data/`·`boards/`·`inbox/` 생성물과 개인 로컬 설정(`.claude/settings.local.json`)은 저장소에 포함하지 않습니다
