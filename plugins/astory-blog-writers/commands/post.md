---
name: astory:post
description: "Create blog posts with Hybrid Author System - Solo (단일 페르소나), Crew (협업), Adaptive (섹션별 전환) 모드 지원"
allowed-tools:
  - Task
  - AskUserQuestion
  - TodoWrite
model: inherit
skills:
  - astory
  - writing-standards
  - research
---

## 사전 실행 컨텍스트

!git status --porcelain
!git branch --show-current
!git log --oneline -3

## 필수 파일

@.moai/config/config.yaml
@.moai/docs/astory-author-system-design.md
@.claude/skills/astory-writing-standards/SKILL.md

---

# aStory 포스트 생성: Hybrid AI Author System

**사용자 상호작용 아키텍처**: AskUserQuestion은 반드시 COMMAND 레벨에서만 사용해야 한다. Task()로 호출된 서브에이전트는 상태가 없으며 사용자와 직접 상호작용할 수 없다. 페이즈 실행을 위임하기 전에 모든 승인을 먼저 수집해야 한다.

**실행 모델**: 커맨드는 `Task()` 도구만을 통해 조율한다. 직접적인 도구 사용은 금지된다.

**위임 패턴**: Hybrid Author System을 통한 5단계 순차 워크플로우:
- Phase 0: 리서치 (선택 - astory-researcher를 통한 심층 조사)
- Phase 1: 작성 모드 선택 (Solo/Crew/Adaptive 모드 선택)
- Phase 2: 콘텐츠 세부정보 (제목, 주제, 독자층 수집)
- Phase 3: 작성 (모드별 작가 에이전트 호출)
- Phase 4: 검토 및 게시 (피드백 루프와 파일 저장)

---

## Hybrid Author System 개요

### 3가지 작성 모드

**Solo Mode (단일 페르소나)**:
- 하나의 작가 페르소나가 전체 콘텐츠 작성
- 일관된 음성과 스타일 유지
- 빠른 작성 속도
- Best for: 블로그 포스트, 튜토리얼, 에세이

**Crew Mode (다중 페르소나 협업)**:
- 여러 작가 페르소나가 각자 섹션 담당
- 다양한 관점과 전문성 통합
- 풍부한 콘텐츠 구성
- Best for: 종합 가이드, 비교 분석, 심층 리포트

**Adaptive Mode (섹션별 페르소나 자동 전환)**:
- AI가 각 섹션 특성에 맞는 페르소나 자동 선택
- 컨텍스트 기반 최적화
- 균형 잡힌 스타일
- Best for: 복합 주제, 다양한 독자층, 자동 최적화

---

## 커맨드 목적

각각 고유한 음성, 스타일, 전문성을 가진 AI 작가 페르소나를 통해 프로덕션 수준의 블로그 포스트를 생성한다.

`/astory:post` 커맨드는 단일 범용 작가 대신 전문화된 작가 에이전트에 위임하여 페르소나 기반 블로그 포스트 생성을 조율한다.

**주요 기능**:
- 3가지 작성 모드: Solo, Crew, Adaptive
- 고유한 글쓰기 스타일을 가진 8개의 독립적인 작가 페르소나
- 웹 검색과 미디어 수집을 포함한 선택적 심층 리서치 페이즈
- 자연스러운 한국어 작문을 위한 Anti-AI 패턴 시스템
- 풍부한 콘텐츠 생성을 위한 리서치 브리프 통합

---

## 8개 작가 페르소나

**작가 에이전트** (Phase 3 - 페르소나당 하나):

- **astory-writer-architect**: 기술 아키텍트 - 격식체, 분석적, 권위적
- **astory-writer-developer**: 실무 개발자 - 실용적, 대화체, 경험 기반
- **astory-writer-storyteller**: 스토리텔러 - 공감적, 서사적, 성찰적
- **astory-writer-mentor**: 교육 멘토 - 체계적, 단계별, 입문자 친화적
- **astory-writer-analyst**: 산업 분석가 - 객관적, 데이터 기반, 트렌드 중심
- **astory-writer-reviewer**: 제품 리뷰어 - 균형 잡힌, 비교 분석, 사용 경험 기반
- **astory-writer-curator**: 뉴스 큐레이터 - 간결한, 사실적, 시의성 있는
- **astory-writer-columnist**: 칼럼니스트 - 비판적, 도발적, 통찰력 있는

**핵심 스킬** (모든 작가가 로드해야 함):

- **astory-writing-standards**: Anti-AI 패턴, 한국어 스타일 가이드, 인용 규칙
- **astory-research**: 리서치 프로토콜 및 미디어 수집 패턴

**페르소나 스킬** (각 작가가 로드):

- **astory-persona-architect** ~ **astory-persona-columnist**: 음성, 스타일, 구조 정의

---

## 에이전트 호출 패턴 (CLAUDE.md 준수)

이 커맨드는 CLAUDE.md에 정의된 에이전트 실행 패턴을 사용한다.

### 순차적 페이즈 기반 체이닝

