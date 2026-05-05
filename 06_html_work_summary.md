# HTML 뼈대 작업 요약

---

## 현재 파일
`index.html` — 36개 슬라이드 단일 파일

---

## 기술 스펙

### 라이브러리
- Reveal.js 4.6.1 (CDN)
- Noto Sans KR (Google Fonts)

### Reveal.js 설정
```javascript
Reveal.initialize({
  width: 1920,
  height: 1080,
  margin: 0,
  minScale: 0.1,
  maxScale: 3,
  controls: false,
  progress: false,
  history: true,
  keyboard: true,
  overview: false,
  center: false,
  touch: true,
  loop: false,
  transition: 'slide',          // 슬라이드 전환 (앞 슬라이드가 밀려나고 다음이 드러남)
  transitionSpeed: 'default',
  backgroundTransition: 'none',
  embedded: false,
  mouseWheel: false,
});
```

---

## 레이아웃 구조

### 네비게이션 바
- `position: fixed; top: 0; z-index: 9999`
- 슬라이드 위에 투명하게 얹히는 구조 (슬라이드는 전체 1920×1080)
- 배경: `rgba(30,30,30,0.75)` + `backdrop-filter: blur(12px)`
- 높이: 52px
- 좌측: "AI Agent Experience" 로고
- 우측: Part 1~5 탭 + 호버 시 드롭다운

### 드롭다운 구조
- Part 1~3, 5: 페이지 목록 직접 표시
- Part 4만: 챕터 그룹 헤더(클릭 불가) + 하위 페이지 목록
  - 디자이너가 만드는 것이 달라졌다 (4.1~4.4)
  - 에이전트와 일하기: 반복은 맡기고, 한계는 없애고 (4.5~4.6)
  - 개발자-에이전트-디자이너, 함께 일하기 (4.7~4.9)
  - Conclusion (지능이 벌어다 준 시간: 디자이너의 새로운 격차)
- 좌측 "AI Agent Experience" 로고 클릭 시 표지(0번 슬라이드)로 이동

### 화살표 버튼
- `position: fixed; bottom: 20px; left: 50%`
- 다크 프로스티드 글래스 알약 형태 (반투명 회색 + backdrop-blur 20px)
- ← 슬라이드번호/전체 → 형태
- 흰 글자 + text-shadow로 다크/데이모드 양쪽 가독성 확보

---

## 슬라이드 타입별 클래스

### 풀스크린 슬라이드 `.s-full`
표지, 파트 표지, 챕터 간지에 사용
- 배경: CSS 그라데이션 클래스 (`.g-cover`, `.g-p1`~`.g-p5`, `.g-chap`)
- 텍스트: 우측 정렬, 세로 위치는 `padding-top`으로 조정
- 구성 요소: `.plabel` (소제목) + `.ptitle` (본제목) + `.psub` (부제)

**⚠️ 미해결 이슈:**
현재 풀스크린 슬라이드의 텍스트 세로 위치가 브라우저 창 크기에 따라 달라지는 문제 있음.
Reveal.js `center: false` + `padding-top` 방식으로 시도 중이나 정확한 중앙 배치가 안 됨.
Claude Code에서 로컬 서버로 확인하면서 수정 필요.

### 콘텐츠 슬라이드 `.s-page`
일반 내용 페이지에 사용
- 배경: `#0a0a0a`
- padding: `88px 96px 52px` (상단 padding으로 navbar 가림 방지)
- 구성: `.plabel` + `.ptitle` + `.pcap` + `.body`

### 콘텐츠 컴포넌트 (현재 사용 중)
- `.card` (+ `.c-label` `.c-sub` `.c-title` `.c-desc`) — 기본 콘텐츠 카드
- `.tbl` `.tbl-row` `.tbl-cell` (+ `.head` `.insight` 변형) — 데이터 테이블
- `.tbl-group` (+ `.tbl-cat` `.insight-body`) — 행 그룹화 테이블 (1.3, 1.4)
- `.info-box` (+ `.ib-title` `.ib-body`) — 헤더 + 본문 박스
- `.bullet-list` — 불릿 리스트
- `.kw` `.kws` — 키워드 칩
- `.train` (+ `.train-step` `.train-arrow`) — 가로 파이프라인 (3.1)
- `.theory-tag` — 카드 하단 Theory 태그
- `.converge` (+ `.converge-row` `.converge-box` `.converge-op` `.converge-result`) — 수렴 다이어그램
- `.captured-slide` (4.1, 4.2 흰 종이 mockup) + 부속 (`.cs-header` `.cs-body` `.cs-left` `.cs-right` `.cs-tag` `.cs-filename` `.cs-link-title` `.cs-continuation` `.slide-meta` `.md-section` `.md-label` `.md-body` `.md-bullets` `.mini-tbl` 등)
- `.section-overlay` (+ `.overlay-chart` `.overlay-filename` `.overlay-rightcol` `.overlay-hitl` `.overlay-rules`) — 컬러 사각형 오버레이
- `.leader-lines` (SVG) — 오버레이 ↔ 콜아웃 표시선
- `.cp-overlay` (+ `.cp-num` `.cp-aside` `.cp-1` `.cp-2` `.cp-3` `.cp-42-1` `.cp-42-2`) — 프로스티드 글래스 콜아웃 + 번호 배지
- `.dot` (+ `.dot-mcp` `.dot-api` `.dot-lib` `.dot-claude`) — 컬러 범례 도트
- `.proto-grid` (+ `.proto-level` `.pl-header` `.pl-num` `.pl-name` `.pl-train` `.pl-box` `.pl-arrow` `.pl-footer` `.pf-item` `.pf-label` `.pf-text` `.pl-prompt` `.pl-note`) — 4.6 퀵 프로토타이핑 4단계 차트
- `.part-row` (+ `.p-num` `.p-area` `.p-info` `.p-label` `.p-desc`) — 봇 부위 카드 (2.1)
- `.principle-item` (+ `.pi-label` `.pi-desc`) — 행동 원칙 항목 (4.2)
- `.hitl-msg` — 메시지 코드 블록 (4.2)
- `.tree` `.tree-root` `.tree-item` — 계층 트리 (사용 보류)
- `.footnote` — 작은 주석
- 그리드 헬퍼: `.g2`, `.g3`, `.g4`, `.fw`
- 와이어프레임 플레이스홀더: `.wf` (`.wf.circle`) — 점차 콘텐츠로 교체됨

