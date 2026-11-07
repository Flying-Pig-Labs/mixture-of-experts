# Mixture of Experts: A Decision Intelligence Framework

> **Transform complex decisions into structured, multi-perspective analysis using specialized expert networks and cognitive frameworks**

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

## Table of Contents

- [Overview](#overview)
- [Core Concept](#core-concept)
- [Why Mixture of Experts for Decision-Making?](#why-mixture-of-experts-for-decision-making)
- [Decision-Making Architecture](#decision-making-architecture)
- [Key Features](#key-features)
- [Documentation Index](#documentation-index)
- [Getting Started](#getting-started)
- [Decision Frameworks](#decision-frameworks)
- [Cognitive Tools & Mental Models](#cognitive-tools--mental-models)
- [Expert Specializations](#expert-specializations)
- [Usage Examples](#usage-examples)
- [Advanced Topics](#advanced-topics)
- [Research Foundation](#research-foundation)
- [Contributing](#contributing)
- [License](#license)

---

## Overview

**Mixture of Experts (MoE)** is a cognitive decision intelligence framework that combines multiple specialized expert perspectives with sophisticated gating mechanisms to tackle complex decision-making challenges. Unlike traditional single-model approaches, MoE orchestrates diverse expert viewpoints—analytical, creative, strategic, ethical, and more—to provide comprehensive, multi-dimensional insights.

This repository serves as both a **practical implementation** and a **research compendium** for applying MoE architectures to:

- **Strategic business decisions** with high stakes and uncertainty
- **Product development** requiring cross-functional expertise
- **Complex problem-solving** across multiple domains
- **Risk assessment** with competing priorities
- **Innovation and creative ideation** demanding diverse perspectives
- **Personal development** and decision coaching

---

## Core Concept

### What is Mixture of Experts?

At its foundation, MoE is inspired by neural network architectures that route inputs to specialized sub-networks (experts), with a gating mechanism determining which experts to activate for each input. Applied to decision-making, this translates to:

```
Complex Decision → Gating Mechanism → Specialized Experts → Weighted Synthesis → Informed Decision
```

**Key Components:**

1. **Expert Networks**: Specialized decision-making personas with distinct cognitive frameworks, expertise areas, and analytical lenses
2. **Gating Mechanism**: Intelligent routing that determines which experts are most relevant for a given decision context
3. **Aggregation Layer**: Synthesis mechanism that combines expert recommendations into actionable insights
4. **Cognitive Tools**: Mental models, frameworks, and bias-mitigation strategies that enhance decision quality

### The Decision Intelligence Advantage

Traditional decision-making often suffers from:
- **Single-perspective bias**: Viewing problems through one lens
- **Cognitive blind spots**: Missing important considerations
- **Expertise gaps**: Lacking domain-specific knowledge
- **Emotional overload**: Making rushed or stressed decisions

MoE addresses these by:
- ✅ **Multiplying perspectives**: 5-10+ expert viewpoints on each decision
- ✅ **Filling knowledge gaps**: Domain experts provide specialized insights
- ✅ **Structured process**: Frameworks reduce cognitive load
- ✅ **Bias mitigation**: Multiple perspectives counterbalance individual biases
- ✅ **Confidence calibration**: Expert disagreement signals uncertainty

---

## Why Mixture of Experts for Decision-Making?

### The Problem with Traditional Decision-Making

Most people and organizations make decisions using one of these flawed approaches:

1. **Gut feel alone**: Fast but error-prone, especially under stress
2. **Analysis paralysis**: Endless research without action
3. **Committee approach**: Slow consensus-building with political dynamics
4. **Expert dependency**: Over-reliance on a single expert's view
5. **Framework rigidity**: Forcing every decision through the same process

### The MoE Solution

MoE provides a **dynamic, context-aware decision framework** that:

- **Adapts to decision complexity**: Simple choices use fewer experts; complex decisions activate comprehensive analysis
- **Balances speed and thoroughness**: Quick routing for urgent decisions, deep analysis for strategic ones
- **Combines analytical rigor with creativity**: Logical analysis AND innovative thinking
- **Accounts for human factors**: Emotional, ethical, and social dimensions
- **Learns from outcomes**: Feedback loops improve gating and expert recommendations

### Real-World Applications

| Domain | Decision Type | Expert Mix | Example |
|--------|--------------|------------|---------|
| **Business Strategy** | Market entry | Strategic Analyst + Risk Assessor + Financial Advisor + Market Researcher | Should we expand to Asia-Pacific? |
| **Product Development** | Feature prioritization | Product Manager + UX Designer + Technical Architect + Data Analyst | Which features for Q2 roadmap? |
| **Career** | Job change | Career Coach + Financial Planner + Life Goals Advisor + Risk Assessor | Accept the startup offer? |
| **Investment** | Portfolio allocation | Financial Advisor + Risk Manager + Market Analyst + Tax Strategist | Rebalance for retirement? |
| **Innovation** | R&D direction | Futurist + Technical Expert + Business Strategist + Creative Thinker | Which technology to invest in? |

---

## Decision-Making Architecture

### Three-Layer Architecture

```
┌─────────────────────────────────────────────────────────────┐
│                    INPUT LAYER                               │
│  • Decision context  • Constraints  • Goals  • Data         │
└─────────────────────────────────────────────────────────────┘
                            ↓
┌─────────────────────────────────────────────────────────────┐
│                   GATING LAYER                               │
│  Analyzes decision characteristics:                          │
│  • Complexity score  • Domain identification                 │
│  • Time urgency  • Stakeholder impact                        │
│  • Uncertainty level  • Resource constraints                 │
│                                                               │
│  Routes to appropriate experts with activation weights       │
└─────────────────────────────────────────────────────────────┘
                            ↓
┌─────────────────────────────────────────────────────────────┐
│                   EXPERT LAYER                               │
│  Specialized experts analyze from their perspective:         │
│                                                               │
│  ┌──────────┐ ┌──────────┐ ┌──────────┐ ┌──────────┐       │
│  │Strategic │ │Financial │ │Creative  │ │  Risk    │       │
│  │ Analyst  │ │ Advisor  │ │ Thinker  │ │ Assessor │       │
│  └──────────┘ └──────────┘ └──────────┘ └──────────┘       │
│                                                               │
│  ┌──────────┐ ┌──────────┐ ┌──────────┐ ┌──────────┐       │
│  │  Ethical │ │   Data   │ │  Systems │ │   User   │       │
│  │ Evaluator│ │ Scientist│ │ Thinker  │ │ Advocate │       │
│  └──────────┘ └──────────┘ └──────────┘ └──────────┘       │
│                                                               │
│  Each expert applies:                                        │
│  • Domain frameworks  • Mental models  • Bias checks         │
└─────────────────────────────────────────────────────────────┘
                            ↓
┌─────────────────────────────────────────────────────────────┐
│                 SYNTHESIS LAYER                              │
│  • Weighted aggregation of expert recommendations            │
│  • Conflict identification and resolution                    │
│  • Confidence scoring and uncertainty quantification         │
│  • Actionable decision package with rationale                │
└─────────────────────────────────────────────────────────────┘
                            ↓
┌─────────────────────────────────────────────────────────────┐
│                   OUTPUT LAYER                               │
│  Structured decision brief:                                  │
│  • Recommended action  • Supporting rationale                │
│  • Key considerations  • Risk mitigation strategies          │
│  • Dissenting views  • Implementation roadmap                │
│  • Success metrics  • Decision confidence score              │
└─────────────────────────────────────────────────────────────┘
```

### Decision Processing Phases

The MoE system processes decisions through structured phases (see [PHASES.md](PHASES.md)):

1. **Intake & Context Building** (Phase 0)
   - Gather decision parameters
   - Identify constraints and goals
   - Collect relevant data

2. **Problem Framing** (Phase 1)
   - Define the core question
   - Identify stakeholders
   - Establish success criteria

3. **Expert Routing** (Phase 2)
   - Analyze decision characteristics
   - Select relevant experts
   - Set activation weights

4. **Parallel Analysis** (Phase 3)
   - Each expert applies their frameworks
   - Independent analysis to avoid groupthink
   - Document reasoning and recommendations

5. **Synthesis & Integration** (Phase 4)
   - Aggregate expert insights
   - Identify consensus and conflicts
   - Generate holistic recommendation

6. **Decision Presentation** (Phase 5)
   - Structured decision brief
   - Implementation guidance
   - Risk mitigation plan

7. **Feedback & Learning** (Phase 6)
   - Track decision outcomes
   - Update expert models
   - Refine gating mechanism

---

## Key Features

### 🧠 **Cognitive Frameworks**
- **50+ Mental Models**: From first principles thinking to probabilistic reasoning (see [MENTAL_MODELS.md](research/MENTAL_MODELS.md))
- **Decision Frameworks**: WRAP, OODA Loop, Cynefin, Pre-Mortem, and more (see [DECISION_FRAMEWORKS.md](research/DECISION_FRAMEWORKS.md))
- **Problem-Solving Toolkits**: Issue trees, hypothesis-driven approaches, root cause analysis (see [PROBLEM_SOLVING.md](research/PROBLEM_SOLVING.md))

### 🎯 **Bias Mitigation**
- Comprehensive cognitive bias awareness (100+ biases catalogued)
- Structured debiasing techniques
- Diverse perspective integration
- See [COGNITIVE_BIASES.md](research/COGNITIVE_BIASES.md) for full analysis

### 👥 **Diverse Expert Personas**
- 15+ specialized expert roles with distinct cognitive profiles
- Dynamic expert selection based on decision context
- See [ROLES.md](ROLES.md) for complete expert descriptions

### ⚙️ **Flexible Architecture**
- Configurable expert networks
- Adaptive gating mechanisms
- Custom framework integration
- Neurodivergent-friendly design principles (see [NEURODIVERGENCY_GUIDANCE.md](research/NEURODIVERGENCY_GUIDANCE.md))

### 📊 **Decision Quality Metrics**
- Confidence scoring
- Uncertainty quantification
- Expert agreement/disagreement tracking
- Outcome feedback loops

---

## Documentation Index

### Core System Documents

- **[ROLES.md](ROLES.md)** - Detailed descriptions of all expert personas, their specializations, frameworks, and cognitive tools
- **[PHASES.md](PHASES.md)** - Complete decision processing lifecycle from intake to feedback
- **[COGNITIVE_TOOLS_MAPPING.md](COGNITIVE_TOOLS_MAPPING.md)** - Mapping of mental models, frameworks, and tools to expert roles

### Research & Framework Library

- **[MENTAL_MODELS.md](research/MENTAL_MODELS.md)** - Comprehensive collection of mental models for enhanced thinking
  - First Principles Thinking, Inversion, Second-Order Thinking, Probabilistic Thinking
  - Systems Thinking, Circle of Competence, Occam's Razor, and 40+ more
  - Quick reference guide included

- **[COGNITIVE_BIASES.md](research/COGNITIVE_BIASES.md)** - Deep analysis of cognitive biases in decision-making
  - 100+ biases categorized by type (perception, action, memory, social)
  - Impact on product development and business decisions
  - Mitigation strategies for each bias category
  - Quick reference guide for rapid consultation

- **[DECISION_FRAMEWORKS.md](research/DECISION_FRAMEWORKS.md)** - Proven decision-making methodologies
  - WRAP Framework (Widen, Reality-test, Attain distance, Prepare)
  - OODA Loop (Observe, Orient, Decide, Act)
  - Cynefin Framework for context assessment
  - Pre-Mortem and Prospective Hindsight
  - Multi-Criteria Decision Analysis (MCDA)
  - And 10+ additional frameworks

- **[PROBLEM_SOLVING.md](research/PROBLEM_SOLVING.md)** - Structured problem-solving approaches
  - Issue Trees and Logic Trees
  - Root Cause Analysis (5 Whys, Fishbone Diagrams)
  - Hypothesis-Driven Problem Solving
  - Design Thinking methodology
  - TRIZ (Theory of Inventive Problem Solving)

- **[NEURODIVERGENCY_GUIDANCE.md](research/NEURODIVERGENCY_GUIDANCE.md)** - Inclusive design principles
  - Accessibility considerations for ADHD, autism, dyslexia
  - Cognitive load management
  - Communication style adaptations
  - Sensory and executive function support

### Visual Framework Resources

Explore comprehensive visual frameworks in the **frameworks directory**:

- **[Cognitive Biases Codex](frameworks/README.md#cognitive-biases-codex)** - Complete visual mapping of 200+ cognitive biases
- **[Decision-Making Frameworks](frameworks/README.md#decision-making-frameworks)** - Visual guides for 12+ decision frameworks
- **[Mental Models Collection](frameworks/README.md#mental-models)** - Illustrated mental model library
- **[Product Development Frameworks](frameworks/README.md#product-development)** - Agile, Lean, Design Thinking visuals
- **[Strategy Frameworks](frameworks/README.md#strategy-frameworks)** - Business Model Canvas, SWOT, Porter's Five Forces

---

## Getting Started

### Installation

```bash
# Clone the repository
git clone https://github.com/Flying-Pig-Labs/mixture-of-experts.git
cd mixture-of-experts

# Install dependencies
pip install -r requirements.txt
```

### Quick Start: Your First Decision Analysis

```python
from moe import MixtureOfExperts, DecisionContext

# 1. Initialize the MoE system
moe = MixtureOfExperts(
    num_experts=8,
    gating_strategy="adaptive",
    enable_bias_checking=True
)

# 2. Define your decision context
decision = DecisionContext(
    question="Should we pivot our product from B2C to B2B?",
    constraints={
        "timeline": "3 months",
        "budget": "$500K",
        "team_size": 15
    },
    goals=[
        "Achieve profitability within 12 months",
        "Retain core team",
        "Maintain product quality"
    ],
    context={
        "current_mrr": 50000,
        "burn_rate": 150000,
        "runway_months": 8,
        "customer_segments": ["SMB", "Enterprise"],
        "market_conditions": "competitive"
    }
)

# 3. Process the decision
result = moe.analyze(decision)

# 4. Review the recommendation
print(f"Recommendation: {result.recommendation}")
print(f"Confidence: {result.confidence_score}/10")
print(f"\nKey Insights:")
for insight in result.key_insights:
    print(f"  • {insight}")

print(f"\nExpert Perspectives:")
for expert in result.expert_analyses:
    print(f"  [{expert.name}] {expert.recommendation} - {expert.rationale}")

print(f"\nRisks to Mitigate:")
for risk in result.identified_risks:
    print(f"  ⚠️  {risk.description}")
    print(f"     Mitigation: {risk.mitigation_strategy}")
```

**Output Example:**

```
Recommendation: Conditional Pivot - Pursue B2B with careful transition plan
Confidence: 7.5/10

Key Insights:
  • B2B market shows 3x higher LTV and 60% better retention
  • Current B2C customer base can provide transition revenue
  • Team lacks enterprise sales experience - critical gap
  • 8-month runway is tight but sufficient with careful execution

Expert Perspectives:
  [Strategic Analyst] Pivot to B2B - Market fundamentals favor enterprise
  [Financial Advisor] Cautious yes - Numbers work if execution timeline is met
  [Risk Assessor] Proceed with mitigation - Identify 3 fallback options
  [Product Manager] Staged transition - Maintain B2C during migration
  [Data Scientist] Support with caveats - Limited enterprise conversion data

Risks to Mitigate:
  ⚠️  Execution risk: Team lacks enterprise sales capability
     Mitigation: Hire 1 enterprise sales leader within 30 days; invest in training
  ⚠️  Revenue gap: 3-6 month lag in B2B sales cycles
     Mitigation: Maintain B2C marketing at 30% level; secure bridge financing
  ⚠️  Product-market fit: Unvalidated enterprise assumptions
     Mitigation: Run 10 enterprise pilots before full pivot; validate within 60 days
```

---

## Decision Frameworks

MoE integrates proven decision frameworks to enhance analysis quality. Here's how to apply them:

### WRAP Framework (Widen Options, Reality-test Assumptions, Attain Distance, Prepare to Be Wrong)

```python
from moe.frameworks import WRAPFramework

# Apply WRAP to a hiring decision
wrap = WRAPFramework()

decision = wrap.analyze(
    question="Which candidate should we hire for the VP Engineering role?",

    # W - Widen your options
    options=["Candidate A (internal)", "Candidate B (external)", "Delay and search more"],

    # R - Reality-test assumptions
    assumptions=[
        "Internal candidate will ramp faster",
        "External candidate brings needed expertise"
    ],
    tests=[
        "Trial project for both candidates",
        "Reference checks with 5+ former colleagues",
        "Technical deep-dive with engineering team"
    ],

    # A - Attain distance
    perspective_shifts=[
        "What would we recommend to a peer company?",
        "10/10/10 analysis: How will we feel in 10 days, 10 months, 10 years?"
    ],

    # P - Prepare to be wrong
    scenarios={
        "candidate_a_fails": "What if internal candidate can't scale leadership?",
        "candidate_b_cultural_misfit": "What if external candidate clashes with culture?",
        "both_decline": "What if neither accepts our offer?"
    }
)

print(wrap.recommendation)
```

### Cynefin Framework (Context Assessment)

```python
from moe.frameworks import CynefinFramework

# Classify decision complexity
cynefin = CynefinFramework()

context = cynefin.classify(
    situation="Our app is crashing for 20% of Android users on app startup",
    characteristics={
        "cause_effect_relationship": "unclear",
        "number_of_variables": "high",
        "predictability": "low",
        "expertise_available": "medium"
    }
)

# Output: "Complex" domain → Probe-Sense-Respond approach
# Use experiments and pattern detection rather than best practices

if context.domain == "Complex":
    approach = cynefin.get_approach(context)
    # Returns: Run A/B tests, gather user feedback, iterate rapidly
```

### Pre-Mortem Analysis

```python
from moe.frameworks import PreMortem

# Imagine the decision has failed - why?
premortem = PreMortem()

failure_scenarios = premortem.analyze(
    decision="Launch product in Japan market",
    assumptions=[
        "Japanese users want same features as US users",
        "Translation is sufficient for localization",
        "Our pricing model will work in Japan"
    ]
)

# Output: Identified failure modes
# - Cultural mismatch: Features don't align with local usage patterns
# - Regulatory compliance: Missed data privacy requirements
# - Market dynamics: Entrenched competitors with superior local networks
# - Internal execution: Insufficient local team to provide support
```

See [DECISION_FRAMEWORKS.md](research/DECISION_FRAMEWORKS.md) for 15+ additional frameworks.

---

## Cognitive Tools & Mental Models

### Mental Models Library

MoE experts leverage 50+ mental models. Here are some of the most powerful:

#### 1. First Principles Thinking
**Definition**: Break down complex problems to fundamental truths and rebuild from there.

**When to use**: Novel problems, innovation, challenging status quo

**Example**:
```
❌ Conventional: "Electric cars are expensive because batteries are expensive"
✅ First Principles: "What is the fundamental cost of energy storage?
   Can we rethink battery chemistry, manufacturing, or form factor?"

→ Led to Tesla's battery innovations and vertical integration
```

#### 2. Inversion
**Definition**: Approach problems backwards - instead of asking how to succeed, ask how to fail.

**When to use**: Risk identification, strategy validation, quality assurance

**Example**:
```
Question: "How do we build a great company culture?"
Inverted: "How would we destroy our culture?"

Answers:
- Hire fast without cultural screening → Insight: Invest in hiring process
- Ignore feedback and concerns → Insight: Create feedback mechanisms
- Overwork team without recognition → Insight: Build recognition programs
- Allow toxic behavior from high performers → Insight: Enforce standards equally
```

#### 3. Second-Order Thinking
**Definition**: Consider not just immediate consequences, but consequences of consequences.

**Example**:
```
Decision: Offer free shipping to increase sales

1st Order: Sales increase 20% ✅
2nd Order: Margins decrease, customers expect free shipping as default ⚠️
3rd Order: Unable to remove free shipping without backlash, competitive pressure on margins 🚫

Better approach: Conditional free shipping (minimum order value) or membership program
```

#### 4. Probabilistic Thinking
**Definition**: Estimate likelihood of different outcomes rather than binary yes/no thinking.

**Example**:
```python
from moe.mental_models import ProbabilisticThinking

# Evaluate product launch success
prob = ProbabilisticThinking()

outcome_distribution = prob.estimate(
    scenarios={
        "spectacular_success": {"probability": 0.05, "impact": 10},
        "moderate_success": {"probability": 0.30, "impact": 5},
        "break_even": {"probability": 0.40, "impact": 0},
        "moderate_failure": {"probability": 0.20, "impact": -3},
        "spectacular_failure": {"probability": 0.05, "impact": -8}
    }
)

# Expected value: 0.30*5 + 0.40*0 + 0.20*(-3) + 0.05*10 + 0.05*(-8) = 1.0
# Insight: Positive expected value, but high variance - consider risk tolerance
```

#### 5. Circle of Competence
**Definition**: Understand the boundaries of your knowledge and operate within them, or expand them deliberately.

**Application in MoE**: Gating mechanism routes decisions to experts within their circle of competence.

```python
# Expert self-assessment
expert.evaluate_competence(
    question="Should we use Kubernetes or serverless for our microservices?"
)

# If outside circle of competence → defer to appropriate expert or flag knowledge gap
```

See [MENTAL_MODELS.md](research/MENTAL_MODELS.md) for the complete collection of 50+ models with detailed examples.

---

## Expert Specializations

MoE includes diverse expert personas, each with specialized frameworks and cognitive tools:

### Strategic Analyst
- **Focus**: Long-term thinking, competitive dynamics, market forces
- **Frameworks**: SWOT, Porter's Five Forces, Blue Ocean Strategy, Scenario Planning
- **Mental Models**: Second-order thinking, Game theory, Network effects
- **Best for**: Market entry, competitive strategy, business model decisions

### Financial Advisor
- **Focus**: Economic viability, resource allocation, ROI analysis
- **Frameworks**: NPV/IRR, Break-even analysis, Real Options Valuation
- **Mental Models**: Opportunity cost, Time value of money, Risk-adjusted returns
- **Best for**: Investment decisions, pricing strategy, resource prioritization

### Risk Assessor
- **Focus**: Threat identification, mitigation planning, resilience
- **Frameworks**: Risk matrix, FMEA (Failure Mode Effects Analysis), Pre-mortem
- **Mental Models**: Inversion, Probabilistic thinking, Redundancy
- **Best for**: High-stakes decisions, crisis management, contingency planning

### Creative Thinker
- **Focus**: Innovation, ideation, unconventional solutions
- **Frameworks**: Design Thinking, SCAMPER, Lateral Thinking
- **Mental Models**: First principles, Analogical thinking, Constraint removal
- **Best for**: Product innovation, problem reframing, breakthrough thinking

### Data Scientist
- **Focus**: Evidence-based analysis, statistical reasoning, pattern recognition
- **Frameworks**: A/B testing, Bayesian inference, Regression analysis
- **Mental Models**: Correlation vs causation, Statistical significance, Base rates
- **Best for**: Data-driven decisions, experiment design, metric selection

### Ethical Evaluator
- **Focus**: Values alignment, stakeholder impact, moral considerations
- **Frameworks**: Stakeholder analysis, Ethics frameworks (Utilitarian, Deontological)
- **Mental Models**: Veil of ignorance, Moral principles, Unintended consequences
- **Best for**: Socially impactful decisions, policy choices, brand reputation

### Systems Thinker
- **Focus**: Interconnections, feedback loops, emergent properties
- **Frameworks**: Causal loop diagrams, Stock and flow models, Systems archetypes
- **Mental Models**: Leverage points, Feedback loops, Non-linear dynamics
- **Best for**: Complex organizational changes, ecosystem strategy, scaling decisions

### UX Advocate / User Researcher
- **Focus**: User needs, behavioral insights, experience quality
- **Frameworks**: Jobs-to-be-Done, User journey mapping, Usability heuristics
- **Mental Models**: Empathy mapping, Cognitive load, User mental models
- **Best for**: Product decisions, feature prioritization, design choices

See [ROLES.md](ROLES.md) for complete expert descriptions including additional personas like Product Manager, Technical Architect, Change Management Specialist, and more.

---

## Usage Examples

### Example 1: Career Decision

```python
from moe import MixtureOfExperts, DecisionContext

moe = MixtureOfExperts()

career_decision = DecisionContext(
    question="Should I leave my stable corporate job to join an early-stage startup?",

    constraints={
        "family_obligations": "2 kids, mortgage",
        "savings": "6 months runway",
        "location": "Must stay in current city"
    },

    goals=[
        "Learn new skills",
        "Higher upside potential",
        "More autonomy and impact",
        "Maintain financial security"
    ],

    context={
        "current_comp": 180000,
        "startup_offer": {"base": 130000, "equity": "0.5%"},
        "current_role": "Senior Manager, 5 years",
        "startup_stage": "Series A, 2M ARR",
        "risk_tolerance": "moderate"
    }
)

result = moe.analyze(career_decision)
```

**Key Expert Insights:**

- **Career Coach**: "Growth opportunity is significant, but timing is important given family situation"
- **Financial Advisor**: "Compensation cut is manageable with 6-month runway, but negotiate better equity"
- **Risk Assessor**: "Series A is high risk - 60% fail before Series B. Ensure you have fallback plan"
- **Life Goals Advisor**: "Autonomy and impact align with stated values, but validate cultural fit first"

**Recommendation**: "Conditional Yes - Accept if: (1) Equity increases to 0.8-1%, (2) Trial project validates fit, (3) Spouse/partner is aligned"

---

### Example 2: Product Feature Prioritization

```python
features = [
    {"name": "Advanced analytics dashboard", "effort": 8, "impact": 6},
    {"name": "Mobile app", "effort": 13, "impact": 9},
    {"name": "API for integrations", "effort": 5, "impact": 7},
    {"name": "Improved onboarding", "effort": 3, "impact": 8},
    {"name": "AI-powered recommendations", "effort": 10, "impact": 7}
]

prioritization = moe.prioritize(
    items=features,
    criteria=["user_value", "business_impact", "technical_feasibility", "strategic_fit"],
    constraints={"team_capacity": "20 story points", "timeline": "Q2 2025"}
)

# Output:
# Priority 1: Improved onboarding (High impact, low effort - quick win)
# Priority 2: API for integrations (Enables ecosystem, moderate effort)
# Priority 3: Mobile app (High strategic value, defer to Q3 given effort)
```

---

### Example 3: Crisis Response

```python
crisis = DecisionContext(
    situation="Security breach: Customer data exposed for 5,000 users",

    immediate_context={
        "breach_detected": "2 hours ago",
        "data_exposed": ["emails", "names", "hashed_passwords"],
        "vulnerability": "SQL injection, now patched",
        "attacker_profile": "unknown",
        "media_awareness": "not yet public"
    },

    decision="What actions should we take in the next 24 hours?"
)

crisis_response = moe.analyze_urgent(crisis, time_limit="15_minutes")

# Urgent mode: Activates Crisis Management, Legal, Communications, Technical Security experts
# Returns: Immediate action checklist, communication templates, stakeholder notification plan
```

**Immediate Actions (first 4 hours):**
1. Notify affected users via email (Legal + Communications template)
2. Prepare public statement (Communications expert)
3. Engage security audit firm (Technical Security)
4. Notify legal counsel and prepare regulatory filings (Legal)
5. CEO communication to team (Leadership)

---

### Example 4: Investment Decision with Uncertainty

```python
investment = DecisionContext(
    question="Should we invest $2M in AI/ML capabilities now or wait 6 months?",

    context={
        "current_state": "Rule-based systems, manual processes",
        "market_pressure": "Competitors launching AI features",
        "team_readiness": "Limited ML expertise",
        "budget_available": 2000000,
        "expected_benefits": "30% efficiency gain, new revenue streams"
    },

    uncertainty_factors=[
        "AI technology evolution pace",
        "Regulatory landscape for AI",
        "Availability of ML talent",
        "Customer adoption of AI features"
    ]
)

result = moe.analyze_with_uncertainty(investment)

# Applies Real Options analysis
# Recommendation: "Invest $500K now in exploration + hiring, preserve option to scale in 6 months"
# Rationale: "High uncertainty warrants staged investment; maintain strategic optionality"
```

---

## Advanced Topics

### Custom Expert Creation

Create domain-specific experts for your unique needs:

```python
from moe import Expert, Framework

# Define a custom "Sustainability Expert"
sustainability_expert = Expert(
    name="Sustainability Advisor",

    expertise_areas=[
        "Environmental impact",
        "ESG compliance",
        "Circular economy",
        "Carbon accounting"
    ],

    frameworks=[
        Framework("Life Cycle Assessment"),
        Framework("Triple Bottom Line"),
        Framework("Cradle-to-Cradle Design")
    ],

    mental_models=[
        "Systems thinking",
        "Long-term thinking",
        "Externality analysis"
    ],

    decision_criteria=[
        "Environmental impact",
        "Resource efficiency",
        "Stakeholder value",
        "Regulatory compliance"
    ]
)

# Add to your MoE instance
moe.add_expert(sustainability_expert)
```

### Gating Strategy Customization

Tune how decisions route to experts:

```python
from moe import AdaptiveGating

gating = AdaptiveGating(
    # High-complexity decisions activate more experts
    complexity_threshold={
        "simple": 2,      # 2-3 experts
        "moderate": 5,    # 5-6 experts
        "complex": 8,     # 8-10 experts
        "critical": 12    # All available experts
    },

    # Domain detection for expert selection
    domain_keywords={
        "financial": ["revenue", "cost", "ROI", "budget", "pricing"],
        "technical": ["architecture", "scalability", "infrastructure"],
        "user_focused": ["UX", "customer", "user experience", "adoption"]
    },

    # Urgency affects depth of analysis
    urgency_modifiers={
        "immediate": 0.3,   # 30% of normal analysis depth
        "standard": 1.0,    # Full analysis
        "strategic": 1.5    # 50% deeper analysis
    }
)

moe.set_gating_strategy(gating)
```

### Bias Detection & Mitigation

Activate bias checking for higher-quality decisions:

```python
from moe import BiasDetection

bias_checker = BiasDetection(
    # Common biases to check for
    enabled_checks=[
        "confirmation_bias",        # Seeking confirming evidence only
        "anchoring",                # Over-relying on first information
        "availability_heuristic",   # Overweighting recent/memorable data
        "sunk_cost_fallacy",        # Continuing due to past investment
        "groupthink",               # Pressure for consensus
        "recency_bias",             # Overweighting recent events
        "optimism_bias",            # Unrealistic positive expectations
        "planning_fallacy"          # Underestimating time/costs
    ],

    # Mitigation strategies
    auto_mitigation=True,  # Automatically apply debiasing techniques

    strategies={
        "confirmation_bias": "Actively seek disconfirming evidence",
        "anchoring": "Consider multiple reference points",
        "sunk_cost": "Focus on forward-looking value, ignore past costs"
    }
)

moe.enable_bias_detection(bias_checker)
```

### Outcome Tracking & Learning

Improve decision quality over time:

```python
# Record decision
decision_id = moe.analyze(decision_context)

# Track outcome after implementation
moe.record_outcome(
    decision_id=decision_id,

    actual_result={
        "metric": "revenue_growth",
        "predicted": 0.25,      # Predicted 25% growth
        "actual": 0.18,         # Actual 18% growth
        "variance": -0.07
    },

    lessons_learned=[
        "Market adoption slower than expected",
        "Implementation timeline was accurate",
        "Risk mitigation strategies were effective"
    ],

    expert_accuracy={
        "Strategic Analyst": 0.85,   # 85% accurate prediction
        "Financial Advisor": 0.72,
        "Market Researcher": 0.65
    }
)

# System learns: Adjust expert weights, refine gating, update models
```

---

## Research Foundation

This framework synthesizes insights from multiple disciplines:

### Decision Science
- Bounded rationality (Herbert Simon)
- Prospect theory (Kahneman & Tversky)
- Recognition-primed decision making (Gary Klein)
- Naturalistic decision making research

### Cognitive Psychology
- Dual-process theory (System 1 & System 2 thinking)
- Cognitive biases and heuristics
- Mental models and analogical reasoning
- Expertise development (Ericsson)

### Organizational Behavior
- Group decision-making dynamics
- Diversity and decision quality
- Organizational learning
- Knowledge management

### Machine Learning & AI
- Mixture of Experts neural architectures (Jacobs et al., 1991)
- Ensemble methods and model aggregation
- Transfer learning and domain adaptation
- Explainable AI and interpretability

### Strategic Management
- Strategic decision-making under uncertainty
- Real options theory
- Scenario planning methodologies
- Competitive dynamics

### Key Research Papers

1. **Jacobs, R. A., et al. (1991)**. "Adaptive mixtures of local experts." *Neural Computation*, 3(1), 79-87.
   - Foundational MoE architecture

2. **Kahneman, D., Lovallo, D., & Sibony, O. (2011)**. "Before you make that big decision." *Harvard Business Review*, 89(6), 50-60.
   - Quality decision-making process

3. **Heath, C., & Heath, D. (2013)**. *Decisive: How to make better choices in life and work.* Crown Business.
   - WRAP framework

4. **Snowden, D. J., & Boone, M. E. (2007)**. "A leader's framework for decision making." *Harvard Business Review*, 85(11), 68.
   - Cynefin framework

5. **Klein, G. (2008)**. "Naturalistic decision making." *Human Factors*, 50(3), 456-460.
   - Expert intuition and recognition-primed decisions

See [DECISION_FRAMEWORKS.md](research/DECISION_FRAMEWORKS.md) for comprehensive bibliography.

---

## Contributing

We welcome contributions! Areas where we especially need help:

### Research Contributions
- Additional mental models and frameworks
- Cognitive bias mitigation techniques
- Case studies and decision outcome data
- Academic research integration

### Code Contributions
- New expert personas and specializations
- Gating algorithm improvements
- Framework implementations
- Visualization tools

### Documentation
- Usage examples and case studies
- Framework guides and tutorials
- Translation to other languages
- Accessibility improvements

**How to contribute:**

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/new-expert-persona`)
3. Make your changes with clear documentation
4. Add tests if applicable
5. Submit a pull request with detailed description

See [CONTRIBUTING.md](CONTRIBUTING.md) for detailed guidelines.

---

## Project Structure

```text
mixture-of-experts/
├── README.md                          # This file
├── requirements.txt                   # Python dependencies
├── setup.py                          # Package setup
│
├── src/                              # Source code
│   ├── __init__.py
│   ├── moe/                         # Core MoE system
│   │   ├── experts/                 # Expert implementations
│   │   ├── gating/                  # Gating mechanisms
│   │   ├── synthesis/               # Aggregation logic
│   │   └── frameworks/              # Decision framework implementations
│   ├── models/                      # Data models
│   ├── utils/                       # Utilities
│   └── config/                      # Configuration
│
├── research/                         # Research documents
│   ├── MENTAL_MODELS.md
│   ├── COGNITIVE_BIASES.md
│   ├── DECISION_FRAMEWORKS.md
│   ├── PROBLEM_SOLVING.md
│   └── NEURODIVERGENCY_GUIDANCE.md
│
├── frameworks/                       # Visual frameworks & images
│   ├── README.md
│   ├── cognitive-biases/
│   ├── decision-frameworks/
│   ├── mental-models/
│   └── strategy/
│
├── docs/                            # Core documentation
│   ├── ROLES.md
│   ├── PHASES.md
│   └── COGNITIVE_TOOLS_MAPPING.md
│
├── examples/                        # Usage examples
│   ├── career_decision.py
│   ├── product_prioritization.py
│   ├── business_strategy.py
│   └── crisis_response.py
│
├── tests/                           # Test suite
│   ├── unit/
│   ├── integration/
│   └── fixtures/
│
└── notebooks/                       # Jupyter notebooks
    ├── getting_started.ipynb
    ├── custom_experts.ipynb
    └── case_studies.ipynb
```

---

## License

This project is licensed under the **MIT License** - see the [LICENSE](LICENSE) file for details.

---

## Acknowledgments

### Inspiration & Research

- **Daniel Kahneman** - Prospect theory and cognitive biases
- **Chip Heath & Dan Heath** - WRAP framework and decision-making research
- **Shane Parrish & Farnam Street** - Mental models compendium
- **Gary Klein** - Naturalistic decision making
- **Dave Snowden** - Cynefin framework
- **Herbert Simon** - Bounded rationality
- **Annie Duke** - Thinking in bets and decision quality

### Technical Foundations

- Mixture of Experts neural architecture research (Jacobs et al., Shazeer et al.)
- Ensemble learning and model aggregation methods
- Multi-agent systems and distributed AI

### Community

- Contributors to cognitive bias research and cataloging
- Open-source decision framework implementations
- Product management and UX research communities
- Neurodivergent accessibility advocates

---

## Contact & Support

- **Issues & Bug Reports**: [GitHub Issues](https://github.com/Flying-Pig-Labs/mixture-of-experts/issues)
- **Discussions & Questions**: [GitHub Discussions](https://github.com/Flying-Pig-Labs/mixture-of-experts/discussions)
- **Documentation**: [Project Wiki](https://github.com/Flying-Pig-Labs/mixture-of-experts/wiki)

---

## Roadmap

### Current Version: 0.1.0 (Foundation)
- ✅ Core expert personas defined
- ✅ Research framework library
- ✅ Basic gating mechanism
- ✅ Decision context modeling

### Version 0.2.0 (Q2 2025)
- [ ] Advanced bias detection
- [ ] Custom expert builder UI
- [ ] Outcome tracking system
- [ ] Interactive decision workbench

### Version 0.3.0 (Q3 2025)
- [ ] Machine learning-enhanced gating
- [ ] Expert ensemble optimization
- [ ] Real-time collaboration features
- [ ] Mobile application

### Version 1.0.0 (Q4 2025)
- [ ] Production-ready API
- [ ] Enterprise integrations
- [ ] Advanced analytics dashboard
- [ ] Community expert marketplace

---

## Quick Links

- 📚 **[Full Documentation](docs/)**
- 🧠 **[Mental Models Library](research/MENTAL_MODELS.md)**
- ⚖️ **[Decision Frameworks](research/DECISION_FRAMEWORKS.md)**
- 🎯 **[Cognitive Biases Guide](research/COGNITIVE_BIASES.md)**
- 👥 **[Expert Roles](ROLES.md)**
- 🔄 **[Decision Phases](PHASES.md)**
- 🖼️ **[Visual Frameworks](frameworks/README.md)**

---

**Make better decisions. Think from multiple perspectives. Navigate complexity with confidence.**

*Built with ❤️ by the Flying Pig Labs team*