커맨드는 5개 페이즈를 통한 순차 체이닝을 구현한다:

페이즈 플로우:
- Phase 0: 리서치 (astory-researcher 서브에이전트 - 선택)
- Phase 1: 작성 모드 선택 (Solo/Crew/Adaptive 선택)
- Phase 2: 콘텐츠 세부정보 (제목, 주제, 독자층 수집)
- Phase 3: 작성 (모드별 작가 서브에이전트)
- Phase 4: 검토 및 게시 (피드백 루프와 파일 저장)

각 페이즈는 이전 페이즈의 출력을 컨텍스트로 받는다.

WHY: 순차 실행은 리서치가 작성에 반영되고 페르소나 일관성을 보장한다
- Phase 3은 Phase 0의 리서치 브리프가 필요하다 (수행된 경우)
- Phase 3은 Phase 1의 모드 선택이 필요하다
- Phase 4는 Phase 3의 초안 콘텐츠가 필요하다

IMPACT: 페이즈 건너뛰기나 병렬 실행은 일관성 없는 콘텐츠를 생성한다

---

## 실행 철학: "리서치 - 선택 - 작성 - 검토 - 게시"

`/astory:post` 커맨드는 5개의 순차 페이즈를 통한 페르소나 기반 에이전트 위임으로 블로그 포스트를 생성한다.

### 출력 형식 규칙

사용자 대면 리포트: 모든 사용자 커뮤니케이션에 마크다운 형식을 사용한다.

사용자 리포트 예시 (Phase 4 완료):

```
초안 작성 완료

모드: Solo Mode
작가: 기술 아키텍트 (astory-writer-architect)
제목: Saga 패턴 딥다이브
주제: 분산 트랜잭션 관리
글자 수: 2,800자

사용된 리서치 소스: 5개
수집된 이미지: 3개
참조된 비디오: 1개

다음 단계:
1. 초안 검토 및 승인
2. 수정 요청
3. 다른 작가 페르소나로 시도
```

내부 에이전트 데이터: XML 태그는 에이전트 간 데이터 전송에만 사용된다. 사용자에게 XML 태그를 표시하지 않는다.

### 도구 사용 규율

이 커맨드는 다음 세 가지 도구 카테고리만 사용해야 한다:

- **Task()**: 페르소나별 작가 에이전트에 위임
  - WHY: 아키텍처 명확성과 관심사 분리를 유지한다
  - IMPACT: 각 페르소나가 집중적이고 재사용 가능하도록 보장한다

- **AskUserQuestion()**: COMMAND 레벨에서만 사용자 선호도 수집
  - WHY: Task()를 통한 서브에이전트는 상태가 없으며 사용자와 상호작용할 수 없다
  - IMPACT: 에이전트가 AskUserQuestion을 사용할 것으로 기대하면 워크플로우 실패를 초래한다
  - CORRECT: 커맨드가 모든 선호도를 수집하고 에이전트에 파라미터로 전달한다

- **TodoWrite()**: 페이즈 전반에 걸친 작업 진행 상황 추적
  - WHY: 콘텐츠 생성 워크플로우의 가시성을 유지한다
  - IMPACT: 다중 페이즈 프로세스의 진행 상황 모니터링을 가능하게 한다

- **에이전트가 모든 직접 도구 사용을 처리한다** (Read, Write, Edit, Bash, Grep, Glob)
  - WHY: 커맨드는 가볍게 유지하고 에이전트가 도메인 전문성을 제공한다
  - IMPACT: 커맨드 복잡성을 줄이면서 신뢰성을 향상시킨다

---

## PHASE 0: 리서치 (선택)

목표: 사용자가 요청하면 astory-researcher 에이전트를 통해 심층 리서치를 수행한다

### Step 0.1: 리서치 필요 여부 확인

AskUserQuestion으로 리서치 필요 여부를 확인한다:

AskUserQuestion 파라미터:
- Question: "참고할 URL이나 주제에 대한 심층 조사가 필요하신가요?"
- Header: "리서치"
- MultiSelect: false
- Options:
  - Label: "심층 조사 필요"
  - Description: "웹검색 + URL 자료 수집 + 활용 계획"
  - Label: "직접 작성"
  - Description: "리서치 없이 바로 작성 시작"

### Step 0.2: 리서치 파라미터 수집 (리서치 선택 시)

사용자가 "심층 조사 필요"를 선택하면:

AskUserQuestion 파라미터:
- Question: "조사할 주제와 참고 URL을 입력해주세요"
- Header: "리서치 정보"
- MultiSelect: false
- Options:
  - Label: "주제만 입력"
  - Description: "웹검색으로 자료 수집"
  - Label: "URL 포함"
  - Description: "특정 URL 분석 + 웹검색"
  - Label: "URL만 분석"
  - Description: "제공된 URL만 분석"

이후 주제와 URL을 자유 텍스트 입력으로 수집한다.

### Step 0.3: 리서치 에이전트 호출

리서치를 선택한 경우, astory-researcher에 위임한다:

