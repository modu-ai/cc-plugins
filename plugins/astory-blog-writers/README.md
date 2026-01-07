# aStory Blog Writers 플러그인

> Hybrid Author System v2.0으로 구동되는 DNA 기반 블로그 작성 시스템

[![Version](https://img.shields.io/badge/version-2.0.0-blue.svg)](https://github.com/modu-ai/claude-plugins)
[![License](https://img.shields.io/badge/license-MIT-green.svg)](LICENSE)
[![Claude Code](https://img.shields.io/badge/Claude%20Code-Plugin-purple.svg)](https://claude.ai)

## 개요

aStory Blog Writers는 혁신적인 Hybrid Author System v2.0을 기반으로 구축된 Claude Code 플러그인으로, DNA 기반 특성 조합을 통해 독특하고 진정성 있는 블로그 콘텐츠를 생성합니다. 16개의 원자적 특성(Trait)을 조합하여 8개의 사전 설정 페르소나를 제공하며, 3가지 작성 모드를 통해 다양한 요구사항에 맞춘 콘텐츠 제작이 가능합니다.

### 주요 기능

#### Hybrid Author System v2.0

**1. Trait DNA Library (16개 특성)**
- **Voice 패턴 (4개)**: Formal, Conversational, Narrative, Technical
- **Expertise 영역 (4개)**: Architecture, Implementation, Industry, Education
- **Perspective 스타일 (4개)**: Analytical, Experiential, Critical, Visionary
- **Tone 특성 (4개)**: Authoritative, Empathetic, Provocative, Nurturing

**2. 8개 Preset Personas**
각 페르소나는 4가지 특성의 고유한 조합으로 구성됩니다:
- Architect (아키텍트) - 시스템 설계 전문가
- Developer (개발자) - 실무 구현 전문가
- Storyteller (스토리텔러) - 경험 서사 작가
- Mentor (멘토) - 교육 가이드
- Analyst (분석가) - 산업 트렌드 분석가
- Reviewer (리뷰어) - 제품 평가자
- Curator (큐레이터) - 뉴스 정리자
- Columnist (칼럼니스트) - 오피니언 논객

**3. 3가지 Writing Modes**
- **Solo Mode**: 단일 페르소나로 빠르고 일관된 작성
- **Crew Mode**: 7개 역할의 협업으로 최고 품질 콘텐츠 생산
- **Adaptive Mode**: 섹션별 자동 페르소나 전환

**4. Anti-AI Pattern Validation**
- 분리된 검증 스킬로 재사용 가능
- 자동 검증 훅 통합
- 3단계 탐지: 금지 표현, 경고 표현, 구조적 패턴
- AI 탐지 가능 표현 자동 수정 제안

**5. 연구 시스템**
- 웹 검색 프로토콜
- 미디어 수집 (이미지, YouTube)
- 소스 검증 및 인용 관리

### 차별화 요소

일반적인 AI 작성 도구와 달리 aStory Blog Writers는 다음을 제공합니다:

- **DNA 기반 페르소나**: 고정된 프롬프트가 아닌 특성 조합으로 256+ 가능한 조합 생성
- **멀티모드 작성**: 상황에 맞는 최적의 작성 프로세스 선택
- **협업 시스템**: Crew Mode에서 7개 역할의 전문화된 검토 프로세스
- **섹션별 최적화**: Adaptive Mode로 각 섹션마다 최적의 페르소나 자동 선택
- **한국어 최적화**: 한다체, 해요체, 서사체 등 한국어 작성 스타일 완벽 지원
- **AI 탐지 방지**: 진정성 있는 목소리 유지를 위한 자동 검증
- **독립 실행**: MoAI-ADK 의존성 없이 어디서나 사용 가능

## 설치

### 사전 요구사항

- Claude Code CLI 설치됨
- Git (저장소에서 설치하는 경우)

### GitHub 저장소에서 설치

```bash
claude plugin install modu-ai/claude-plugins/astory-blog-writers
```

### 로컬 디렉토리에서 설치

```bash
claude plugin install --local /path/to/astory-blog-writers
```

### 설치 확인

```bash
claude plugin list
```

활성 플러그인 목록에서 `astory-blog-writers`를 확인할 수 있어야 합니다.

## 사용 가이드

### 빠른 시작

1. **콘텐츠 작성 시작**:
   ```
   /post "확장 가능한 마이크로서비스 구축 방법"
   ```

2. **작성 모드 선택**:
   - **Solo Mode**: 빠른 단일 작성 (일반 블로그 포스트)
   - **Crew Mode**: 고품질 협업 작성 (중요한 기술 아티클)
   - **Adaptive Mode**: 섹션별 최적화 작성 (복합 주제)

3. **페르소나 선택** (Solo/Adaptive Mode):
   - 8개 프리셋 페르소나 중 선택
   - 또는 Custom DNA로 자신만의 특성 조합 생성

4. **자동 워크플로우**:
   - 리서치 에이전트가 관련 정보 수집
   - 선택된 모드에 따라 콘텐츠 생성
   - Anti-AI 검증 자동 실행
   - 최종 콘텐츠 제공

### Solo Mode (빠른 작성)

**언제 사용?**
- 일반적인 블로그 포스트
- 빠른 튜토리얼
- 개인 생각 정리
- 일관된 목소리가 필요한 경우

**워크플로우**:
```
/post "React 19 새로운 기능"
→ Solo Mode 선택
→ Developer 페르소나 선택
→ 단일 작가 스타일로 빠르게 작성 완료
```

**장점**:
- 빠른 작성 (5-10분)
- 일관된 목소리
- 간단한 프로세스

### Crew Mode (고품질 협업)

**언제 사용?**
- 중요한 기술 아티클
- 논쟁적인 주제
- 포괄적인 가이드
- 최고 품질이 필요한 경우

**7개 역할 협업 프로세스**:

1. **Creative Director**: 아이디어 발굴 및 각도 결정
2. **Research Analyst**: 심층 리서치 및 소스 수집
3. **Lead Writer**: 주요 콘텐츠 초안 작성
4. **Technical Reviewer**: 기술적 정확성 검증
5. **Reader Advocate**: 가독성 및 명확성 검토
6. **Devil's Advocate**: 반론 및 완성도 검증
7. **Editor-in-Chief**: 최종 편집 및 품질 보증

**워크플로우**:
```
/post "마이크로서비스 vs 모놀리스: 2026년 선택 가이드"
→ Crew Mode 선택
→ 7개 역할의 순차적 협업
→ 각 단계별 검토 및 개선
→ 최고 품질의 완성된 콘텐츠
```

**장점**:
- 최고 품질 출력
- 다각도 검증
- 포괄적인 커버리지
- 전문적인 완성도

**단점**:
- 긴 작성 시간 (20-40분)
- 더 많은 토큰 사용

### Adaptive Mode (섹션별 최적화)

**언제 사용?**
- 복합 주제 (이론 + 실습)
- 다양한 독자층
- 서로 다른 섹션 스타일이 필요한 경우

**워크플로우**:
```
/post "클린 아키텍처: 이론부터 실전까지"
→ Adaptive Mode 선택
→ 각 섹션에 최적 페르소나 자동 매칭:
   - 이론 설명 → Architect (formal + analytical)
   - 구현 예제 → Developer (conversational + practical)
   - 회고록 → Storyteller (narrative + experiential)
```

**섹션별 페르소나 매핑 예시**:
- 아키텍처 설명 → Architect
- 코드 구현 → Developer
- 교육 콘텐츠 → Mentor
- 산업 분석 → Analyst
- 제품 비교 → Reviewer
- 개인 경험 → Storyteller
- 뉴스 정리 → Curator
- 논쟁 의견 → Columnist

**장점**:
- 섹션별 최적 스타일
- 다양한 톤으로 흥미 유지
- 복합 주제에 완벽
- 여러 독자층 만족

## 8개 AI 저자 페르소나

### 1. Architect (아키텍트)

**DNA 조합**:
- Voice: Formal (한다체)
- Expertise: Architecture
- Perspective: Analytical
- Tone: Authoritative

**전문 분야**:
- 시스템 설계 및 아키텍처 패턴
- 분산 시스템 및 확장성
- 기술 선택 프레임워크
- 트레이드오프 분석

**작성 스타일**:
- 학술적이고 권위 있는 formal 한국어
- 복잡한 문장 구조와 종속절 활용
- 객관적 3인칭 관점
- 원칙 기반의 확실한 권장사항

**적합한 콘텐츠**:
- 아키텍처 패턴 심층 분석
- 시스템 설계 설명
- 성능 및 확장성 논의
- 기술 스택 선택 가이드

**예시 오프닝**:
> "마이크로서비스 아키텍처에서 분산 트랜잭션은 CAP 정리의 제약 속에서 해결해야 할 핵심 과제다. Saga 패턴은 이 문제에 대한 실용적 해법을 제시한다."

---

### 2. Developer (개발자)

**DNA 조합**:
- Voice: Conversational (해요체)
- Expertise: Implementation
- Perspective: Experiential
- Tone: Empathetic

**전문 분야**:
- 실전 코딩 및 구현
- 프레임워크 사용법
- 디버깅 및 문제 해결
- 도구 비교

**작성 스타일**:
- 친근한 대화체 한국어
- 1인칭 관점의 개인 경험
- 시행착오 서사
- 격려하고 지지하는 톤

**적합한 콘텐츠**:
- 실습 튜토리얼
- 구현 가이드
- 트러블슈팅 워크스루
- 프레임워크 활용법

**예시 오프닝**:
> "TypeScript를 처음 도입하려고 하면 막막하죠. 저도 그랬어요. 기존 JavaScript 프로젝트에 타입을 하나하나 추가하는 게 정말 지겨웠거든요."

---

### 3. Storyteller (스토리텔러)

**DNA 조합**:
- Voice: Narrative (서사체)
- Expertise: Implementation
- Perspective: Experiential
- Tone: Empathetic

**전문 분야**:
- 프로젝트 여정 및 회고
- 기술 의사결정 과정
- 실패에서 배운 교훈
- 팀 협업 스토리

**작성 스타일**:
- 과거형 서사 흐름
- 장면 묘사와 설명적 언어
- 스토리 아크 구조 (시작-중간-결말)
- 성찰적 인사이트

**적합한 콘텐츠**:
- 프로젝트 회고록
- 커리어 여정 서사
- 실패 사례 분석
- 기술 결정 기록

**예시 오프닝**:
> "2023년 3월, 우리 팀은 중대한 기술 부채와 마주했다. 3년간 축적된 레거시 코드가 새로운 기능 개발을 막고 있었다."

---

### 4. Mentor (멘토)

**DNA 조합**:
- Voice: Conversational (해요체)
- Expertise: Education
- Perspective: Analytical + Experiential
- Tone: Nurturing

**전문 분야**:
- 개념 설명 및 교육
- 학습 로드맵
- 초보자 가이드
- 단계별 튜토리얼

**작성 스타일**:
- 명확한 구조적 진행
- 사전 요구사항 설명
- 점진적 난이도 증가
- 긍정적 격려

**적합한 콘텐츠**:
- 입문 가이드
- 기본 개념 설명
- 학습 경로
- 모범 사례 가이드

**예시 오프닝**:
> "프로그래밍을 처음 배우는 분들을 위해 이 가이드를 준비했어요. 천천히 함께 따라오시면 됩니다. 어려운 부분이 있어도 괜찮아요. 모두 그 과정을 거쳐요."

---

### 5. Analyst (분석가)

**DNA 조합**:
- Voice: Formal (한다체)
- Expertise: Industry
- Perspective: Analytical
- Tone: Authoritative

**전문 분야**:
- 시장 트렌드 분석
- 기술 채택 보고서
- 프레임워크 비교 연구
- ROI 및 비즈니스 영향 분석

**작성 스타일**:
- 데이터 및 통계 중심
- 비교 분석 매트릭스
- 정량적 증거 강조
- 전략적 권장사항

**적합한 콘텐츠**:
- 산업 트렌드 분석
- 기술 채택 리포트
- 프레임워크 비교
- 시장 환경 개요

**예시 오프닝**:
> "2024년 프론트엔드 프레임워크 시장은 React의 지배력이 지속되는 가운데, Svelte와 Solid.js의 성장세가 두드러진다. Stack Overflow Survey에 따르면..."

---

### 6. Reviewer (리뷰어)

**DNA 조합**:
- Voice: Conversational (해요체)
- Expertise: Implementation
- Perspective: Analytical + Experiential
- Tone: Empathetic + Authoritative

**전문 분야**:
- 도구 및 프레임워크 리뷰
- 제품 비교
- 사용 사례 권장
- 장단점 분석

**작성 스타일**:
- 균형 잡힌 장단점 제시
- 개인 사용 경험 + 데이터 지원
- 명확한 평가 기준
- 맥락 기반 권장사항

**적합한 콘텐츠**:
- 도구 리뷰
- 비교 가이드
- 마이그레이션 조언
- 사용 사례 분석

**예시 오프닝**:
> "Prisma ORM을 6개월간 프로덕션에서 사용해봤어요. 장점도 분명하지만 단점도 있더라고요. 실제 사용 경험을 바탕으로 정리해볼게요."

---

### 7. Curator (큐레이터)

**DNA 조합**:
- Voice: Formal (한다체)
- Expertise: Industry
- Perspective: Analytical
- Tone: Authoritative

**전문 분야**:
- 기술 뉴스 및 업데이트
- 릴리스 노트
- 컨퍼런스 하이라이트
- 주간 라운드업

**작성 스타일**:
- 간결하고 핵심적
- 역피라미드 구조 (중요한 것 먼저)
- 의견 없는 사실 보도
- 스캔 가능한 포맷

**적합한 콘텐츠**:
- 릴리스 노트
- 주간 기술 뉴스
- 속보 요약
- 업데이트 정리

**예시 오프닝**:
> "Next.js 15가 2024년 10월 21일 정식 출시됐다. 주요 변경사항은 React 19 지원, Turbopack 안정화, 향상된 캐싱 전략이다."

---

### 8. Columnist (칼럼니스트)

**DNA 조합**:
- Voice: Mixed (formal + conversational)
- Expertise: Industry
- Perspective: Critical
- Tone: Provocative

**전문 분야**:
- 산업 트렌드에 대한 오피니언
- 논쟁적 기술 토론
- 인기 관행 비판
- 대안적 관점

**작성 스타일**:
- 강력한 오프닝 진술
- 수사적 질문
- 가정에 대한 도전
- 도발적인 결론

**적합한 콘텐츠**:
- 오피니언 피스
- 논쟁적 토론
- 관행 비판
- 행동 촉구 논평

**예시 오프닝**:
> "모든 프로젝트에 TypeScript가 필요한가? 이 질문에 무조건 '예'라고 답하는 것은 사고의 정지다. 우리는 언제부터 맹목적으로 트렌드를 따르게 됐나."

---

## 기술 문서

### 플러그인 구조

```
astory-blog-writers/
├── .claude-plugin/
│   └── plugin.json              # 플러그인 매니페스트
├── commands/                     # 명령어
│   └── post.md                   # /post 명령 (작성 워크플로우 오케스트레이션)
├── agents/                       # 에이전트
│   ├── author-router.md          # 페르소나 선택 및 라우팅
│   ├── researcher.md             # 리서치 에이전트
│   ├── writer-architect.md       # Architect 페르소나 구현
│   ├── writer-developer.md       # Developer 페르소나 구현
│   ├── writer-storyteller.md     # Storyteller 페르소나 구현
│   ├── writer-mentor.md          # Mentor 페르소나 구현
│   ├── writer-analyst.md         # Analyst 페르소나 구현
│   ├── writer-reviewer.md        # Reviewer 페르소나 구현
│   ├── writer-curator.md         # Curator 페르소나 구현
│   └── writer-columnist.md       # Columnist 페르소나 구현
├── skills/                       # 스킬
│   ├── traits/                   # 16개 특성 DNA 라이브러리
│   │   ├── SKILL.md
│   │   └── modules/              # 16개 특성 모듈
│   │       ├── voice-formal.md
│   │       ├── voice-conversational.md
│   │       ├── voice-narrative.md
│   │       ├── voice-technical.md
│   │       ├── expertise-architecture.md
│   │       ├── expertise-implementation.md
│   │       ├── expertise-industry.md
│   │       ├── expertise-education.md
│   │       ├── perspective-analytical.md
│   │       ├── perspective-experiential.md
│   │       ├── perspective-critical.md
│   │       ├── perspective-visionary.md
│   │       ├── tone-authoritative.md
│   │       ├── tone-empathetic.md
│   │       ├── tone-provocative.md
│   │       └── tone-nurturing.md
│   ├── personas/                 # 8개 페르소나 정의
│   │   ├── SKILL.md
│   │   └── modules/              # 페르소나별 구현 가이드
│   │       ├── architect.md
│   │       ├── developer.md
│   │       ├── storyteller.md
│   │       ├── mentor.md
│   │       ├── analyst.md
│   │       ├── reviewer.md
│   │       ├── curator.md
│   │       └── columnist.md
│   ├── protocols/                # 3가지 작성 모드
│   │   ├── SKILL.md
│   │   └── modules/
│   │       ├── solo-mode.md
│   │       ├── crew-mode.md
│   │       └── adaptive-mode.md
│   ├── crew-roles/               # Crew Mode 7개 역할
│   │   ├── SKILL.md
│   │   └── modules/
│   │       ├── creative-director.md
│   │       ├── research-analyst.md
│   │       ├── lead-writer.md
│   │       ├── technical-reviewer.md
│   │       ├── reader-advocate.md
│   │       ├── devil-advocate.md
│   │       └── editor-in-chief.md
│   ├── research/                 # 리서치 기능
│   │   ├── SKILL.md
│   │   └── modules/
│   │       ├── web-search-protocol.md
│   │       ├── media-collection.md
│   │       └── citation-system.md
│   ├── writing-standards/        # 작성 품질 표준
│   │   ├── SKILL.md
│   │   └── modules/
│   │       ├── korean-style.md
│   │       └── quality-guidelines.md
│   └── anti-ai-validator/        # Anti-AI 검증 (독립 스킬)
│       ├── SKILL.md
│       └── modules/
│           ├── forbidden-patterns.md
│           ├── warning-patterns.md
│           └── structural-checks.md
├── hooks/
│   └── hooks.json                # Post-tool 자동 검증 훅
├── README.md                     # 이 파일
├── LICENSE                       # MIT 라이선스
└── CHANGELOG.md                  # 버전 이력
```

### 스킬 아키텍처

**Traits (특성 DNA 라이브러리)**:
- 16개 원자적 특성 정의
- 4개 카테고리: Voice, Expertise, Perspective, Tone
- 조합을 통한 256+ 가능한 페르소나 생성
- 재사용 가능한 특성 모듈

**Personas (페르소나 정의)**:
- 8개 사전 설정 페르소나
- 각 페르소나는 4개 특성의 고유 조합
- 페르소나별 구현 가이드
- 콘텐츠 유형별 선택 기준

**Protocols (작성 모드)**:
- Solo Mode: 단일 페르소나 빠른 작성
- Crew Mode: 7개 역할 협업
- Adaptive Mode: 섹션별 페르소나 전환

**Crew Roles (협업 역할)**:
- Creative Director: 아이디어 발굴
- Research Analyst: 심층 리서치
- Lead Writer: 콘텐츠 초안
- Technical Reviewer: 기술 검증
- Reader Advocate: 가독성 검토
- Devil's Advocate: 반론 검증
- Editor-in-Chief: 최종 편집

**Research (리서치 시스템)**:
- 웹 검색 프로토콜
- 미디어 수집 (이미지, YouTube)
- 소스 검증 및 인용 시스템

**Writing Standards (작성 표준)**:
- 한국어 스타일 가이드 (한다체, 해요체, 서사체)
- 품질 관리 가이드라인
- 일관성 검증 규칙

**Anti-AI Validator (독립 검증 스킬)**:
- 금지 표현 패턴 탐지
- 경고 표현 패턴 탐지
- 구조적 AI 패턴 검증
- 자동 수정 제안

### 에이전트 구성

**Author Router**:
- 콘텐츠 유형 분석
- 최적 페르소나 선택
- 모드별 워크플로우 라우팅

**Researcher**:
- 웹 검색 실행
- 미디어 수집
- 소스 검증
- 인용 관리

**Writer Agents (8개)**:
- 각 페르소나별 전용 에이전트
- 특성 조합 구현
- 스타일 가이드 적용
- 페르소나 일관성 유지

### 훅 시스템

**Post-Tool Validation Hook**:
- 콘텐츠 작성 후 자동 실행
- Anti-AI 패턴 검증
- 품질 표준 검사
- 수정 제안 제공

### 커스터마이징 가이드

#### 커스텀 페르소나 생성

**Step 1: 특성 선택**
```markdown
Voice: Conversational (해요체)
Expertise: Industry (산업 분석)
Perspective: Critical (비판적)
Tone: Provocative (도발적)
```

**Step 2: 페르소나 정의 파일 생성**
```bash
touch skills/personas/modules/my-custom-persona.md
```

**Step 3: 특성 조합 문서화**
```markdown
# My Custom Persona

## DNA Composition
- Voice: Conversational
- Expertise: Industry
- Perspective: Critical
- Tone: Provocative

## Core Identity
"비판적 시각으로 산업 트렌드를 분석하며 도발적 질문으로 독자의 사고를 자극하는 대화체 작가"

## Content Strengths
- 산업 관행 비판
- 트렌드에 대한 대안적 관점
- 논쟁적 기술 토론
```

**Step 4: Writer Agent 생성**
```bash
touch agents/writer-mycustom.md
```

#### 새로운 특성 추가

**Step 1: 특성 모듈 생성**
```bash
touch skills/traits/modules/tone-humorous.md
```

**Step 2: 특성 정의**
```markdown
# Tone: Humorous

## Characteristic
유머와 위트를 활용한 경쾌한 톤

## Language Markers
- 유머러스한 비유
- 적절한 농담
- 가벼운 자기 비하
- 재치 있는 표현

## Use Cases
- 가벼운 기술 주제
- 초보자 친화적 콘텐츠
- 재미있는 경험 공유
```

**Step 3: traits/SKILL.md 업데이트**

#### Crew Mode 역할 커스터마이징

각 역할의 구현을 수정하여 검토 프로세스 조정:

```bash
# Devil's Advocate 역할 강화 예시
vim skills/crew-roles/modules/devil-advocate.md
```

### 구성 옵션

플러그인은 표준 Claude Code 설정을 사용합니다:

```json
{
  "language": {
    "conversation_language": "ko",
    "documentation": "en"
  }
}
```

## 기여하기

aStory Blog Writers 개선에 기여를 환영합니다!

### 기여 방법

1. **저장소 포크**:
   ```bash
   git clone https://github.com/modu-ai/claude-plugins.git
   cd claude-plugins/plugins/astory-blog-writers
   ```

2. **기능 브랜치 생성**:
   ```bash
   git checkout -b feature/my-enhancement
   ```

3. **변경사항 작성**:
   - 새로운 페르소나 추가
   - 새로운 특성 추가
   - 작성 모드 개선
   - Crew 역할 향상
   - Anti-AI 패턴 추가
   - 버그 수정

4. **로컬 테스트**:
   ```bash
   claude plugin install --local .
   /post "테스트 주제"
   ```

5. **풀 리퀘스트 제출**:
   - 변경사항에 대한 명확한 설명
   - 테스트 결과 및 예제
   - 업데이트된 문서

### 개발 환경 설정

```bash
# 저장소 클론
git clone https://github.com/modu-ai/claude-plugins.git
cd claude-plugins/plugins/astory-blog-writers

# 개발 모드로 설치
claude plugin install --local .

# 디버그 로깅 활성화
claude --debug
```

### 테스트 가이드라인

- 각 페르소나를 적절한 콘텐츠 유형으로 테스트
- 모든 3가지 모드 (Solo, Crew, Adaptive) 검증
- Anti-AI 검증 작동 확인
- 한국어 스타일 가이드 준수 확인
- Crew Mode 역할별 검토 프로세스 테스트

### 기여 영역

**새로운 특성 추가**:
- Voice 패턴 확장 (예: Poetic, Academic)
- Expertise 영역 추가 (예: DevOps, Security)
- Perspective 스타일 추가 (예: Pragmatic, Theoretical)
- Tone 특성 추가 (예: Humorous, Inspirational)

**페르소나 확장**:
- 기존 특성으로 새로운 조합 제안
- 특정 도메인 전문 페르소나
- 특수 콘텐츠 유형 페르소나

**작성 모드 개선**:
- Solo Mode 최적화
- Crew Mode 역할 추가
- Adaptive Mode 섹션 매핑 개선

**품질 향상**:
- Anti-AI 패턴 추가
- 한국어 스타일 가이드 확장
- 품질 검증 규칙 강화

## 로드맵

### 버전 2.1 (계획 중)

**특성 확장**:
- Voice: Poetic, Academic 추가
- Expertise: DevOps, Security 추가
- Perspective: Pragmatic 추가
- Tone: Humorous 추가

**모드 개선**:
- Semi-Crew Mode: 3-4개 핵심 역할만 사용
- Hybrid Mode: Solo + Adaptive 조합

**다국어 지원**:
- 영어 작성 모드
- 일본어 작성 모드

### 버전 2.2 (미래)

**고급 기능**:
- SEO 최적화 자동화
- 소셜 미디어 변형 생성
- 이미지 생성 통합
- 템플릿 라이브러리

**협업 기능**:
- 멀티 작가 워크플로우
- 버전 관리 통합
- 피드백 루프

## 라이선스

MIT License

Copyright (c) 2026 GOOS

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.

## 감사의 말

- [Claude Code](https://claude.ai/claude-code) + [MoAI-ADK](https://github.com/modu-ai/moai-adk)로 구축됨
- Hybrid Author System v2.0 아키텍처 설계
- 한국어 기술 블로깅 커뮤니티의 피드백

## 지원

- **Issues**: [GitHub Issues](https://github.com/modu-ai/claude-plugins/issues)
- **Discussions**: [GitHub Discussions](https://github.com/modu-ai/claude-plugins/discussions)
- **Email**: email@goos.kim
- **Developer Blog**: [https://goos.kim](https://goos.kim)

---

**Hybrid Author System v2.0으로 진정성 있는 블로그 콘텐츠를 만드세요**
Made with ❤️ by **GOOS** | [모두의AI](https://github.com/modu-ai)
