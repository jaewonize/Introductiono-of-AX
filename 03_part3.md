# Part 3. 인터랙션 문법: 에이전트 경험의 핵심 설계

---

## 3.1 Human-in-the-loop 사고과정의 공유와 개입

**페이지 구성:** 상단 에이전트 실행 단계 기차 블록 + 하단 하이라이트 블록별 카드 + Theory 블록 연결

**도입 카피:** "지능이 인간을 불러야 한다고 판단하는 명분과 절차"

### 상단: 에이전트 실행 단계 기차 블록 (가로 1줄)

User Request → Goal Interpretation → Task Planning → Agent/Tool Selection → Information Gathering → Option Generation → Evaluation/Negotiation → Action Execution → Observation → Feedback/Refinement

- **컬러 하이라이트 블록:** Goal Interpretation / Evaluation/Negotiation / Feedback/Refinement
- **작은 주석:** AutoGPT, LangChain Agents, CrewAI, CAMEL Multi-agent 프레임워크에서 공통적으로 나타나는 단계를 참고해 작성

### 하단: 하이라이트 블록 → 카드 → Theory 블록 연결 구조

**① Goal Interpretation**
↓
목적: Goal Alignment
AI-사용자 의도 간 misalignment가 자주 발생
> 사용자의 의도를 명확히 드러내고 AI와의 목표 정렬 필요
↓
Theory: Mental Model / Constructed Preference

**② Evaluation/Negotiation**
↓
목적: Decision Support
멀티에이전트 환경에서는 옵션이 급격히 증가
> 인간의 인지 부담을 줄이면서 합리적 선택을 도울 필요
↓
Theory: Bounded Rationality / Prospect Theory

**③ Feedback/Refinement**
↓
목적: Adaptive Learning
피드백 = 단순 평가가 아닌 모델 개선에 활용
> 사용자 경험 기반 AI 지속 학습 및 신뢰 관계 형성 필요
↓
Theory: Reinforcement Learning / Trust Calibration

*Theory 블록: 이름만 표기, 추후 링크 추가 예정

---

## 3.2 유동적 인터페이스 Generative UI

**페이지 구성:** 상단 기존 앱 UX vs 에이전트 UX 2블록 + 중단 Generative UI 3가지 생성 방식 테이블 + 하단 DESIGN.md 섹션

**도입 카피:** "에이전트가 답변의 성격과 의도에 따라 UI를 스스로 결정하고 생성하는 인터페이스 패러다임"

### 상단: 기존 앱 UX vs 에이전트 UX (2블록 대비)

**기존 앱 UX**
미리 설계된 화면 레이아웃과 확정된 에셋 라이브러리 안에서만 작동. 사용자가 할 수 있는 행동과 볼 수 있는 정보가 설계 시점에 모두 확정됨. 설계되지 않은 상황은 존재하지 않음.

**에이전트 UX**
답변의 성격·의도·데이터 구조에 따라 그때그때 가장 적합한 UI를 에이전트가 판단하고 생성. 사전에 모든 상황을 설계할 수 없기 때문에 UI 자체가 동적으로 만들어져야 함.

### 중단: Generative UI의 3가지 생성 방식 (테이블)

| 방식 | 설명 | 적합한 상황 |
|------|------|------------|
| **Rule-based Generation** | 상황별 최적 UI 룰이 사전 정의되어 있고 에이전트가 룰을 참조해 UI 결정 | 반복적·예측 가능한 답변 유형 |
| **Library-based Generation** | UI 컴포넌트 라이브러리에서 에이전트가 적합한 컴포넌트를 조합해 생성 | 구조화된 데이터, 비교·선택이 필요한 상황 |
| **From Scratch Generation** | 기존 룰이나 라이브러리로 커버되지 않는 예외적 상황에서 에이전트가 UI를 직접 설계 | 경향을 벗어난 복합적·특수한 답변 |

### 하단: DESIGN.md — 에이전트를 위한 디자인 시스템

위 테이블의 **Rule-based Generation**의 실제 구현체. 기존 디자인 시스템을 에이전트가 자동으로 읽고 적용 가능한 표준 형식으로 변환.

**기존 방식 vs DESIGN.md 방식 (2블록 비교)**

**기존 방식**
에이전트에게 매번 브랜드 컬러·폰트·컴포넌트를 설명해야 함. 툴을 바꿀 때마다, 새 대화를 시작할 때마다 처음부터 다시.

**DESIGN.md 방식**
파일 하나로 끝. YAML 토큰(정확한 값) + 마크다운 텍스트(왜 이 값인지 이유)를 함께 담아 에이전트가 자동으로 읽고 적용. Google Labs가 2026년 4월 오픈소스로 공개. Claude Code, Cursor, Copilot 모두 지원.

---

## 3.3 비가시적 경험 Ambient AX

**페이지 구성:** 상단 정의 1블록 + 중단 HITL·Generative UI 수렴 다이어그램 + 하단 설계 원칙 테이블

**도입 카피:** "HITL과 Generative UI가 만나는 최적 지점"

### 상단: Ambient AX의 정의 (1블록)

제로 인터랙션이 아닌 미니멈 인터랙션. 에이전트가 백그라운드에서 조용히 작동하다가, 꼭 인간이 필요한 순간에만 개입을 요청하고, 그 순간에 가장 적합한 형태의 UI를 생성해 출력하는 경험. 존재감을 최소화하되 개입의 질을 극대화하는 인터페이스 철학.

### 중단: HITL + Generative UI 수렴 다이어그램

HITL × Generative UI → Ambient AX

- HITL: 꼭 필요한 순간에만 인간을 부름
- Generative UI: 그 순간에 최적의 UI를 생성해 출력
- 수렴 메시지: "불렸을 때 완벽하게"

HITL의 기여: 불필요한 개입을 걷어내고 꼭 필요한 순간만 남김
Generative UI의 기여: 그 순간에 맥락에 맞는 UI를 즉석에서 생성

### 하단: Ambient AX의 3가지 설계 원칙 (테이블)

| 원칙 | 내용 |
|------|------|
| **Invisible by default** | 에이전트는 기본적으로 보이지 않음. 작동 중이라는 신호만 최소한으로 |
| **Visible when needed** | 개입이 필요한 순간, 맥락에 맞는 최적 UI로 존재를 드러냄 |
| **Gone when done** | 개입이 끝나면 다시 사라짐. 잔여 UI를 남기지 않음 |
