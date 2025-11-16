# Mixture of Experts: AI-Powered Thinking Coach

> **An intelligent conversational assistant that helps you apply expert decision-making frameworks without needing to be an expert**

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

---

## What Is This?

**MoE Thinking Coach** is an AI-powered tool that democratizes expert decision-making by:

1. **Understanding your problem** through natural conversation
2. **Matching you to the right mental models/frameworks** (from 50+ options)
3. **Guiding you through structured thinking** with adaptive questions
4. **Generating visual + text analysis** you can use immediately
5. **Learning your patterns** to give better suggestions over time

### The Problem We're Solving

**Before this tool:**
- You read business books to learn frameworks
- You try to remember which applies when
- You struggle to apply them correctly
- You end up going with gut feel
- You have no documentation of your reasoning

**With MoE:**
- You describe your problem naturally (text or voice)
- You get matched to the right framework automatically
- You answer guided questions that adapt to your responses
- You get expert-level structured analysis with visualizations
- You have documented reasoning you can share immediately

---

## Core Product Vision

### "McKinsey Consultant in Your Pocket"

An AI assistant that:
- ✅ Knows 50+ decision-making frameworks
- ✅ Suggests which fits your specific situation
- ✅ Asks you the right questions (adapting based on your answers)
- ✅ Applies the framework properly with LLM-powered analysis
- ✅ Gives you structured, shareable output (dashboards, reports, exports)
- ✅ Learns your decision-making patterns over time
- ✅ Proactively catches blind spots ("you didn't mention competitors")

### What Makes It Different

- **Conversational + Structured**: Natural dialogue meets expert frameworks
- **Adaptive**: Questions branch based on your answers, not rigid scripts
- **Visual + Text**: Rich dashboards, heat maps, matrices + formatted reports
- **Learning**: Gets smarter as you use it (detects your patterns)
- **Multi-modal**: Text, voice, visual inputs
- **Context-aware**: Remembers your history, suggests proactively

---

## How It Works

### 1. Describe Your Decision

```
┌─────────────────────────────────────────────┐
│  🧠 What decision are you working on?       │
│                                             │
│  "Should we migrate to microservices?"     │
│                                             │
│  🎤 Speak    ⌨️ Type    📋 Past Decisions  │
└─────────────────────────────────────────────┘
```

AI analyzes your problem for:
- Decision type (technical, hiring, product, strategic)
- Complexity level
- Key themes (risk, comparison, timing, resources)

### 2. Get Matched to Frameworks

```
Based on your technical architecture decision:

⭐ Inversion (20 min) - Recommended
"Think about how this migration could fail"
[Why: High-risk decision + you mentioned concerns]

📊 Weighted Decision Matrix (30 min)
"Compare microservices vs alternatives"
[Why: Multiple options to evaluate]

🔮 Second-Order Thinking (25 min)
"Explore consequences of consequences"
```

### 3. Guided Conversation

One question at a time, adaptive, with context:

```
🎯 What is the primary outcome you're aiming for?

ℹ️ This helps me understand what "success" looks like

┌────────────────────────────────────────────┐
│ Successfully migrate by Q3 with improved... │
└────────────────────────────────────────────┘

💭 Based on your goal to "reduce deployment time,"
   I'm focusing on velocity and operational risks.

[Next Question →]
```

### 4. Get Visual Analysis

**Risk Heat Map**:
```
     High Impact
         ↑
         │    [Team Skills Gap] 🔴
         │    [Data Consistency] 🔴
         │
         │    [Velocity Drop] 🟡
         │                 [Cost] 🟡
         │
         └──────────────────────────→
                    High Probability
```

**Structured Report**:
- **Recommendation**: DELAY 6-9 months
- **Confidence**: 73%
- **Critical Gaps**: Team lacks expertise, no service mesh
- **Next Steps**: Hire senior engineer, extract 1 service for learning
- **Unanswered Questions**: Budget? Can you afford velocity drop?

**Export Options**:
- 📄 PDF Report
- 📝 Markdown (for docs/git)
- 💬 Slack message
- 📋 Notion/Confluence

---

## Example Use Cases

### For Individual Contributors
- **Technical Decisions**: "Should we use PostgreSQL or MongoDB?"
- **Career Moves**: "Should I take this job offer?"
- **Project Planning**: "How should I prioritize Q1 features?"

### For Managers & Leaders
- **Strategic Planning**: "Should we pivot to B2B?"
- **Hiring**: "Which candidate should we hire?"
- **Resource Allocation**: "Where should we invest our budget?"
- **Risk Assessment**: "What could go wrong with this product launch?"

### For Teams
- **Architecture Reviews**: Document technical decisions as ADRs
- **Product Decisions**: Collaborative framework application
- **Post-Mortems**: Structured retrospectives
- **Planning Sessions**: Pre-mortem before launches