Task 위임 (subagent_type: "astory-researcher") 지침:

다음 주제에 대한 심층 리서치를 수행한다.

주제: (Step 0.2에서 수집)
참고 URL: (Step 0.2에서 수집, 제공된 경우)

전체 리서치 워크플로우를 실행한다:

1. 웹 검색: 주제에 대한 다중 쿼리 검색 수행
2. URL 분석: 제공된 URL의 콘텐츠와 미디어 분석
3. 미디어 수집: 관련 이미지와 YouTube 링크 추출
4. 소스 검증: 신뢰성과 라이선스 정보 검증
5. 활용 계획: 수집된 리소스를 콘텐츠 섹션에 매핑

다음을 포함한 구조화된 형식으로 리서치 브리프를 반환한다:
- 관련성 점수가 포함된 웹 소스
- 대체 텍스트, 컨텍스트, 라이선스 정보가 포함된 이미지
- 타임스탬프와 활용 계획이 포함된 비디오
- 콘텐츠 통합을 위한 섹션 매핑
- 포함 준비된 인용

Phase 3에서 사용할 research_brief를 저장한다.

---

## PHASE 1: 작성 모드 선택

목표: 사용자가 Hybrid Author System의 3가지 모드 중 하나를 선택한다

### Step 1.1: 작성 모드 선택

AskUserQuestion 파라미터:
- Question: "어떤 방식으로 작성할까요?"
- Header: "작성 모드"
- MultiSelect: false
- Options:
  - Label: "Solo Mode (단일 페르소나)"
  - Description: "한 명의 작가가 전체 작성 - 빠르고 일관된 스타일"
  - Label: "Crew Mode (협업)"
  - Description: "여러 작가가 협업 - 다양한 관점과 전문성"
  - Label: "Adaptive Mode (자동)"
  - Description: "AI가 섹션별 최적 페르소나 자동 선택"

### Step 1.2: 모드별 작가 선택

**Solo Mode 선택 시**:

첫 번째 작가 그룹 제시 (4개 옵션):

AskUserQuestion 파라미터:
- Question: "어떤 작가 스타일로 작성할까요?"
- Header: "작가 선택"
- MultiSelect: false
- Options:
  - Label: "기술 아키텍트"
  - Description: "Deep Dive, 아키텍처 가이드 - 권위있고 분석적인 한다체"
  - Label: "실무 개발자"
  - Description: "튜토리얼, 구현 가이드 - 실용적이고 경험 기반 구어체"
  - Label: "스토리텔러"
  - Description: "에세이, 회고록 - 공감하며 이야기하는 서사체"
  - Label: "더 많은 작가 보기"
  - Description: "교육 멘토, 산업 분석가, 리뷰어, 큐레이터, 칼럼니스트"

두 번째 작가 그룹 제시 ("더 많은 작가 보기" 선택 시):

AskUserQuestion 파라미터:
- Question: "어떤 작가 스타일로 작성할까요?"
- Header: "작가 선택 (추가)"
- MultiSelect: false
- Options:
  - Label: "교육 멘토"
  - Description: "입문 가이드, 로드맵 - 단계별 친절한 해요체"
  - Label: "산업 분석가"
  - Description: "트렌드 리포트 - 객관적이고 데이터 기반 한다체"
  - Label: "제품 리뷰어"
  - Description: "비교 분석 - 균형잡힌 사용 경험 해요체"
  - Label: "뉴스 큐레이터"
  - Description: "릴리스 노트 - 간결하고 사실적인 한다체"

추가 옵션이 필요한 경우:

AskUserQuestion 파라미터:
- Question: "마지막 작가 옵션입니다"
- Header: "작가 선택 (마지막)"
- MultiSelect: false
- Options:
  - Label: "칼럼니스트"
  - Description: "의견 칼럼 - 비판적이고 통찰력 있는 혼합체"
  - Label: "처음으로 돌아가기"
  - Description: "첫 번째 작가 그룹으로 돌아가기"

**Crew Mode 선택 시**:

AskUserQuestion 파라미터:
- Question: "몇 명의 작가가 협업할까요?"
- Header: "협업 작가 수"
- MultiSelect: false
- Options:
  - Label: "2명"
  - Description: "2개 섹션을 각각 다른 스타일로"
  - Label: "3명"
  - Description: "3개 섹션을 각각 다른 스타일로"
  - Label: "4명"
  - Description: "4개 섹션을 각각 다른 스타일로"

이후 선택된 작가 수만큼 작가 선택을 반복한다 (Solo Mode와 동일한 선택 UI 사용).

각 작가 선택 시 담당 섹션 설명을 입력받는다:

AskUserQuestion 파라미터:
- Question: "[작가 이름]이 작성할 섹션을 설명해주세요"
- Header: "섹션 설명"
- MultiSelect: false
- Options:
  - Label: "섹션 설명 입력"
  - Description: "해당 작가가 담당할 내용 설명"

**Adaptive Mode 선택 시**:

섹션 수와 주제만 수집:

