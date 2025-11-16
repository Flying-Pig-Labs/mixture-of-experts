# MoE Thinking Coach: Implementation Plan v2.0

> **An AI-powered conversational thinking coach that helps you apply expert decision-making frameworks**

## Executive Summary

We're building a **thinking coach tool** that democratizes expert decision-making by:
1. Understanding your problem through natural conversation
2. Matching you to the right mental models/frameworks
3. Guiding you through structured thinking with adaptive questions
4. Generating visual + text analysis you can use immediately
5. Learning your patterns to give better suggestions over time

**Core Insight**: People don't have a "thinking framework problem" - they have a "knowing which framework to use and how to apply it" problem.

---

## Table of Contents

1. [What We're Really Building](#what-were-really-building)
2. [Product Experience](#product-experience)
3. [Architecture Overview](#architecture-overview)
4. [Core Components](#core-components)
5. [Implementation Phases](#implementation-phases)
6. [Platform Variations](#platform-variations)
7. [Success Metrics](#success-metrics)

---

## What We're Really Building

### The Problem

**Before this tool:**
- Read business books to learn frameworks
- Try to remember which applies when
- Struggle to apply correctly
- End up going with gut feel
- No documentation of reasoning

**After:**
- Describe your problem naturally
- Get matched to right framework
- Answer guided questions
- Get expert-level analysis
- Have documented reasoning

### The Core Value Proposition

**"McKinsey consultant in your pocket"** who:
- ✅ Knows 50+ frameworks
- ✅ Suggests which fits your situation
- ✅ Asks the right questions
- ✅ Applies the framework properly
- ✅ Gives you structured, shareable output
- ✅ Learns your patterns over time

### What Makes It Different

Not just another chatbot or decision tool:
- **Conversational + Structured**: Natural conversation meets expert frameworks
- **Adaptive**: Branches based on your answers, not rigid scripts
- **Visual + Text**: Rich dashboards + formatted reports
- **Learning**: Gets better as you use it
- **Multi-modal**: Text, voice, visual inputs
- **Context-aware**: Remembers your history, suggests proactively

---

## Product Experience

### 1. Opening Experience

**Simple, Natural Entry Point**

```
┌─────────────────────────────────────────────────────────┐
│                                                         │
│         🧠 What decision are you working on?            │
│                                                         │
│  ┌───────────────────────────────────────────────────┐ │
│  │ Should we migrate to microservices?              │ │
│  └───────────────────────────────────────────────────┘ │
│                                                         │
│         🎤 Speak    ⌨️ Type    📋 Past Decisions       │
│                                                         │
└─────────────────────────────────────────────────────────┘
```

**What happens:**
- NLP analyzes: context, intent, emotional tone, complexity
- Classifies decision type: technical, strategic, hiring, product, etc.
- Identifies key themes: risk, comparison, timing, resource allocation

---

### 2. Smart Framework Matching

**AI suggests 2-4 relevant frameworks with visual previews**

```
┌─────────────────────────────────────────────────────────────┐
│ Based on your technical architecture decision, I suggest:   │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│ ⭐ Inversion (20 min) - Recommended                         │
│ "Think about how this migration could fail"                │
│                                                             │
│ Why this fits: High-risk decision + you mentioned concerns │
│                                                             │
│ [Visual: Simple flowchart showing "Goal → Failures         │
│          → Mitigations → Decision"]                        │
│                                                             │
│ ┌─────────────────────────┐                                │
│ │    Start Inversion      │                                │
│ └─────────────────────────┘                                │
│                                                             │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│ 📊 Weighted Decision Matrix (30 min)                        │
│ "Compare microservices vs alternatives with scoring"       │
│                                                             │
│ Why this fits: You have multiple options to evaluate       │
│                                                             │
│ [Visual: Simple 3x4 grid showing comparison matrix]        │
│                                                             │
│ ┌─────────────────────────┐                                │
│ │   Start Matrix Analysis │                                │
│ └─────────────────────────┘                                │
│                                                             │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│ 🔮 Second-Order Thinking (25 min)                           │
│ "Explore consequences of consequences"                     │
│                                                             │
│ [Show all frameworks] [Let me describe more first]         │
│                                                             │
└─────────────────────────────────────────────────────────────┘
```

**Key UX Patterns:**
- Progressive disclosure (show 2-4, not 50)
- Clear "why this fits" explanations
- Visual preview of structure
- Time estimates
- Recommended choice highlighted

---

### 3. Guided Conversation Flow

**One question at a time, adaptive, with context**

```
┌─────────────────────────────────────────────────────────────┐
│ Applying: Inversion                                   [1/4] │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│ 🎯 What is the primary outcome you're aiming for?          │
│                                                             │
│ ℹ️  This helps me understand what "success" looks like     │
│    so we can identify what would prevent it                │
│                                                             │
│  ┌────────────────────────────────────────────────────────┐│
│  │ Successfully migrate to microservices by Q3 with...   ││
│  │                                                        ││
│  └────────────────────────────────────────────────────────┘│
│                                                             │
│  🎤 Voice input    Skip this question →                    │
│                                                             │
│                                                    [Next] │
│                                                             │
└─────────────────────────────────────────────────────────────┘
```

**Chain of Thought Display (builds trust)**

```
┌─────────────────────────────────────────────────────────────┐
│ 💭 Based on your goal to "reduce deployment time," I'm     │
│    focusing my next questions on velocity and operational  │
│    complexity risks rather than cost concerns.             │
└─────────────────────────────────────────────────────────────┘
```

**Reflection Pattern (ensures alignment)**

After 2-3 questions:

```
┌─────────────────────────────────────────────────────────────┐
│ ✨ So far, I understand:                                    │
│                                                             │
│  • Main concern: Team capacity and skills                  │
│  • Key worry: Operational complexity explosion            │
│  • Timeline: Q3 2026 target                                │
│  • Not mentioned yet: Budget constraints                   │
│                                                             │
│  [That's right ✓]  [Let me clarify...]                     │
└─────────────────────────────────────────────────────────────┘
```

**Adaptive Branching**

If user mentions "budget" → AI explores deeper:

```
┌─────────────────────────────────────────────────────────────┐
│ 💡 You mentioned budget constraints. Let me explore that:   │
│                                                             │
│ Are budget concerns:                                        │
│  ○ A hard constraint (must stay under $X)                  │
│  ○ A consideration (prefer cheaper, but flexible)          │
│  ○ Not a major factor                                      │
└─────────────────────────────────────────────────────────────┘
```

---

### 4. Analysis Output: Visual + Structured

**Decision Dashboard (Web)**

```
┌─────────────────────────────────────────────────────────────┐
│ ⚡ Decision Analysis: Microservices Migration               │
│ Framework: Inversion | Completed: Nov 16, 2025             │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│ 📊 RECOMMENDATION                                           │
│ ┌─────────────────────────────────────────────────────────┐ │
│ │ DELAY 6-9 months for preparation                       │ │
│ │ Confidence: 73%                                        │ │
│ └─────────────────────────────────────────────────────────┘ │
│                                                             │
│ 🔥 RISK HEAT MAP                                            │
│ ┌─────────────────────────────────────────────────────────┐ │
│ │      High Impact                                       │ │
│ │         ↑                                              │ │
│ │         │    [Team Skills Gap] 🔴                      │ │
│ │         │    [Data Consistency] 🔴                     │ │
│ │         │                                              │ │
│ │         │    [Velocity Drop] 🟡                        │ │
│ │         │                 [Cost] 🟡                    │ │
│ │         │                                              │ │
│ │         └──────────────────────────→                   │ │
│ │                    High Probability                    │ │
│ └─────────────────────────────────────────────────────────┘ │
│                                                             │
│ 📋 KEY FINDINGS                                             │
│                                                             │
│  Critical Gaps (Fix Before Proceeding):                    │
│  🔴 Team lacks distributed systems experience              │
│  🔴 No service mesh or distributed tracing                 │
│  🔴 Data consistency strategy undefined                    │
│                                                             │
│  Moderate Concerns:                                        │
│  🟡 Dev velocity will drop 40-60% during migration         │
│  🟡 Infrastructure costs likely 2-4x higher                │
│                                                             │
│ 🎯 NEXT STEPS (Priority Order)                              │
│                                                             │
│  ☐ Month 1-2: Hire senior distributed systems engineer    │
│  ☐ Month 3-5: Extract 1 non-critical service (learning)   │
│  ☐ Month 6-7: Set up service mesh + observability         │
│  ☐ Month 8-9: Design data consistency strategy            │
│  ☐ Month 10: Reassess readiness                           │
│                                                             │
│ ❓ UNANSWERED QUESTIONS                                     │
│                                                             │
│  • What's your budget for infrastructure increase?         │
│  • Can you afford 40% velocity drop for 6 months?         │
│  • Have you validated microservices actually solve pain?  │
│                                                             │
│ ⚙️  [Export PDF] [Share to Slack] [Edit Decision]          │
│                                                             │
└─────────────────────────────────────────────────────────────┘
```

**Structured Text Output (for sharing)**

Auto-formatted markdown ready to paste into Slack, Notion, or commit to git:

```markdown
# Decision Analysis: Microservices Migration

**Framework**: Inversion
**Date**: November 16, 2025
**Confidence**: 73%

## Recommendation
**DELAY** migration for 6-9 months to address critical preparation gaps.

## Key Findings

### Critical Gaps (🔴 Fix Before Proceeding)
- Team lacks distributed systems production experience
- Infrastructure: No service mesh, distributed tracing, or observability
- Data strategy: No plan for distributed transactions/consistency

### Moderate Concerns (🟡 Manage Carefully)
- Development velocity will drop 40-60% for 6+ months
- Infrastructure costs projected 2-4x current spend

## Failure Mode Analysis

| Failure Mode | Probability | Impact | Risk Score | Mitigation Status |
|--------------|-------------|--------|------------|-------------------|
| Team skills gap | 9/10 | 9/10 | 81 | WEAK |
| Data consistency issues | 7/10 | 10/10 | 70 | NONE |
| Operational complexity | 8/10 | 8/10 | 64 | WEAK |
...

## Recommended Actions

**Months 1-2**: Preparation
- Hire senior distributed systems engineer
- Set up foundational infrastructure (service mesh, tracing, logging)

**Months 3-5**: Learning
- Extract first non-critical service (e.g., notifications)
- Entire team participates in design and operations

...

## Unanswered Questions
- Budget capacity for 2-4x infrastructure cost increase?
- Business can accept 40% velocity drop for 6 months?
- Root cause validation: Do microservices actually solve the pain points?

---
*Generated with MoE Thinking Coach*
```

---

### 5. Session Memory & Learning

**Sidebar Navigation (Persistent)**

```
┌─────────────────────┐
│ 🏠 Home             │
│                     │
│ 📝 Current Session  │
│   Microservices     │
│   Migration         │
│                     │
│ 📚 Recent Decisions │
│   • Hire Sr Eng     │
│   • Pricing Change  │
│   • AWS vs GCP      │
│                     │
│ 📊 Your Patterns    │
│   Most Used:        │
│   • Inversion       │
│   • Pre-Mortem      │
│                     │
│   Underused:        │
│   • 2nd Order       │
│                     │
│ 👥 Team Decisions   │
│   (Pro plan)        │
│                     │
│ ⚙️  Settings        │
└─────────────────────┘
```

**Pattern Learning (shown periodically)**

```
┌─────────────────────────────────────────────────────────────┐
│ 💡 I've noticed in your last 5 technical decisions:         │
│                                                             │
│  • You tend to underweight operational complexity risks    │
│  • You're optimistic about timelines (avg 40% longer)      │
│  • You prioritize team impact over cost                    │
│                                                             │
│  Should I emphasize operational concerns more in future    │
│  technical decisions?  [Yes] [No] [Maybe]                  │
└─────────────────────────────────────────────────────────────┘
```

---

### 6. Proactive Features

**Calendar Integration Suggestions**

```
┌─────────────────────────────────────────────────────────────┐
│ 📅 You have "Product Roadmap Meeting" tomorrow at 2pm      │
│                                                             │
│ 💡 Want to run a Pre-Mortem on the Q1 launch plan?         │
│                                                             │
│  [Yes, start now]  [Remind me 1 hour before]  [Dismiss]   │
└─────────────────────────────────────────────────────────────┘
```

**Blind Spot Detection (Mid-Conversation)**

```
┌─────────────────────────────────────────────────────────────┐
│ ⚠️  Hold on - I notice you haven't mentioned competitors    │
│                                                             │
│    In similar architecture decisions where competitors were│
│    overlooked, teams regretted it later when they couldn't │
│    match new features due to tech constraints.             │
│                                                             │
│    Should we explore competitive implications?             │
│                                                             │
│  [Yes, good catch]  [Not relevant here]                    │
└─────────────────────────────────────────────────────────────┘
```

**Decision Replay (Learning Tool)**

```
┌─────────────────────────────────────────────────────────────┐
│ 🔄 Decision Replay: "Hire Frontend Lead" (6 months ago)    │
│                                                             │
│  Then: You prioritized "Culture Fit" (40% weight)          │
│  Now: Would you change this?                               │
│                                                             │
│  Outcome: Hire worked out well, but slower ramp than       │
│           expected due to skills gap                       │
│                                                             │
│  Lesson: Consider increasing "Skills" weight in future     │
│          hiring decisions?                                 │
└─────────────────────────────────────────────────────────────┘
```

---

## Architecture Overview

### High-Level Architecture

```
┌─────────────────────────────────────────────────────────────┐
│                   CLIENT LAYER                              │
│                                                             │
│  ┌──────────┐  ┌──────────┐  ┌──────────┐  ┌──────────┐  │
│  │ Web App  │  │ Mobile   │  │  Slack   │  │   CLI    │  │
│  │ (React)  │  │  (RN)    │  │   Bot    │  │ (Python) │  │
│  └──────────┘  └──────────┘  └──────────┘  └──────────┘  │
│       │              │              │             │        │
└───────┼──────────────┼──────────────┼─────────────┼────────┘
        │              │              │             │
        └──────────────┴──────────────┴─────────────┘
                           │
                           ↓ GraphQL API / REST
┌─────────────────────────────────────────────────────────────┐
│                  APPLICATION LAYER                          │
│                                                             │
│  ┌─────────────────────────────────────────────────────┐  │
│  │  API Gateway (Node.js / Python FastAPI)            │  │
│  │  • Authentication (Auth0 / Clerk)                   │  │
│  │  • Rate limiting                                    │  │
│  │  • Request routing                                  │  │
│  └─────────────────────────────────────────────────────┘  │
│                           │                                 │
│         ┌─────────────────┼─────────────────┐              │
│         ↓                 ↓                 ↓              │
│  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐       │
│  │Conversation │  │  Analysis   │  │  Learning   │       │
│  │   Engine    │  │   Engine    │  │   Engine    │       │
│  │             │  │             │  │             │       │
│  │ • NLP       │  │ • Framework │  │ • Pattern   │       │
│  │ • Intent    │  │   Matching  │  │   Detection │       │
│  │ • Adaptive  │  │ • Question  │  │ • User      │       │
│  │   Branching │  │   Gen       │  │   Modeling  │       │
│  │ • Context   │  │ • LLM       │  │ • Suggest   │       │
│  │   Mgmt      │  │   Prompts   │  │   Engine    │       │
│  └─────────────┘  └─────────────┘  └─────────────┘       │
│                                                             │
└─────────────────────────────────────────────────────────────┘
                           │
                           ↓
┌─────────────────────────────────────────────────────────────┐
│                    DATA LAYER                               │
│                                                             │
│  ┌──────────────┐  ┌──────────────┐  ┌──────────────┐     │
│  │  PostgreSQL  │  │    Redis     │  │  Vector DB   │     │
│  │              │  │              │  │  (Pinecone/  │     │
│  │ • Users      │  │ • Sessions   │  │   Weaviate)  │     │
│  │ • Decisions  │  │ • Cache      │  │              │     │
│  │ • Patterns   │  │ • Pub/Sub    │  │ • Embeddings │     │
│  │ • Teams      │  │              │  │ • Semantic   │     │
│  │              │  │              │  │   Search     │     │
│  └──────────────┘  └──────────────┘  └──────────────┘     │
│                                                             │
└─────────────────────────────────────────────────────────────┘
                           │
                           ↓
┌─────────────────────────────────────────────────────────────┐
│                   SERVICES LAYER                            │
│                                                             │
│  ┌──────────────┐  ┌──────────────┐  ┌──────────────┐     │
│  │ Claude API   │  │  Rendering   │  │  Storage     │     │
│  │              │  │              │  │              │     │
│  │ • Analysis   │  │ • Charts     │  │ • S3 / GCS   │     │
│  │ • Synthesis  │  │ • PDF Gen    │  │ • Reports    │     │
│  │ • Embeddings │  │ • Markdown   │  │ • Exports    │     │
│  └──────────────┘  └──────────────┘  └──────────────┘     │
│                                                             │
└─────────────────────────────────────────────────────────────┘
```

---

## Core Components

### 1. Conversation Engine

**Purpose**: Manage adaptive, context-aware conversations

**Responsibilities**:
- **Intent Classification**: Understand what type of decision (technical, hiring, product, strategic)
- **Context Management**: Track conversation state, previous questions/answers
- **Adaptive Branching**: Decide next question based on user responses
- **Natural Language Understanding**: Parse user inputs (including voice transcription)
- **Reflection Generation**: Periodically summarize understanding

**Key Technologies**:
- **NLP**: spaCy or Hugging Face Transformers for intent/entity extraction
- **State Management**: State machine (XState) for conversation flow
- **LLM Integration**: Claude for adaptive question generation and context understanding

**Data Model**:

```typescript
interface ConversationState {
  sessionId: string
  userId: string
  currentPhase: 'problem_input' | 'framework_selection' | 'guided_questions' | 'analysis_review'
  problemDescription: string
  selectedFramework?: string
  conversationHistory: Message[]
  extractedContext: {
    decisionType: string
    keywords: string[]
    emotionalTone: 'confident' | 'uncertain' | 'concerned'
    complexity: 'simple' | 'moderate' | 'complex'
  }
  questionsAsked: Question[]
  userAnswers: Record<string, any>
  metadata: {
    startedAt: Date
    lastActivity: Date
    branchingPoints: number
  }
}
```

---

### 2. Analysis Engine

**Purpose**: Match frameworks, generate questions, apply frameworks to create analysis

**Responsibilities**:
- **Framework Matching**: Given problem description, rank relevant frameworks
- **Question Generation**: Create contextual, adaptive questions for selected framework
- **Analysis Synthesis**: Apply framework logic to user answers, generate insights
- **Visual Data Prep**: Format data for charts (risk heat maps, decision matrices)
- **Output Generation**: Create structured markdown, JSON, and visual formats

**Key Technologies**:
- **Framework Registry**: YAML-based mental model library (existing)
- **LLM Prompting**: Claude with specialized prompts per framework
- **Template Engine**: Jinja2 for dynamic question/output generation
- **Data Viz Prep**: Transform analysis results into chart-ready JSON

**Core Functions**:

```python
class AnalysisEngine:
    def match_frameworks(
        self,
        problem_description: str,
        context: dict
    ) -> List[FrameworkMatch]:
        """
        Returns 2-4 best-fit frameworks with relevance scores and reasons
        """
        pass

    def generate_questions(
        self,
        framework_id: str,
        problem: str,
        known_answers: dict,
        conversation_context: dict
    ) -> List[AdaptiveQuestion]:
        """
        Generates next question(s) based on framework requirements
        and conversation history. Adaptive branching.
        """
        pass

    def apply_framework(
        self,
        framework_id: str,
        problem: str,
        answers: dict
    ) -> AnalysisResult:
        """
        Applies framework logic, returns structured analysis with:
        - Recommendation
        - Key findings
        - Risk assessment
        - Next steps
        - Unanswered questions
        - Visualizations (heat maps, matrices)
        """
        pass
```

---

### 3. Learning Engine

**Purpose**: Learn user patterns, provide personalized suggestions, detect blind spots

**Responsibilities**:
- **Pattern Detection**: Analyze past decisions to find trends
- **Personalized Suggestions**: Recommend frameworks based on user history
- **Blind Spot Detection**: Flag missing considerations (e.g., "you didn't mention competitors")
- **Proactive Prompts**: Suggest decisions based on calendar, context
- **Outcome Tracking**: Learn from decision outcomes over time

**Key Technologies**:
- **ML Models**: Simple classification for pattern detection (scikit-learn or simple heuristics initially)
- **Embeddings**: Store decision embeddings for similarity search (vector DB)
- **Rule Engine**: Pattern matching rules for common blind spots

**Data Model**:

```typescript
interface UserProfile {
  userId: string
  patterns: {
    mostUsedFrameworks: FrameworkUsage[]
    underweightedFactors: string[]  // e.g., "cost", "competitors"
    timelineOptimismBias: number    // % avg underestimation
    decisionsByType: Record<string, number>
  }
  preferences: {
    skillLevel: 'beginner' | 'intermediate' | 'expert'
    preferredModality: 'text' | 'voice' | 'mixed'
    verbosity: 'concise' | 'standard' | 'detailed'
  }
  history: Decision[]
}

interface Decision {
  id: string
  date: Date
  problem: string
  frameworkUsed: string
  outcome?: {
    result: 'success' | 'mixed' | 'failure'
    lessonsLearned: string[]
    whatChanged: string[]
  }
}
```

---

### 4. Rendering Engine

**Purpose**: Generate visual and text outputs

**Responsibilities**:
- **Charts**: Risk heat maps, decision matrices, timeline views
- **PDF Generation**: Formatted reports
- **Markdown**: Clean, shareable text
- **Integration Formats**: Slack, Notion, Confluence

**Technologies**:
- **Charts**: D3.js or Chart.js for web, exported to PNG/SVG
- **PDF**: Puppeteer or react-pdf
- **Markdown**: markdown-it or remark
- **Templates**: React components for web, Jinja2 for text

---

## Implementation Phases

### Phase 0: Foundation (Weeks 1-2)

**Goal**: Establish core infrastructure and validate approach

**Deliverables**:
- [ ] Repository structure (monorepo: web app + API + shared libs)
- [ ] Mental model registry (10 frameworks defined in YAML)
- [ ] Basic data models (User, Session, Decision, Framework)
- [ ] Development environment (local setup, Docker)
- [ ] LLM integration (Claude API wrapper)

**Success Criteria**:
- Can load framework definitions
- Can call Claude API with simple prompts
- Database schema validated

---

### Phase 1: Conversation Engine MVP (Weeks 3-5)

**Goal**: Build adaptive conversation flow for 1 framework

**Deliverables**:
- [ ] Problem input with NLP analysis (intent, keywords, complexity)
- [ ] Framework matching (simple scoring algorithm)
- [ ] Guided question flow for Inversion framework
- [ ] Conversation state management
- [ ] Basic reflection/summary generation

**Tech Stack**:
- Backend: Python FastAPI or Node.js Express
- State: Redis for session state
- DB: PostgreSQL for persistence
- LLM: Claude Sonnet 4.5

**Success Criteria**:
- User can describe problem → get framework suggestions
- User can select Inversion → complete guided Q&A
- Conversation adapts based on answers (simple branching)
- Session persists and can be resumed

---

### Phase 2: Analysis Engine (Weeks 6-7)

**Goal**: Generate structured analysis from user inputs

**Deliverables**:
- [ ] Apply framework templates (Inversion only initially)
- [ ] Structured output generation (findings, risks, recommendations)
- [ ] Simple data prep for visualizations (JSON output)
- [ ] Markdown export
- [ ] "Unanswered questions" detection

**Success Criteria**:
- Complete Inversion flow end-to-end
- Output includes: recommendation, key findings, next steps
- Markdown export works
- Output quality validated by 5 beta users

---

### Phase 3: Web Interface (Weeks 8-10)

**Goal**: Beautiful, usable web app

**Deliverables**:
- [ ] Landing page + signup/login (Auth0 or Clerk)
- [ ] Problem input screen (text + voice)
- [ ] Framework selection UI with visual previews
- [ ] Guided question interface (one question at a time)
- [ ] Analysis dashboard with basic charts
- [ ] Session history sidebar
- [ ] Export options (PDF, Markdown, Slack)

**Tech Stack**:
- Frontend: React + TypeScript
- Styling: Tailwind CSS
- Charts: Recharts or Chart.js
- Voice: Web Speech API (basic)
- State: React Query + Zustand

**Success Criteria**:
- Complete user journey works smoothly
- Mobile-responsive
- Fast (<2s load time)
- Accessible (WCAG AA)

---

### Phase 4: Multi-Framework Support (Weeks 11-12)

**Goal**: Expand to 5 core frameworks

**Frameworks to Add**:
1. ✅ Inversion (done in Phase 1-2)
2. Weighted Decision Matrix
3. Pre-Mortem
4. First Principles
5. SMART Goals

**Deliverables**:
- [ ] 4 additional framework definitions
- [ ] Framework-specific question templates
- [ ] Framework-specific analysis templates
- [ ] Visual outputs per framework (matrices, trees, etc.)

**Success Criteria**:
- 5 frameworks work end-to-end
- Framework matching suggests right one >80% of time (user feedback)
- Each framework has distinct, valuable output

---

### Phase 5: Learning & Personalization (Weeks 13-15)

**Goal**: Make it smarter over time

**Deliverables**:
- [ ] User profile and pattern tracking
- [ ] "Most used frameworks" stats
- [ ] Simple blind spot detection (rule-based)
- [ ] "You tend to..." insights
- [ ] Framework recommendation based on history

**Success Criteria**:
- After 3 decisions, system shows accurate patterns
- Blind spot detection fires at right moments (not annoying)
- Recommendations improve with use (A/B test)

---

### Phase 6: Platform Expansion (Weeks 16-20)

**Goal**: Multi-platform access

**Deliverables**:

**Mobile App** (React Native):
- [ ] Simplified, voice-first interface
- [ ] Core flow (problem → framework → questions → analysis)
- [ ] Sync with web

**Slack Integration**:
- [ ] `/decide` slash command
- [ ] In-channel guided flow
- [ ] Formatted output for thread discussions
- [ ] Team decision sharing

**CLI** (Original Vision):
- [ ] Terminal interface using web API
- [ ] Session management
- [ ] Markdown output for piping to files

**Success Criteria**:
- Each platform handles core flow
- Data syncs across platforms
- Slack sees 20% adoption in beta companies

---

### Phase 7: Team Features (Weeks 21-24)

**Goal**: Collaborative decision-making

**Deliverables**:
- [ ] Team workspaces
- [ ] Shared decision library
- [ ] Multi-stakeholder input (parallel answers)
- [ ] Disagreement highlighting
- [ ] Team pattern analysis

**Success Criteria**:
- Teams of 5-10 can collaborate on decisions
- Disagreements surfaced clearly
- Team patterns (e.g., "we underweight UX") shown

---

## Platform Variations

### Web App (Primary)

**Target Users**: Individual knowledge workers, managers, founders

**Key Features**:
- Full-featured dashboard
- Rich visualizations
- Long-form analysis
- History and patterns
- Export options

**Technical Approach**:
- React + TypeScript
- Server-side rendering (Next.js) for SEO
- Real-time updates (WebSockets for live analysis)

---

### Mobile App

**Target Users**: Busy decision-makers on-the-go

**Key Features**:
- Voice-first input
- Simplified UI (focus on current decision)
- Push notifications (proactive suggestions)
- Quick review mode (swipe through findings)

**Technical Approach**:
- React Native (code sharing with web)
- Offline support (queue decisions, sync later)
- Native speech recognition

---

### Slack Integration

**Target Users**: Teams making decisions collaboratively

**Key Features**:
- `/decide [problem]` to start
- In-channel Q&A
- Thread-based discussions
- Auto-post to #decisions channel
- Mention team members for input

**Technical Approach**:
- Slack Bolt framework
- Slash commands + interactive messages
- Block Kit for rich formatting

---

### CLI

**Target Users**: Engineers, technical decision-makers

**Key Features**:
- Fast, keyboard-driven
- Pipe-able outputs
- Git integration (commit decisions as ADRs)
- Session management in ~/.moe/

**Technical Approach**:
- Python with Typer or Rich
- Calls web API
- Local config for API keys

---

## Success Metrics

### Product Metrics

**Activation**:
- % of signups who complete first decision: >60%
- Time to first decision: <10 minutes

**Engagement**:
- Decisions per user per month: >2
- Return rate (use within 7 days): >40%
- Session completion rate: >70%

**Value**:
- User rating "Was this helpful?": >4.0/5.0
- Framework relevance (right suggestion): >80%
- Output usage (exported/shared): >50%

### Quality Metrics

**Analysis Quality**:
- Expert review of outputs: >7/10 quality score
- User reports analysis was thorough: >75%
- Users discover new considerations: >80%

**Conversation Quality**:
- Questions clear and answerable: >85% approval
- Conversation feels natural: >4/5 rating
- Adaptive branching adds value: >70% notice it

### Business Metrics

**Growth**:
- Month-over-month user growth: >20%
- Word-of-mouth referrals: >30% of signups
- Retention (30-day): >50%

**Monetization** (Post-Beta):
- Free → Paid conversion: >10%
- Team plan adoption: >5 teams in first quarter
- Avg revenue per user: $15-30/month

---

## Technical Stack Summary

### Backend
- **API**: Python FastAPI or Node.js Express
- **Database**: PostgreSQL (relational) + Redis (cache/sessions)
- **Vector DB**: Pinecone or Weaviate (embeddings)
- **LLM**: Claude Sonnet 4.5 (Anthropic)
- **Auth**: Auth0 or Clerk
- **Hosting**: Vercel (API) or Railway

### Frontend (Web)
- **Framework**: React + TypeScript + Next.js
- **Styling**: Tailwind CSS
- **Charts**: Recharts or D3.js
- **State**: React Query + Zustand
- **Forms**: React Hook Form

### Mobile
- **Framework**: React Native
- **State**: Redux or Zustand
- **Storage**: AsyncStorage + SQLite

### Infrastructure
- **Hosting**: Vercel (frontend), Railway/Render (backend)
- **CDN**: Cloudflare
- **Monitoring**: Sentry + PostHog
- **Analytics**: PostHog or Mixpanel

---

## Open Questions

1. **Voice Quality**: How critical is voice transcription accuracy? (affects choice of speech API)
2. **Real-time vs Async**: Should analysis generation be real-time (streaming) or async (job queue)?
3. **Pricing Model**: Freemium with usage limits, or free trial → paid?
4. **Framework Authoring**: Allow users to create custom frameworks? (Complexity vs power-user value)
5. **Team vs Individual**: Build for individuals first, teams later? Or co-develop?
6. **Data Privacy**: How to handle sensitive decision data? End-to-end encryption needed?

---

## Next Steps

### This Week
1. ✅ Finalize product vision and implementation plan
2. ⏭️ Set up development environment (repo, tools, API keys)
3. ⏭️ Define 10 frameworks in YAML (Inversion + 9 more)
4. ⏭️ Validate data models (schema design)
5. ⏭️ Create simple framework matching algorithm (v0)

### Next 2 Weeks (Phase 1 Kickoff)
1. Build conversation engine MVP
2. Implement Inversion framework end-to-end
3. Test with 3-5 real decisions
4. Gather feedback, iterate

---

**End of Implementation Plan v2.0**

*This is a living document - update as we learn and build*