---

## Repository Structure

```
mixture-of-experts/
├── README.md                          # You are here
├── IMPLEMENTATION_PLAN_V2.md          # Detailed technical roadmap
├── COGNITIVE_FRAMEWORKS_LIBRARY.md    # 35+ frameworks reference
│
├── registry/                          # Mental model definitions
│   ├── schema/
│   │   └── model.schema.json
│   ├── models/
│   │   ├── inversion.yaml
│   │   ├── weighted_decision_matrix.yaml
│   │   └── ... (more frameworks)
│   ├── index.yaml
│   └── README.md
│
├── research/                          # Background research
│   ├── MENTAL_MODELS.md
│   ├── COGNITIVE_BIASES.md
│   ├── DECISION_FRAMEWORKS.md
│   ├── PROBLEM_SOLVING.md
│   └── NEURODIVERGENCY_GUIDANCE.md
│
├── frameworks/                        # Visual framework references
│   ├── README.md
│   └── *.jpeg (6 reference images)
│
├── COGNITIVE_TOOLS_MAPPING.md
├── ROLES.md                           # Expert personas
└── PHASES.md                          # Decision processing phases
```

---

## Current Status

**Stage**: Design & Planning ✅

**Completed**:
- ✅ Product vision defined
- ✅ Implementation plan v2.0 complete
- ✅ Mental model registry schema designed
- ✅ 2 example frameworks fully defined (Inversion, Weighted Matrix)
- ✅ Cognitive frameworks library (35+ frameworks documented)
- ✅ Repository structure established

**Next Steps** (Phase 0 - Weeks 1-2):
- [ ] Set up development environment
- [ ] Define 10 core frameworks in YAML
- [ ] Validate data models
- [ ] Create simple framework matching algorithm
- [ ] LLM integration proof-of-concept

---

## Planned Features

### Phase 1-2: Core Experience (Weeks 1-7)
- Conversational problem input with NLP
- Framework matching and selection
- Guided adaptive Q&A for Inversion framework
- Structured analysis output with basic visualizations
- Session persistence

### Phase 3-4: Full Web App (Weeks 8-12)
- Beautiful web interface with rich visuals
- 5 core frameworks (Inversion, Weighted Matrix, Pre-Mortem, First Principles, SMART Goals)
- Dashboard with heat maps, matrices, timelines
- Export to PDF, Markdown, Slack
- Session history and management

### Phase 5-6: Intelligence & Multi-Platform (Weeks 13-20)
- Pattern learning ("you tend to underweight risks")
- Blind spot detection ("you didn't mention competitors")
- Proactive suggestions
- Mobile app (voice-first)
- Slack integration (`/decide` command)
- CLI for developers

### Phase 7: Team Features (Weeks 21-24)
- Team workspaces
- Collaborative decisions
- Multi-stakeholder input
- Shared decision library
- Team pattern analysis

---

## Technology Stack

### Backend
- **API**: Python FastAPI or Node.js
- **Database**: PostgreSQL + Redis + Vector DB
- **LLM**: Claude Sonnet 4.5 (Anthropic)
- **Auth**: Auth0 or Clerk

### Frontend (Web)
- **Framework**: React + TypeScript + Next.js
- **Styling**: Tailwind CSS
- **Charts**: Recharts or D3.js
- **State**: React Query + Zustand

### Mobile
- **Framework**: React Native
- **Voice**: Native speech recognition

### Integrations
- Slack (Bolt framework)
- CLI (Python Typer)

---

## Documentation

### Core Documents
- **[IMPLEMENTATION_PLAN_V2.md](IMPLEMENTATION_PLAN_V2.md)** - Complete technical roadmap with architecture, components, phases
- **[COGNITIVE_FRAMEWORKS_LIBRARY.md](COGNITIVE_FRAMEWORKS_LIBRARY.md)** - Reference library of 35+ frameworks organized by category
- **[registry/README.md](registry/README.md)** - How to contribute new mental models
- **[ROLES.md](ROLES.md)** - Expert personas and specializations
- **[PHASES.md](PHASES.md)** - Decision processing lifecycle

### Research Library
- **[MENTAL_MODELS.md](research/MENTAL_MODELS.md)** - 50+ mental models
- **[COGNITIVE_BIASES.md](research/COGNITIVE_BIASES.md)** - 100+ biases catalog
- **[DECISION_FRAMEWORKS.md](research/DECISION_FRAMEWORKS.md)** - Proven methodologies
- **[PROBLEM_SOLVING.md](research/PROBLEM_SOLVING.md)** - Structured approaches

---

## Product Philosophy

### Core Principles

1. **Democratize Expert Thinking**: You shouldn't need an MBA or years of experience to apply powerful frameworks

2. **Natural Interaction**: Conversation should feel human, not like filling out a form