AskUserQuestion 파라미터:
- Question: "몇 개의 섹션으로 구성할까요?"
- Header: "섹션 구성"
- MultiSelect: false
- Options:
  - Label: "3개 섹션"
  - Description: "도입 - 본론 - 결론"
  - Label: "4개 섹션"
  - Description: "도입 - 본론1 - 본론2 - 결론"
  - Label: "5개 섹션"
  - Description: "도입 - 본론1 - 본론2 - 본론3 - 결론"

### Step 1.3: 선택을 에이전트에 매핑

작가-에이전트 매핑:
- 기술 아키텍트: astory-writer-architect
- 실무 개발자: astory-writer-developer
- 스토리텔러: astory-writer-storyteller
- 교육 멘토: astory-writer-mentor
- 산업 분석가: astory-writer-analyst
- 제품 리뷰어: astory-writer-reviewer
- 뉴스 큐레이터: astory-writer-curator
- 칼럼니스트: astory-writer-columnist

Phase 3에서 사용할 mode_config를 저장한다:
- mode: "solo", "crew", or "adaptive"
- writers: List of selected writer agents
- sections: Section descriptions (Crew/Adaptive mode only)

---

## PHASE 2: 콘텐츠 세부정보

목표: 제목, 주제, 추가 콘텐츠 파라미터 수집

### Step 2.1: 제목 수집

AskUserQuestion 파라미터:
- Question: "포스트 제목을 입력해주세요"
- Header: "제목"
- MultiSelect: false
- Options:
  - Label: "제목 직접 입력"
  - Description: "원하는 제목을 자유롭게 입력"
  - Label: "AI 제목 추천"
  - Description: "주제 입력 후 AI가 제목 추천"

"제목 직접 입력" 선택 시, 자유 텍스트로 제목을 수집한다.
"AI 제목 추천" 선택 시, 주제 수집을 먼저 진행한다.

### Step 2.2: 주제 및 설명 수집

AskUserQuestion 파라미터:
- Question: "어떤 주제로 글을 작성할까요? 구체적으로 설명해주세요"
- Header: "주제"
- MultiSelect: false
- Options:
  - Label: "주제 직접 입력"
  - Description: "작성하고 싶은 내용을 자세히 설명"
  - Label: "React/Next.js"
  - Description: "React 또는 Next.js 관련 주제"
  - Label: "TypeScript"
  - Description: "TypeScript 관련 주제"
  - Label: "AI/ML"
  - Description: "인공지능, 머신러닝 관련 주제"

자유 텍스트로 상세 주제 설명을 수집한다.

### Step 2.3: 대상 독자 수집 (선택)

AskUserQuestion 파라미터:
- Question: "주요 독자층을 선택해주세요 (선택사항)"
- Header: "대상 독자"
- MultiSelect: false
- Options:
  - Label: "입문자"
  - Description: "해당 분야를 처음 접하는 독자"
  - Label: "중급자"
  - Description: "기본 지식이 있는 실무 개발자"
  - Label: "고급자"
  - Description: "심화 내용을 원하는 경험 많은 개발자"
  - Label: "전체"
  - Description: "모든 수준의 독자 대상"

### Step 2.4: 핵심 포인트 수집 (선택)

AskUserQuestion 파라미터:
- Question: "반드시 다뤄야 할 핵심 포인트가 있나요? (선택사항)"
- Header: "핵심 포인트"
- MultiSelect: false
- Options:
  - Label: "핵심 포인트 입력"
  - Description: "꼭 포함해야 할 내용 직접 입력"
  - Label: "건너뛰기"
  - Description: "AI가 자동으로 구성"

"핵심 포인트 입력" 선택 시, 자유 텍스트로 핵심 포인트를 수집한다.

Phase 3에서 사용할 content_details를 저장한다:
- title: 수집한 제목
- topic: 수집한 주제 설명
- target_audience: 선택한 독자 수준
- key_points: 수집한 핵심 포인트 (선택)

---

## PHASE 3: 작가 에이전트 호출

목표: 선택한 모드에 따라 작가 에이전트에 작성 위임

### Step 3.1: 진행 상황 추적을 위한 TodoWrite 초기화

다음 항목으로 TodoWrite를 초기화한다:
- Content: "리서치 브리프 로드 (가능한 경우)", Status: in_progress, ActiveForm: "리서치 컨텍스트 로딩 중"
- Content: "모드에 따른 작가 에이전트 호출", Status: pending, ActiveForm: "작가 에이전트 호출 중"
- Content: "초안 콘텐츠 생성", Status: pending, ActiveForm: "초안 콘텐츠 생성 중"
- Content: "Anti-AI 패턴 검증 적용", Status: pending, ActiveForm: "작성 패턴 검증 중"

### Step 3.2: Solo 모드 실행

모드가 "solo"인 경우:

Task 위임 (subagent_type: Phase 1에서 선택한 작가 에이전트) 지침:

고유한 페르소나 음성을 사용하여 aStory 플랫폼용 블로그 포스트를 작성한다.