---

## 슬라이드 순서 및 goTo() 인덱스

| 인덱스 | 슬라이드 |
|--------|---------|
| 0 | Cover |
| 1 | Part 1 표지 |
| 2 | 1.1 AI 에이전트의 정의 |
| 3 | 1.2 디자인 R&R의 확장 |
| 4 | 1.3 디자인 대상의 전환 |
| 5 | 1.4 디자인 프로세스의 진화 |
| 6 | Part 2 표지 |
| 7 | 2.1 에이전트 존재의 설계도 |
| 8 | 2.2 에이전트 액추에이터 |
| 9 | 2.3 도구에서 스킬로 |
| 10 | 2.4 메모리 아키텍처 |
| 11 | 2.5 OpenClaw와 Agentic AI Framework |
| 12 | Part 3 표지 |
| 13 | 3.1 Human-in-the-loop |
| 14 | 3.2 Generative UI |
| 15 | 3.3 Ambient AX |
| 16 | Part 4 표지 |
| 17 | Chap A 간지 |
| 18 | 4.1 화면 기획에서 로직 기획으로 |
| 19 | 4.2 하네스 엔지니어링 |
| 20 | 4.3 직접 만들기 |
| 21 | 4.4 디자인시스템의 진화 |
| 22 | Chap B 간지 |
| 23 | 4.5 디자인 자동화 루틴 |
| 24 | 4.6 코딩 에이전트와 퀵 프로토타이핑 |
| 25 | Chap C 간지 |
| 26 | 4.7 정적 가이드에서 실행 가능한 로직으로 |
| 27 | 4.8 시각적 검수에서 시스템적 검증으로 |
| 28 | 4.9 레이아웃 전달에서 구조적 페어링으로 |
| 29 | Part 4 Conclusion |
| 30 | Part 5 표지 |
| 31 | 5.1 버티컬 에이전트 Preset 전략 |
| 32 | 5.2 특화 지능: 인지와 기억 에이전트 |
| 33 | 5.3 Skill-as-a-Service |
| 34 | 5.4 No-code 에이전트 조립 도구 |
| 35 | 5.5 멀티 디바이스 오케스트레이션 |

---

## 커버 슬라이드 내용
- 소제목 (plabel): Introduction of AX
- 본제목 (ptitle): AI 에이전트 경험
- 부제 (psub): 개념 이해와 예제

---

## 진행 상황 요약 (2025-05 기준)

### 완료
- ✅ 풀스크린 슬라이드 텍스트 세로 정렬 (1920×1080 고정 + center 정렬로 해결)
- ✅ 네비게이션 드롭다운 goTo() 인덱스 정확히 매핑
- ✅ Cover, Part 1~3 콘텐츠 전체 채움
- ✅ Part 4 Chap A (4.1~4.4): mockup 양식 적용 (4.1, 4.2는 흰 종이 캡처 슬라이드 + 오버레이/콜아웃)
- ✅ Part 4 Chap B (4.5~4.6): 4.6은 4컬럼 세로 흐름 + 프롬프트 템플릿
- ✅ Part 4 Chap C (4.7~4.9): 3카드 패턴 (4.10은 삭제됨)
- ✅ 띄어쓰기 통일: "시스템 프롬프트"
- ✅ 페이지 컨트롤 알약 (다크/데이모드 양쪽 가독성)
- ✅ 로고 클릭 시 표지 이동

### 진행 중 / 남은 작업
1. **콘텐츠 채우기**
   - Part 4 Conclusion (인덱스 29)
   - Part 5 (인덱스 31~35)

2. **키 스크린 3개 선택 후 Claude Design 시안 작업**

3. **최종 디자인 적용**

---

## 주요 디자인 패턴 (현재 사용)

### 4.1, 4.2 캡처 슬라이드 mockup
- 다크 슬라이드 위에 흰 종이(off-white #f8f7f3) 캡처 슬라이드가 그림자와 함께 떠 있는 형태
- 슬라이드 하단은 자연스럽게 크롭
- 좌상단 외곽에 메타 주석 (`.slide-meta`)
- 각 섹션 위에 반투명 보라 사각형 오버레이 + 점선 표시선 + 프로스티드 글래스 콜아웃 (번호 배지 1, 2, 3)
- 콜아웃 스타일: 반투명 흰 배경 + 보라 테두리 + backdrop-blur (비치는 콘텐츠 흐림 처리)

### 4.6 4컬럼 세로 흐름 차트
- 4개 레벨 (L1~L4) 컬럼이 슬라이드 폭을 균등 분할
- 각 컬럼 세로 흐름: 목적 → 결과물 → 헤더 → 흐름도(↓ 메인 / ⋮ 대안) → 프롬프트 템플릿 → 주석(L4)

### 캡처 슬라이드 컬러 범례 (4.1)
- MCP 서버: #7B6FE8 (보라)
- API 서비스: #14C19A (녹색)
- 기성 라이브러리: #E8732B (주황)
- Claude 내장 스킬: #FFFFFF (흰색 + 회색 외곽선)