3. **Adaptive, Not Rigid**: Questions should branch based on your answers, not follow a script

4. **Visual + Structured**: Both rich dashboards for exploration and clean text for sharing

5. **Learning Over Time**: The tool should get better at helping YOU specifically

6. **Actionable Output**: Every analysis should lead to clear next steps

7. **Transparent Reasoning**: Always show why the AI suggested something

---

## Comparison to Other Tools

| Feature | MoE Thinking Coach | Generic ChatGPT | Decision Matrices (Excel) | Consulting Firm |
|---------|-------------------|-----------------|---------------------------|-----------------|
| **Framework Knowledge** | 50+ built-in | General knowledge | None | High (human) |
| **Guided Process** | ✅ Adaptive Q&A | ❌ Freeform chat | ❌ Manual | ✅ Structured |
| **Visual Outputs** | ✅ Dashboards | ❌ Text only | ⚠️ Basic | ✅ Slide decks |
| **Learns Your Patterns** | ✅ Over time | ❌ No memory | ❌ Static | ⚠️ Manual |
| **Cost** | $20-50/month | $20/month | Free | $5,000-50,000 |
| **Speed** | Minutes | Minutes | Hours | Weeks |
| **Consistency** | ✅ Always thorough | ⚠️ Variable | ⚠️ Manual | ⚠️ Varies by consultant |

---

## Success Metrics

### Product Metrics (Target)
- **Activation**: >60% of signups complete first decision
- **Engagement**: >2 decisions per user per month
- **Retention**: >40% return within 7 days
- **Quality**: >4.0/5.0 "Was this helpful?" rating

### Quality Metrics
- **Framework Relevance**: >80% users agree suggestion was right
- **Output Quality**: >7/10 expert review score
- **Discovery**: >80% users find new considerations they hadn't thought of

---

## Contributing

We welcome contributions! Areas of interest:

### Framework Library
- Add new mental models and frameworks
- Improve existing framework definitions
- Add examples and case studies

### Code (Coming Soon)
- Backend (conversation engine, analysis engine)
- Frontend (React components, visualizations)
- Integrations (Slack, Notion, etc.)

### Research
- Decision-making case studies
- Framework effectiveness studies
- UX research and user testing

See [registry/README.md](registry/README.md) for framework contribution guidelines.

---

## Roadmap

### 2025 Q1: Foundation
- ✅ Product vision and design
- ⏭️ Core infrastructure
- ⏭️ 10 frameworks defined
- ⏭️ Conversation engine MVP

### 2025 Q2: Web App Launch
- Web app with 5 frameworks
- Visual dashboards
- Export capabilities
- Beta testing with 50-100 users

### 2025 Q3: Intelligence & Mobile
- Pattern learning
- Blind spot detection
- Mobile app launch
- Slack integration

### 2025 Q4: Team Features
- Team workspaces
- Collaborative decisions
- Public launch

---

## Philosophy: Why "Mixture of Experts"?

The name comes from two sources:

### 1. Machine Learning Architecture
**Mixture of Experts (MoE)** neural networks route inputs to specialized sub-networks. Each "expert" handles what it's good at, and a gating mechanism decides which experts to activate.

**Our Application**: Route decisions to the right mental models/frameworks (the "experts"), with AI as the gating mechanism.

### 2. Decision-Making Wisdom
Good decisions require **multiple perspectives**:
- Strategic thinking (long-term view)
- Risk analysis (what could go wrong)
- First principles (challenge assumptions)
- Second-order thinking (consequences of consequences)
- Empathy (user/stakeholder impact)

**Our Approach**: Apply the right mix of expert frameworks to each unique decision.

---

## License

This project is licensed under the **MIT License** - see the [LICENSE](LICENSE) file for details.

---

## Contact & Support

- **Issues & Bugs**: [GitHub Issues](https://github.com/Flying-Pig-Labs/mixture-of-experts/issues)
- **Discussions**: [GitHub Discussions](https://github.com/Flying-Pig-Labs/mixture-of-experts/discussions)
- **Questions**: Open a discussion or issue

---

## Acknowledgments

### Inspiration
- **Decision Science**: Kahneman, Tversky, Gary Klein, Annie Duke
- **Mental Models**: Shane Parrish (Farnam Street), Charlie Munger
- **Frameworks**: Chip & Dan Heath (WRAP), Dave Snowden (Cynefin), McKinsey, BCG

### Technical Foundations
- **Mixture of Experts**: Neural architecture research (Jacobs et al., Shazeer et al.)
- **Conversational AI**: IBM Watson Decision Assistant, Google Dialogflow patterns
- **Decision Support Systems**: Academic research in DSS and expert systems

---

**Transform complex decisions into structured, expert-level analysis. Think better. Decide smarter.**

*Built with ❤️ by Flying Pig Labs*