작가 페르소나 컨텍스트:
- 페르소나: (Phase 1에서 선택한 페르소나)
- 에이전트: (Phase 1에서 선택한 에이전트)
- 모드: Solo (전체 콘텐츠 단일 작성)

콘텐츠 세부정보:
- 제목: (Phase 2에서 수집한 제목)
- 주제: (Phase 2에서 수집한 주제)
- 대상 독자: (Phase 2에서 수집한 독자층)
- 핵심 포인트: (Phase 2에서 수집, 제공된 경우)

리서치 브리프: (Phase 0에서 수집, 가능한 경우)

작성 요구사항:

1. 음성 및 스타일 가이드를 위해 페르소나 스킬 (astory-persona-{persona-type}) 로드
2. Anti-AI 패턴 검증을 위해 astory-writing-standards 스킬 로드
3. 전체에 걸쳐 고유한 톤, 스타일, 관점을 일관되게 적용
4. 제공된 경우 리서치 브리프 소스와 미디어 사용
5. 적절한 frontmatter가 포함된 완전한 MDX 콘텐츠 생성

Anti-AI 패턴 검증 (필수):
- "~를 넘어" 패턴 금지 (가장 탐지 가능한 AI 패턴)
- 금지어 사용 금지: 패러다임, 혁신, 획기적, 놀라운
- "매우/아주/정말"을 구체적인 수치로 대체
- 다양한 문장 구조 확보
- 다양한 접속사 사용

출력 요구사항:
- frontmatter가 포함된 완전한 MDX 파일 콘텐츠
- 페르소나에 적합한 섹션 구조
- 코드 예제 (기술 콘텐츠인 경우)
- Mermaid 다이어그램 (아키텍처 콘텐츠인 경우)
- 사용한 리서치 소스에 대한 인용

사용자 검토를 위해 초안 콘텐츠를 반환한다.

### Step 3.3: Crew 모드 실행

모드가 "crew"인 경우:

협업 팀의 각 작가에 대해:

Task 위임 (subagent_type: 작가 에이전트) 지침:

고유한 페르소나 음성을 사용하여 협업 블로그 포스트의 섹션을 작성한다.

협업 컨텍스트:
- 모드: Crew Mode (협업 작성)
- 역할: {total_writers}명 중 {index}번째 작가
- 담당 섹션: {section_description}

작가 페르소나 컨텍스트:
- 페르소나: (작가 페르소나)
- 에이전트: (작가 에이전트)

콘텐츠 세부정보:
- 전체 제목: (Phase 2에서 수집한 제목)
- 전체 주제: (Phase 2에서 수집한 주제)
- 담당 섹션 초점: (Phase 1에서 수집한 섹션 설명)
- 대상 독자: (Phase 2에서 수집한 독자층)

리서치 브리프: (Phase 0에서 수집, 가능한 경우)

협업 가이드라인:
1. 할당된 섹션에만 집중
2. 고유한 음성과 스타일 유지
3. 다음 작가를 위한 매끄러운 전환 확보
4. 담당 섹션과 관련된 리서치 소스 참조
5. 전체 콘텐츠 구조와 조율

작성 요구사항:
1. 음성 가이드라인을 위해 페르소나 스킬 로드
2. Anti-AI 패턴을 위해 astory-writing-standards 스킬 로드
3. 섹션 내에서 페르소나를 일관되게 적용
4. 제공된 경우 담당 섹션에 리서치 브리프 사용

출력 요구사항:
- 담당 섹션 콘텐츠만 (H2 제목 + 문단)
- 섹션과 관련된 경우 코드 예제
- 섹션에서 사용한 소스에 대한 인용

모든 섹션을 순차적으로 결합하고 frontmatter가 포함된 최종 MDX를 생성한다.

### Step 3.4: Adaptive 모드 실행

모드가 "adaptive"인 경우:

섹션별 적합한 작가 에이전트를 순차적으로 호출하여 콘텐츠를 생성한다.

Adaptive 모드 실행 프로세스:

1. 섹션 분석 및 페르소나 매핑:
   - 기술 설명 섹션 → astory-writer-architect
   - 튜토리얼/실습 섹션 → astory-writer-developer 또는 astory-writer-mentor
   - 스토리/경험 섹션 → astory-writer-storyteller
   - 비교/리뷰 섹션 → astory-writer-reviewer
   - 뉴스/업데이트 섹션 → astory-writer-curator
   - 의견/비평 섹션 → astory-writer-columnist
   - 데이터 분석 섹션 → astory-writer-analyst

2. 각 섹션에 대해 순차적으로 Task 위임:

Task 위임 (subagent_type: 매핑된 작가 에이전트) 지침:

Adaptive Mode로 블로그 포스트의 특정 섹션을 작성한다.

Adaptive 컨텍스트:
- 모드: Adaptive Mode (섹션별 자동 페르소나 전환)
- 섹션 수: {number_of_sections}개
- 섹션 구조: {section_descriptions}
- 현재 섹션: {current_section_index}/{total_sections}
- 이전 섹션 내용: {previous_sections_content}

콘텐츠 세부정보:
- 제목: (Phase 2에서 수집한 제목)
- 주제: (Phase 2에서 수집한 주제)
- 대상 독자: (Phase 2에서 수집한 독자층)
- 핵심 포인트: (Phase 2에서 수집, 제공된 경우)

리서치 브리프: (Phase 0에서 수집, 가능한 경우)

섹션별 작성 지침:
1. 할당된 섹션의 내용과 목적 분석
2. 페르소나의 음성과 스타일 적용
3. 이전 섹션과의 매끄러운 전환 확보
4. 전체 콘텐츠 일관성 유지

작성 요구사항:
1. Anti-AI 패턴을 위해 astory-writing-standards 스킬 로드
2. 섹션에 적합한 페르소나 스킬 동적 로드
3. 모든 섹션에 Anti-AI 검증 적용
4. 전체에 걸쳐 리서치 브리프 소스 사용

출력 요구사항:
- 담당 섹션 콘텐츠 (H2 제목 + 문단)
- 음성 변화에도 불구하고 일관된 전체 구조
- 적절한 경우 코드 예제와 다이어그램
- 사용한 모든 리서치 소스에 대한 인용

3. 모든 섹션 완료 후:
   - 각 섹션을 순차적으로 결합
   - frontmatter가 포함된 완전한 MDX 생성
   - 페르소나 매핑 정보 포함

사용자 검토를 위해 페르소나 매핑이 포함된 초안 콘텐츠를 반환한다.

---

## PHASE 4: 품질 검증 및 게시

목표: 콘텐츠 품질 검증, 사용자 검토를 위한 초안 제시, 승인된 콘텐츠 저장

### Step 4.0: 품질 검증 (3단계 검증)

**품질 검증 순서**: Anti-AI 검사 → 인용 검증 → 최종 교정

Phase 3 작성 완료 후, 콘텐츠가 게시되기 전에 3단계 품질 검증을 수행한다.

**1단계: Anti-AI 패턴 검사**

writing-standards 스킬을 활용하여 Anti-AI 검증을 수행한다:

다음 콘텐츠에 대해 Anti-AI 검증을 수행한다.

검증 항목:
1. Critical Pattern: "~를 넘어 ~하다" 패턴 탐지 및 대체 제안
2. Forbidden Vocabulary: 금지어 (패러다임, 혁신, 획기적 등) 탐지
3. Empty Intensifiers: 빈 강조어 (매우, 아주, 정말 등) 탐지
4. Structural Issues: 반복적 문장 패턴, 단조로운 문장 길이

출력: 위반 목록과 수정 제안

발견된 위반이 있으면 자동으로 수정을 적용한다.

**2단계: 인용 검증**

인용 및 출처 검증을 수행한다.

검증 항목:
1. 본문 내 모든 사실적 주장에 인용 번호 존재 여부 확인
2. 참고자료 섹션의 완전성 검증
3. 인용 형식 일관성 확인 (저자, 제목, URL, 접근일)
4. 리서치 브리프 소스와 실제 인용 매칭 확인

출력: 누락된 인용 목록, 형식 오류 목록

**3단계: 최종 교정**

최종 교정을 수행한다.

검증 항목:
1. 한다체 문장 종결 일관성 확인
2. 기술 용어 한글 번역 + 영문 병기 확인
3. 문단 구조 검증 (최소 3문장, 논리적 연결)
4. 전체적 흐름과 가독성 최종 점검

출력: 교정된 최종 콘텐츠

품질 검증 통과 후 Step 4.1로 진행한다.

---

### Step 4.1: 초안 요약 제시

작가 에이전트 완료 후, 사용자에게 요약을 제시한다:

**Solo 모드 요약 형식**:
- 모드: Solo Mode
- 작가 페르소나: (선택한 페르소나 이름)
- 제목: (생성/입력된 제목)
- 글자 수: (문자 수)
- 사용한 리서치 소스: (리서치가 수행된 경우 개수)
- 섹션: (H2 제목 목록)

**Crew 모드 요약 형식**:
- 모드: Crew Mode (협업)
- 작가진: (페르소나 이름 목록)
- 제목: (생성/입력된 제목)
- 글자 수: (문자 수)
- 섹션 분배:
  - 섹션 1: {페르소나} - {글자수}자
  - 섹션 2: {페르소나} - {글자수}자
  - ...
- 사용한 리서치 소스: (개수)

**Adaptive 모드 요약 형식**:
- 모드: Adaptive Mode (자동)
- 페르소나 전환: (섹션별 사용된 페르소나 목록)
- 제목: (생성/입력된 제목)
- 글자 수: (문자 수)
- 섹션 매핑:
  - 섹션 1: {페르소나} (이유: {사유})
  - 섹션 2: {페르소나} (이유: {사유})
  - ...
- 사용한 리서치 소스: (개수)

### Step 4.2: 사용자 피드백 수집

AskUserQuestion 파라미터:
- Question: "작성된 초안을 검토하셨나요? 다음 단계를 선택해주세요"
- Header: "검토"
- MultiSelect: false
- Options:
  - Label: "게시 승인"
  - Description: "초안을 승인하고 파일로 저장"
  - Label: "수정 필요"
  - Description: "피드백을 반영해 재작성"
  - Label: "다른 모드/작가로 재시도"
  - Description: "모드 변경 또는 다른 페르소나 선택"

### Step 4.3: 사용자 결정 처리

"게시 승인" 선택 시:
- 파일명 생성: YYYY-MM-DD-{slug}.mdx (현재 날짜 사용)
- 주제/콘텐츠 유형에서 카테고리 결정
- 저장 위치: content/posts/{category}/
- 최종 메타데이터로 frontmatter 업데이트
- 필요시 card.png 및 og 이미지 생성

"수정 필요" 선택 시:
- AskUserQuestion으로 구체적 피드백 수집
- 수정 지시와 함께 작가 에이전트 재호출
- 모드 및 페르소나 선택 유지
- 수정된 초안으로 Step 4.1로 복귀

"다른 모드/작가로 재시도" 선택 시:
- Phase 1: 모드 선택으로 복귀
- 리서치 브리프 및 콘텐츠 세부정보 유지
- 모드 변경 또는 다른 작가 선택 허용
- 동일한 컨텍스트로 새 작가 에이전트 호출

### Step 4.4: 저장 및 완료

Task 위임 (subagent_type: "astory-writer-developer") 지침:

승인된 블로그 포스트를 최종 확정하고 저장한다.

초안 콘텐츠: (Phase 3에서 승인된 초안)
모드: (사용된 모드: solo/crew/adaptive)
파일명: (생성된 파일명)
카테고리: (결정된 카테고리)
저장 경로: content/posts/{category}/{filename}

최종 단계:
1. MDX 문법 검증
2. frontmatter 완전성 확인
3. frontmatter에 모드 메타데이터 추가:
   - mode: solo/crew/adaptive
   - authors: 사용된 페르소나 목록
   - crew/adaptive의 경우: 섹션별 페르소나가 포함된 section_mapping
4. 제목에서 slug 생성
5. 즉시 게시를 위해 draft: false 설정
6. 올바른 위치에 파일 저장
7. 설정된 경우 이미지 생성

파일 경로와 함께 완료 상태를 반환한다.

---

## 빠른 참조

**사용법**: `/astory:post` - 모든 옵션은 대화형으로 수집됨

**모드 선택 가이드**:

- **Solo Mode**:
  - 적합 대상: 빠른 작성, 일관된 스타일, 단일 관점
  - 활용 사례: 블로그 포스트, 튜토리얼, 개인 에세이

- **Crew Mode**:
  - 적합 대상: 다양한 관점, 전문성 통합, 종합 가이드
  - 활용 사례: 비교 분석, 심층 리포트, 다면적 주제

- **Adaptive Mode**:
  - 적합 대상: 자동 최적화, 복합 주제, 균형 잡힌 구성
  - 활용 사례: 복잡한 기술 문서, 다양한 독자층, 자동 섹션 구성

**일반적인 시나리오**:

- **기술 딥다이브**: Solo Mode → "기술 아키텍트"
  - 스타일: 격식체 한다체, 분석적, 권위적

- **튜토리얼 작성**: Solo Mode → "실무 개발자" 또는 "교육 멘토"
  - 스타일: 대화체, 경험 기반 또는 체계적

- **종합 가이드**: Crew Mode → 아키텍트 + 개발자 + 멘토
  - 섹션: 개념 설명 + 구현 + 학습 로드맵

- **제품 비교**: Crew Mode → 분석가 + 리뷰어
  - 섹션: 시장 분석 + 사용 경험 비교

- **복합 기술 포스트**: Adaptive Mode → AI가 섹션별 자동 선택
  - 예시: 개념(아키텍트) → 구현(개발자) → 트러블슈팅(리뷰어)

**작가 페르소나 빠른 참조**:

- 기술 아키텍트: 격식체, 분석적, 한다체, 3인칭
- 실무 개발자: 실용적, 대화체, 구어체, 1인칭
- 스토리텔러: 공감적, 서사적, 서사체, 1인칭
- 교육 멘토: 체계적, 단계별, 해요체, 2인칭
- 산업 분석가: 객관적, 데이터 기반, 한다체, 3인칭
- 제품 리뷰어: 균형 잡힌, 비교 분석, 해요체, 혼합
- 뉴스 큐레이터: 간결한, 사실적, 한다체, 3인칭
- 칼럼니스트: 비판적, 도발적, 혼합체, 1인칭

**메타데이터**:

버전: 4.0.0
생성일: 2025-12-05
수정일: 2026-01-07
패턴: Hybrid Author System - 순차적 5단계 다중 모드 에이전트 위임
준수사항: CLAUDE.md 모범 사례 + AI 작가 시스템 설계
아키텍처: Commands -> Agents -> Skills (완전 위임)
모드: 대화형 전용 (모든 파라미터는 AskUserQuestion을 통해 수집)
변경 이력:
- v4.0.0: Solo/Crew/Adaptive 모드가 포함된 Hybrid Author System 추가
- v4.0.0: Crew 모드에서 다중 작가 협업 지원
- v4.0.0: Adaptive 모드에서 자동 페르소나 선택
- v4.0.0: 모드 및 섹션 매핑이 포함된 향상된 메타데이터
- v3.0.0: 8개 AI 작가 페르소나 시스템으로 완전 재작성
- v3.0.0: astory-researcher 에이전트를 통한 Phase 0 리서치 추가
- v3.0.0: 페르소나별 작가 에이전트 라우팅
- v3.0.0: Anti-AI 패턴 검증 통합
- v2.5.0: 단일 content-writer 에이전트를 사용한 이전 버전

---

## 최종 단계: 다음 액션 선택

콘텐츠 생성 완료 후, AskUserQuestion 도구를 사용하여 사용자에게 다음 액션을 안내한다:

**요구사항**:

- 생성 완료 요약을 마크다운 형식으로 표시
  - WHY: 완료된 작업에 대한 사용자 확인 제공
  - IMPACT: 시스템에 대한 사용자 신뢰도 향상

- 명확한 다음 액션 옵션 제시 (비차단)
  - WHY: 사용자 자율성과 의사결정 존중
  - IMPACT: 정보에 기반한 워크플로우 진행 가능

- 모든 사용자 대면 출력에 한국어 사용 (설정에 따라)
  - WHY: 언어 설정으로 사용자가 모든 커뮤니케이션을 이해하도록 보장
  - IMPACT: 잘못된 언어 사용은 사용성 문제 야기

- 모든 AskUserQuestion 필드에서 이모지 제외
  - WHY: 인터페이스 간 이모지 지원이 다양함
  - IMPACT: 시스템 간 일관된 포맷팅

**다음 단계 옵션**:

1. **게시물 미리보기**
   - 액션: 생성된 MDX 파일을 미리보기로 열기
   - WHY: 게시 전 콘텐츠 확인

2. **새 게시물 작성**
   - 액션: 새 주제로 `/astory:post` 실행
   - WHY: 지속적인 콘텐츠 생성 가능

3. **게시물 수정**
   - 액션: 생성된 파일을 수동 편집용으로 열기
   - WHY: AI 생성 콘텐츠의 세부 조정 허용

4. **완료**
   - 액션: 세션 완료
   - WHY: 작업 완료 시 우아한 종료 허용

---

## 실행 지시문

이 커맨드를 구현할 때, 위에 문서화된 실행 철학과 페이즈 구조를 정확히 따라야 한다.

**필수 액션**:

1. Phase 0 실행: 리서치 (선택)
   - AskUserQuestion으로 리서치 필요 여부 확인
   - 필요한 경우: 주제/URL 수집 및 astory-researcher 에이전트 호출
   - Phase 3에서 사용할 research_brief 저장

2. Phase 1 실행: 모드 선택
   - 3가지 모드 제시: Solo, Crew, Adaptive
   - Solo: 단일 페르소나 선택 (2개 그룹에 걸쳐 8개 옵션)
   - Crew: 작가 수 선택 후 각 작가 + 섹션 선택
   - Adaptive: 섹션 수 선택
   - mode_config 저장

3. Phase 2 실행: 콘텐츠 세부정보
   - AskUserQuestion으로 제목 수집
   - AskUserQuestion으로 주제 설명 수집
   - 대상 독자 수집 (선택)
   - 핵심 포인트 수집 (선택)
   - content_details 저장

4. Phase 3 실행: 작가 에이전트 호출
   - 진행 상황 추적을 위한 TodoWrite 초기화
   - Solo: 선택한 에이전트로 단일 Task() 호출
   - Crew: 순차적으로 여러 Task() 호출
   - Adaptive: 섹션별 적합한 에이전트로 순차 Task() 호출
   - research_brief, mode_config, content_details 전달
   - 에이전트가 페르소나별 음성과 Anti-AI 패턴 적용

5. Phase 4 실행: 검토 및 게시
   - 모드별 세부정보가 포함된 초안 요약 제시
   - AskUserQuestion으로 피드백 수집
   - 승인/수정/재시도 결정 처리
   - 모드 메타데이터와 함께 승인된 콘텐츠 저장

**준수 검증**:

- 도구 사용 규율 검증: Task, AskUserQuestion, TodoWrite만 사용
- 페이즈 실행 검증: 모든 페이즈가 적절한 순서로 실행
- 모드 구현 검증: 모드별 올바른 에이전트 호출
- 페르소나 일관성 검증: 작가가 선택한 페르소나와 일치
- Anti-AI 패턴 검증: 최종 콘텐츠에 금지 표현 없음
- 사용자 제어 검증: 에이전트 위임 전 모든 선호도 수집
- 언어 검증: 모든 사용자 대면 출력이 한국어 (설정에 따라)
- 메타데이터 검증: frontmatter에 모드 및 작가 정보 포함
