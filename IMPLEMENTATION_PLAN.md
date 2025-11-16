# MoE Decision Framework: Implementation Plan

> **A stateful CLI with MCP backend for interactive decision-making using mental models and frameworks**

## Executive Summary

This plan outlines the implementation of a Mixture of Experts (MoE) decision framework as a **CLI tool** with an **MCP (Model Context Protocol) server** backend. The system enables users to:

1. **Get suggestions** for which mental models/frameworks apply to their problem
2. **Interactive Q&A** to gather context and apply a chosen framework
3. **Direct application** of specific frameworks with guided questions

The architecture separates concerns cleanly:
- **CLI**: Stateful session management, user interaction, formatting
- **MCP Server**: Framework routing, question generation, decision synthesis
- **Model Registry**: Structured library of mental models with metadata

---

## Table of Contents

1. [Architecture Overview](#architecture-overview)
2. [Core Components](#core-components)
3. [MCP Server Design](#mcp-server-design)
4. [CLI Design](#cli-design)
5. [Mental Model Registry Schema](#mental-model-registry-schema)
6. [User Flows (Three Scenarios)](#user-flows-three-scenarios)
7. [Implementation Phases](#implementation-phases)
8. [Technical Stack](#technical-stack)
9. [File Structure](#file-structure)
10. [Success Metrics](#success-metrics)

---

## Architecture Overview

### Four-Layer Architecture

```
┌─────────────────────────────────────────────────────────────────┐
│                         CLI Layer                                │
│  • Command parsing & routing                                     │
│  • Session state management (~/.moe/sessions/)                   │
│  • User interaction (prompts, Q&A loops)                         │
│  • Output formatting (markdown, tables, reports)                 │
└─────────────────────────────────────────────────────────────────┘
                              ↓ MCP Protocol
┌─────────────────────────────────────────────────────────────────┐
│                      MCP Server Layer                            │
│  Tools:                                                          │
│  • suggest_models(problem_description) → model suggestions       │
│  • generate_questions(model_id, problem, known_answers)          │
│  • apply_model(model_id, problem, answers) → decision report     │
│  • validate_inputs(model_id, answers) → missing fields           │
└─────────────────────────────────────────────────────────────────┘
                              ↓
┌─────────────────────────────────────────────────────────────────┐
│                   Mental Model Registry                          │
│  Structured YAML/JSON library:                                   │
│  • Model metadata (id, name, description, tags)                  │
│  • Required/optional inputs with prompts                         │
│  • Application templates and examples                            │
│  • LLM prompt templates for synthesis                            │
└─────────────────────────────────────────────────────────────────┘
                              ↓
┌─────────────────────────────────────────────────────────────────┐
│                         LLM Layer                                │
│  • Claude/GPT for intelligent routing                            │
│  • Prompt templates for each framework                           │
│  • Structured output generation                                  │
└─────────────────────────────────────────────────────────────────┘
```

### Design Principles

1. **Deterministic when possible**: Model selection and question generation are rule-based; only synthesis uses LLM
2. **Stateful CLI, stateless MCP**: CLI manages sessions locally; MCP server is purely functional
3. **Progressive disclosure**: Start simple (suggestions), go deeper (Q&A), or jump direct (specific model)
4. **Explicit missing info**: Never vague "tell me more" — always specific questions needed
5. **Idempotent operations**: Same inputs → same outputs for reproducibility

---

## Core Components

### 1. CLI Application (`moe`)

**Technology**: Python (Click/Typer) or Go (Cobra)

**Responsibilities**:
- Parse commands and route to appropriate handlers
- Manage local session state in `~/.moe/sessions/*.json`
- Call MCP server tools via MCP protocol
- Handle interactive Q&A loops
- Format and display outputs

**Key Features**:
- Session persistence across commands
- Rich terminal UI (colors, tables, markdown rendering)
- Interactive and non-interactive modes
- Configuration management (`~/.moe/config.yaml`)

### 2. MCP Server (`moe-server`)

**Technology**: Python (FastMCP) or TypeScript (MCP SDK)

**Responsibilities**:
- Expose MCP tools for model operations
- Load and query mental model registry
- Generate LLM prompts for synthesis
- Return structured responses

**Key Features**:
- Stateless operation (no session management)
- Fast response times (<2s for suggestions)
- Structured output schemas
- Error handling with actionable messages

### 3. Mental Model Registry

**Technology**: YAML files with JSON Schema validation

**Responsibilities**:
- Store mental model definitions
- Define required/optional inputs
- Provide prompt templates
- Include examples and best practices

**Key Features**:
- Human-readable and editable
- Version controlled
- Extensible (users can add custom models)
- Tagged for categorization

### 4. LLM Integration

**Technology**: Anthropic Claude API (primary), OpenAI compatible (fallback)

**Responsibilities**:
- Rank/filter models for problem descriptions
- Generate contextual questions
- Apply frameworks to user inputs
- Synthesize decision reports

**Key Features**:
- Prompt caching for efficiency
- Structured outputs (JSON mode)
- Temperature control per use case
- Token usage tracking

---

## MCP Server Design

### MCP Tools

#### 1. `suggest_models`

**Purpose**: Analyze a problem and suggest relevant mental models/frameworks

**Input Schema**:
```json
{
  "problem_description": "string (required)",
  "tags": ["array of strings (optional)"],
  "constraints": {
    "time_available": "string (optional)",
    "complexity_preference": "simple|moderate|complex (optional)"
  },
  "context": {
    "domain": "business|personal|technical|etc (optional)",
    "decision_type": "strategic|tactical|operational (optional)"
  }
}
```

**Output Schema**:
```json
{
  "status": "success",
  "suggestions": [
    {
      "model_id": "inversion",
      "name": "Inversion",
      "relevance_score": 0.92,
      "reason": "Problem involves risk identification and failure mode analysis",
      "best_for": ["risk assessment", "strategy validation"],
      "estimated_time": "15-30 minutes",
      "complexity": "moderate"
    },
    {
      "model_id": "weighted_decision_matrix",
      "name": "Weighted Decision Matrix",
      "relevance_score": 0.85,
      "reason": "Multiple options with quantifiable criteria",
      "best_for": ["multi-criteria decisions", "vendor selection"],
      "estimated_time": "20-40 minutes",
      "complexity": "simple"
    }
  ],
  "suggested_combinations": [
    {
      "models": ["pre_mortem", "inversion"],
      "reason": "Complementary risk analysis approaches"
    }
  ],
  "next_action": "user_selects_model"
}
```

**Implementation**:
1. Load model registry
2. Use LLM to analyze problem description
3. Match against model metadata (tags, best_for, descriptions)
4. Rank by relevance
5. Return top 3-5 suggestions

---

#### 2. `generate_questions`

**Purpose**: Generate questions needed to apply a specific model

**Input Schema**:
```json
{
  "model_id": "string (required)",
  "problem_description": "string (required)",
  "known_answers": {
    "key": "value"
  }
}
```

**Output Schema**:
```json
{
  "status": "success",
  "model_id": "weighted_decision_matrix",
  "model_name": "Weighted Decision Matrix",
  "questions": [
    {
      "id": "options",
      "prompt": "List all the options you're deciding between (comma-separated):",
      "type": "list",
      "required": true,
      "example": "Vendor A, Vendor B, Vendor C",
      "validation": {
        "min_items": 2,
        "max_items": 10
      }
    },
    {
      "id": "criteria",
      "prompt": "What criteria matter most for this decision? (e.g., cost, reliability, speed)",
      "type": "list",
      "required": true,
      "example": "Cost, Reliability, Integration complexity",
      "follow_up": "criteria_weights"
    },
    {
      "id": "criteria_weights",
      "prompt": "How would you weight these criteria? (0-1, must sum to 1)",
      "type": "weights",
      "required": true,
      "depends_on": "criteria",
      "example": "Cost=0.3, Reliability=0.4, Integration=0.3",
      "validation": {
        "sum_to": 1.0,
        "all_positive": true
      }
    }
  ],
  "optional_questions": [
    {
      "id": "constraints",
      "prompt": "Any hard constraints that would disqualify an option?",
      "type": "text",
      "required": false,
      "helps_with": "Filtering options before scoring"
    }
  ],
  "estimated_time": "20 minutes",
  "next_action": "collect_answers"
}
```

**Implementation**:
1. Load model definition from registry
2. Check `known_answers` against required inputs
3. Filter out already-answered questions
4. Use LLM to contextualize question prompts to the specific problem
5. Return ordered list of remaining questions

---

#### 3. `apply_model`

**Purpose**: Apply a mental model to generate decision analysis and recommendations

**Input Schema**:
```json
{
  "model_id": "string (required)",
  "problem_description": "string (required)",
  "answers": {
    "question_id": "answer_value"
  },
  "options": {
    "detail_level": "concise|standard|comprehensive (default: standard)",
    "include_examples": "boolean (default: false)",
    "format": "text|markdown|json (default: markdown)"
  }
}
```

**Output Schema**:
```json
{
  "status": "success",
  "model_applied": "weighted_decision_matrix",
  "timestamp": "2025-11-16T10:30:00Z",

  "executive_summary": {
    "recommendation": "Vendor B is the recommended choice",
    "confidence": 0.82,
    "key_insight": "Vendor B scores highest on weighted criteria (8.2/10) with strong reliability and acceptable cost"
  },

  "analysis": {
    "framework_steps": [
      {
        "step": 1,
        "title": "Define Options",
        "content": "Three vendors evaluated: Vendor A, Vendor B, Vendor C"
      },
      {
        "step": 2,
        "title": "Establish Criteria and Weights",
        "content": "Cost (30%), Reliability (40%), Integration complexity (30%)"
      },
      {
        "step": 3,
        "title": "Score Options",
        "content": "Each vendor scored 1-10 on each criterion...",
        "data": {
          "Vendor A": {"Cost": 9, "Reliability": 6, "Integration": 7},
          "Vendor B": {"Cost": 7, "Reliability": 9, "Integration": 9},
          "Vendor C": {"Cost": 8, "Reliability": 7, "Integration": 5}
        }
      },
      {
        "step": 4,
        "title": "Calculate Weighted Scores",
        "content": "Vendor A: 7.3, Vendor B: 8.2, Vendor C: 6.7"
      }
    ],

    "decision_matrix": {
      "headers": ["Option", "Cost (30%)", "Reliability (40%)", "Integration (30%)", "Total"],
      "rows": [
        ["Vendor A", "9.0 (2.7)", "6.0 (2.4)", "7.0 (2.1)", "7.3"],
        ["Vendor B", "7.0 (2.1)", "9.0 (3.6)", "9.0 (2.7)", "8.2 ⭐"],
        ["Vendor C", "8.0 (2.4)", "7.0 (2.8)", "5.0 (1.5)", "6.7"]
      ]
    }
  },

  "insights": [
    "Vendor B leads by 0.9 points - statistically significant margin",
    "Reliability is the deciding factor (highest weighted criterion)",
    "Cost difference is minimal when weighted (0.6 points range)",
    "Integration complexity strongly favors Vendor B (4-point gap vs Vendor C)"
  ],

  "caveats": [
    "Scores are subjective - consider running scoring workshop with team",
    "Weight distribution is fairly balanced - sensitivity analysis recommended",
    "Vendor A nearly tied if cost is weighted higher (>45%)"
  ],

  "next_steps": [
    "Validate reliability scores with reference checks",
    "Request detailed integration documentation from Vendor B",
    "Perform sensitivity analysis on criteria weights",
    "Schedule proof-of-concept with Vendor B"
  ],

  "decision_quality_score": 0.78,
  "reasoning_transparency": "high",
  "bias_checks": [
    "Confirmation bias: Are we seeking data that confirms Vendor B preference?",
    "Anchoring: Did initial impressions bias scoring?"
  ]
}
```

**Implementation**:
1. Validate all required inputs are provided
2. Load model-specific prompt template
3. Generate LLM prompt with problem + answers + framework template
4. Parse structured output
5. Add bias checks and quality scoring
6. Return comprehensive report

---

#### 4. `validate_inputs`

**Purpose**: Check if provided answers satisfy model requirements

**Input Schema**:
```json
{
  "model_id": "string (required)",
  "answers": {
    "question_id": "answer_value"
  }
}
```

**Output Schema**:
```json
{
  "status": "valid|incomplete|invalid",
  "missing_required": [
    {
      "id": "criteria_weights",
      "prompt": "How would you weight these criteria?",
      "reason": "Required for weighted scoring calculation"
    }
  ],
  "validation_errors": [
    {
      "field": "criteria_weights",
      "error": "Weights must sum to 1.0 (current sum: 0.85)",
      "suggestion": "Adjust weights or distribute remaining 0.15"
    }
  ],
  "ready_to_apply": false
}
```

---

### MCP Server Configuration

**Server Manifest** (`moe-server/mcp.json`):
```json
{
  "name": "moe-decision-server",
  "version": "0.1.0",
  "description": "Mixture of Experts decision-making framework server",
  "tools": [
    {
      "name": "suggest_models",
      "description": "Analyze a problem and suggest relevant mental models/frameworks",
      "inputSchema": { ... }
    },
    {
      "name": "generate_questions",
      "description": "Generate questions needed to apply a specific mental model",
      "inputSchema": { ... }
    },
    {
      "name": "apply_model",
      "description": "Apply a mental model to generate decision analysis",
      "inputSchema": { ... }
    },
    {
      "name": "validate_inputs",
      "description": "Validate if answers satisfy model requirements",
      "inputSchema": { ... }
    }
  ]
}
```

---

## CLI Design

### Command Structure

```bash
moe [command] [subcommand] [arguments] [flags]
```

### Core Commands

#### 1. `moe decide <problem>`

**Purpose**: Start a new decision session (Scenario A & B)

**Behavior**:
1. Create new session with UUID
2. Call `suggest_models` with problem description
3. Display suggestions
4. Prompt user to select a model or exit

**Examples**:
```bash
# Basic usage
moe decide "Should we migrate to microservices architecture?"

# With context flags
moe decide "Choose pricing strategy for SaaS product" \
  --domain business \
  --time-available 1h \
  --complexity moderate

# Non-interactive (just suggestions)
moe decide "Hire candidate A or B?" --suggest-only
```

**Output**:
```
🧠 Decision Session: session-abc123

Analyzing your problem...

📋 Suggested Mental Models:

1. ⭐ Inversion (Relevance: 92%)
   → Think about what to avoid / how to fail
   → Best for: risk assessment, strategy validation
   → Time: 15-30 minutes

2. 📊 Weighted Decision Matrix (Relevance: 85%)
   → Multi-criteria scoring framework
   → Best for: comparing multiple options
   → Time: 20-40 minutes

3. 🔮 Pre-Mortem (Relevance: 78%)
   → Imagine the decision failed - why?
   → Best for: identifying risks before commitment
   → Time: 20 minutes

💡 Suggested combination: Pre-Mortem + Inversion for thorough risk analysis

Next steps:
  • Run: moe use session-abc123 <model-id>
  • Or: moe show session-abc123
  • Or: moe list
```

---

#### 2. `moe use <session-id> <model-id>`

**Purpose**: Select a model and start Q&A (Scenario B)

**Behavior**:
1. Load session
2. Call `generate_questions` for selected model
3. Store questions in session
4. Enter interactive Q&A or display questions

**Examples**:
```bash
# Interactive mode
moe use session-abc123 inversion

# Non-interactive (show questions)
moe use session-abc123 inversion --show-questions
```

**Interactive Output**:
```
🎯 Applying: Inversion

This framework helps you think backwards - instead of "how to succeed",
ask "how to fail" to identify risks and pitfalls.

I need to ask you 3 questions:

❓ Question 1 of 3

What is the primary outcome you're aiming for?

Example: "Launch product successfully in Q2 with >1000 users"

Your answer: _
```

---

#### 3. `moe answer <session-id>`

**Purpose**: Answer questions (interactive or bulk)

**Behavior**:
1. Load session and pending questions
2. Collect answers (interactive loop or from stdin)
3. Validate inputs
4. Store in session
5. Check if ready to apply model

**Examples**:
```bash
# Interactive
moe answer session-abc123

# Bulk (from file or heredoc)
moe answer session-abc123 <<EOF
goal: Launch product successfully in Q2 with >1000 users
failure_modes: Poor UX, technical bugs, market timing
constraints: 3 month timeline, 5-person team
EOF

# Single answer
moe answer session-abc123 --field goal --value "Increase revenue 30%"
```

---

#### 4. `moe apply <session-id>`

**Purpose**: Apply the model and generate decision report (Turn 3)

**Behavior**:
1. Load session with answers
2. Call `validate_inputs` to check completeness
3. If valid, call `apply_model`
4. Display formatted report
5. Save report to session
6. Mark session as completed

**Examples**:
```bash
# Standard report
moe apply session-abc123

# Detailed report
moe apply session-abc123 --detail comprehensive

# Export formats
moe apply session-abc123 --format json > report.json
moe apply session-abc123 --format pdf > report.pdf
```

**Output**:
```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
🎯 Decision Analysis Report
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Framework: Inversion
Problem: Should we migrate to microservices?
Date: 2025-11-16

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
📊 EXECUTIVE SUMMARY
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Recommendation: Conditional NO - delay migration for 6 months

Confidence: 78%

Key Insight: Inverting the question ("How to make this migration fail")
reveals 8 critical failure modes, 5 of which currently lack mitigation.
Current organizational readiness is insufficient for success.

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
🔍 INVERSION ANALYSIS
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Question: "How would this migration fail catastrophically?"

Failure Modes Identified:

1. ⚠️  Skill Gap Failure
   → Team lacks distributed systems expertise
   → Mitigation: MISSING - need training plan or new hires
   → Impact: HIGH

2. ⚠️  Operational Complexity Explosion
   → 15 services vs 1 monolith = 15x operational burden
   → Mitigation: PARTIAL - have monitoring, lack service mesh
   → Impact: HIGH

[... more failure modes ...]

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
💡 KEY INSIGHTS
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

• Current architecture pain points don't justify migration risk
• Team velocity would drop 40-60% for 6+ months
• DevOps infrastructure requires 3-4 months of prep work
• Alternative: Modularize monolith first, extract later

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
✅ RECOMMENDED ACTIONS
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Immediate (Month 1-2):
  1. Modularize monolith with clear bounded contexts
  2. Implement observability (distributed tracing, metrics)
  3. Hire senior distributed systems engineer

Medium-term (Month 3-6):
  4. Build CI/CD pipeline capable of multi-service deployments
  5. Run chaos engineering experiments on modular monolith
  6. Extract 1-2 non-critical services as proof of concept

Reassess in 6 months with checklist:
  ☐ Team has 2+ people with production microservices experience
  ☐ DevOps can deploy 10+ services with <5min MTTR
  ☐ Clear business justification (scale, team autonomy, etc.)

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

📎 Session: session-abc123
💾 Full report: ~/.moe/sessions/session-abc123/report.md
```

---

#### 5. `moe quick <model-id> <problem>`

**Purpose**: Directly apply a specific model (Scenario C - fast path)

**Behavior**:
1. Create session
2. Call `generate_questions` for model
3. If questions can be inferred or answered via flags, skip Q&A
4. Otherwise enter Q&A mode
5. Apply and show report

**Examples**:
```bash
# With auto-inference
moe quick inversion "Product launch plan" \
  --goal "Ship by Q2" \
  --failure-modes "UX issues, bugs, market timing"

# Minimal (triggers Q&A for missing info)
moe quick weighted_decision_matrix "Choose vendor"
```

---

#### 6. Session Management Commands

```bash
# List all sessions
moe list
moe list --status completed
moe list --recent 10

# Show session details
moe show <session-id>
moe show <session-id> --full

# Delete sessions
moe delete <session-id>
moe clean --older-than 30d

# Export/import
moe export <session-id> --output session.json
moe import session.json
```

---

### Session File Format

**Location**: `~/.moe/sessions/<session-id>.json`

**Schema**:
```json
{
  "session_id": "session-abc123",
  "created_at": "2025-11-16T10:00:00Z",
  "updated_at": "2025-11-16T10:45:00Z",
  "status": "in_progress|completed|abandoned",

  "problem": {
    "description": "Should we migrate to microservices?",
    "domain": "technical",
    "context": {
      "team_size": 5,
      "current_architecture": "monolith"
    }
  },

  "suggested_models": [
    {
      "model_id": "inversion",
      "relevance_score": 0.92,
      "reason": "...",
      "selected": true
    }
  ],

  "selected_model": {
    "model_id": "inversion",
    "selected_at": "2025-11-16T10:15:00Z"
  },

  "questions": [
    {
      "id": "goal",
      "prompt": "What is the primary outcome?",
      "answered": true,
      "answer": "Successfully migrate to microservices by Q3",
      "answered_at": "2025-11-16T10:20:00Z"
    },
    {
      "id": "failure_modes",
      "prompt": "What are worst plausible failures?",
      "answered": true,
      "answer": "Skill gap, operational complexity, cost overruns",
      "answered_at": "2025-11-16T10:25:00Z"
    }
  ],

  "report": {
    "generated_at": "2025-11-16T10:45:00Z",
    "recommendation": "Conditional NO - delay 6 months",
    "confidence": 0.78,
    "full_path": "~/.moe/sessions/session-abc123/report.md"
  }
}
```

---

## Mental Model Registry Schema

### Registry Structure

**Location**: `registry/models/*.yaml`

**Example**: `registry/models/inversion.yaml`

```yaml
# Model Metadata
id: inversion
name: Inversion
category: risk_analysis
tags:
  - risk
  - strategy
  - critical_thinking
  - failure_analysis

# Description
short_description: "Think backwards - identify what to avoid instead of what to pursue"
long_description: |
  Inversion is a powerful mental model where you approach a problem by thinking
  about what you want to avoid rather than what you want to achieve. By asking
  "How could this fail?" instead of "How can this succeed?", you often identify
  critical risks and overlooked failure modes.

  Charlie Munger: "Invert, always invert. Many problems are best solved backwards."

# When to use
best_for:
  - Risk identification
  - Strategy validation
  - Quality assurance
  - Avoiding failure modes
  - Testing assumptions

avoid_when:
  - Need creative ideation (use First Principles instead)
  - Overly pessimistic team culture
  - Time-sensitive decisions with clear upside

# Difficulty and time
complexity: moderate
estimated_time_minutes: 15-30
expertise_required: none

# Required inputs
required_inputs:
  - id: goal
    prompt: "What is the primary outcome you're aiming for?"
    type: text
    placeholder: "Launch product successfully in Q2 with >1000 users"
    validation:
      min_length: 10
      max_length: 500

  - id: failure_modes
    prompt: "What are the worst plausible failure scenarios?"
    type: multiline
    placeholder: |
      Example:
      - Poor user experience leading to churn
      - Critical bugs in production
      - Market timing - launching too early/late
    guidance: "Think about things that would make this a catastrophic failure"
    validation:
      min_length: 20

  - id: current_mitigations
    prompt: "What are you currently doing to prevent these failures?"
    type: multiline
    placeholder: |
      Example:
      - UX testing: Weekly user interviews
      - Quality: Automated test suite with 80% coverage
      - Timing: Market research completed
    validation:
      optional: true

# Application template
application_template: |
  You are applying the Inversion mental model to help analyze a decision.

  Problem: {{problem_description}}
  Goal: {{answers.goal}}
  Identified failure modes: {{answers.failure_modes}}
  Current mitigations: {{answers.current_mitigations}}

  Please provide a comprehensive inversion analysis:

  1. FAILURE MODE ANALYSIS
     - Evaluate each failure mode for:
       * Probability (1-10)
       * Impact if it occurs (1-10)
       * Current mitigation adequacy (none/partial/strong)

  2. HIDDEN FAILURE MODES
     - Identify additional failure modes the user may have missed
     - Consider second-order effects and systemic risks

  3. MITIGATION GAPS
     - For each failure mode, assess if mitigation is sufficient
     - Identify the 3-5 highest priority gaps

  4. INVERSION INSIGHTS
     - What does inverting the question reveal?
     - What should definitely be avoided?
     - What assumptions are most dangerous?

  5. RECOMMENDATION
     - Should they proceed, delay, or pivot?
     - What conditions must be true to proceed safely?
     - Priority actions to strengthen weak points

  Format the output as structured markdown with clear sections.

# Examples
examples:
  - name: "Product Launch Decision"
    problem: "Should we launch our new app in 2 weeks?"
    answers:
      goal: "Successful launch with positive user reception"
      failure_modes: |
        - Critical bugs that crash the app
        - Poor onboarding causing user confusion
        - Server overload from unexpected traffic
        - Negative press reviews
      current_mitigations: |
        - Beta testing with 50 users
        - Basic load testing completed
        - PR team has prepared announcement
    outcome: |
      Analysis revealed insufficient load testing (only tested to 1000 concurrent users,
      but PR push could bring 10K+). Recommendation: Delay 1 week to add auto-scaling
      and conduct proper load tests. Better to launch late than to crash publicly.

  - name: "Hiring Decision"
    problem: "Should we hire this senior engineer?"
    answers:
      goal: "Fill critical backend engineering gap"
      failure_modes: |
        - Cultural misfit leading to team friction
        - Technical skills not as strong as presented
        - Leaves within 6 months
      current_mitigations: |
        - 3 rounds of interviews including technical
        - Reference checks (2 completed)
        - Trial project (1 week assignment)
    outcome: |
      Inversion revealed missing mitigation: no culture-fit deep dive with team.
      Recommendation: Proceed with hire ONLY after team lunch/informal session
      and feedback from would-be peers. High skill + poor culture fit = net negative.

# Related models
related_models:
  - id: pre_mortem
    relationship: complementary
    note: "Pre-mortem is structured inversion for project planning"

  - id: second_order_thinking
    relationship: extends
    note: "Apply inversion to consequences of consequences"

  - id: risk_matrix
    relationship: follows
    note: "Use risk matrix to prioritize identified failure modes"

# References
references:
  - author: "Charlie Munger"
    source: "Poor Charlie's Almanack"
    quote: "Invert, always invert"
    year: 2005

  - author: "Carl Jacobi"
    source: "Mathematical foundations"
    note: "man muss immer umkehren (one must always invert)"
    year: 1804
```

---

### Registry Index

**File**: `registry/index.yaml`

```yaml
version: "1.0.0"
models_directory: "./models"

categories:
  risk_analysis:
    name: "Risk Analysis"
    description: "Models for identifying and mitigating risks"
    models:
      - inversion
      - pre_mortem
      - risk_matrix
      - failure_mode_analysis

  multi_criteria_decision:
    name: "Multi-Criteria Decision Making"
    description: "Comparing options across multiple dimensions"
    models:
      - weighted_decision_matrix
      - pugh_matrix
      - analytic_hierarchy_process

  strategic_thinking:
    name: "Strategic Thinking"
    description: "Long-term planning and competitive analysis"
    models:
      - second_order_thinking
      - game_theory
      - blue_ocean_strategy
      - scenario_planning

  creative_thinking:
    name: "Creative & Innovative Thinking"
    description: "Generating novel solutions"
    models:
      - first_principles
      - lateral_thinking
      - scamper
      - design_thinking

  probability_estimation:
    name: "Probability & Uncertainty"
    description: "Reasoning under uncertainty"
    models:
      - bayesian_updating
      - expected_value
      - monte_carlo
      - base_rate_neglect

# Model quick search index
tags_index:
  risk: [inversion, pre_mortem, risk_matrix, expected_value]
  strategy: [second_order_thinking, game_theory, blue_ocean_strategy]
  innovation: [first_principles, lateral_thinking, scamper]
  comparison: [weighted_decision_matrix, pugh_matrix]
  uncertainty: [bayesian_updating, monte_carlo, scenario_planning]
```

---

## User Flows (Three Scenarios)

### Scenario A: Suggestions Only

**User Goal**: "Just show me what frameworks might help"

**Flow**:
```bash
$ moe decide "Choosing a pricing strategy for B2B SaaS"

🧠 Analyzing your problem...

📋 Suggested Mental Models:

1. ⭐ Value-Based Pricing (Relevance: 94%)
   → Price based on customer value, not cost
   → Time: 30-45 min

2. 📊 Conjoint Analysis (Relevance: 87%)
   → Measure feature value trade-offs
   → Time: 1-2 hours

3. 🎯 Price Anchoring Strategy (Relevance: 82%)
   → Use reference points to shape perception
   → Time: 20-30 min

💡 Learn more: moe show-model value_based_pricing
💡 Apply: moe use <session-id> value_based_pricing
```

**User Action**: Reads suggestions, maybe explores externally, done.

---

### Scenario B: Full Interactive Journey

**Turn 1: Problem Description**

```bash
$ moe decide "Should we pivot from B2C to B2B?"

🧠 Decision Session: session-f8a3

📋 Top 3 Models for your decision:
  1. Weighted Decision Matrix
  2. Pre-Mortem Analysis
  3. Strategic Options Framework

Next: moe use session-f8a3 <model-id>
```

**Turn 2: Model Selection + Questions**

```bash
$ moe use session-f8a3 weighted_decision_matrix

🎯 Applying: Weighted Decision Matrix

This framework helps you compare options across multiple criteria
with explicit weightings for importance.

I'll ask you 4 questions to build your decision matrix.

❓ Question 1 of 4

List all the options you're deciding between:

Example: "B2C only, B2B only, Hybrid approach"

Your answer: B2C only, B2B only, Hybrid (B2C + B2B)

✓ Saved

❓ Question 2 of 4

What criteria matter for this decision?

Example: "Revenue potential, Market size, Team capability"

Your answer: Revenue potential, Market fit, Team experience, Time to profit

✓ Saved

[... questions 3 & 4 ...]

✅ All questions answered!

Next: moe apply session-f8a3
```

**Turn 3: Apply & Report**

```bash
$ moe apply session-f8a3

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
🎯 DECISION ANALYSIS REPORT
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Recommendation: Hybrid approach (B2C + B2B)
Confidence: 72%

[... full report ...]

💾 Saved to: ~/.moe/sessions/session-f8a3/report.md
```

---

### Scenario C: Direct Model Application

**User Goal**: "I know I want to use Inversion, just help me apply it"

**Flow**:

```bash
$ moe quick inversion "Launch marketing campaign next week"

🎯 Applying Inversion to your problem...

To use Inversion, I need a bit more info:

❓ What is your primary goal?

Your answer: Get 1000 signups from the campaign

❓ What are the worst failure scenarios?

Your answer:
- Low conversion (<1%)
- Ad spend waste
- Brand damage from poor messaging

✓ Generating analysis...

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
INVERSION ANALYSIS
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

[... report ...]
```

**Faster** if user provides inputs upfront:

```bash
$ moe quick inversion "Launch campaign" \
  --goal "1000 signups" \
  --failure-modes "Low conversion, budget waste, brand damage"

# Skips Q&A, goes straight to report
```

---

## Implementation Phases

### Phase 0: Foundation (Week 1-2)

**Deliverables**:
- [ ] Project structure and repository setup
- [ ] Mental model registry schema design
- [ ] 5 initial mental models defined in YAML
  - Inversion
  - Weighted Decision Matrix
  - Pre-Mortem
  - First Principles
  - Second-Order Thinking
- [ ] Technology stack decisions finalized
- [ ] Development environment setup

**Success Criteria**:
- Registry validates against JSON Schema
- Can load and query model definitions
- Clear contribution guide for adding models

---

### Phase 1: MCP Server MVP (Week 3-4)

**Deliverables**:
- [ ] MCP server scaffolding
- [ ] `suggest_models` tool implementation
- [ ] `generate_questions` tool implementation
- [ ] `apply_model` tool implementation (1-2 models)
- [ ] LLM integration with prompt templates
- [ ] Model registry loader
- [ ] Unit tests for each tool

**Success Criteria**:
- Server responds to all 3 core tools
- Can suggest models for a problem description
- Can generate questions for at least 2 models
- Can apply those models and return structured output
- Response time <3s for suggestions

---

### Phase 2: CLI MVP (Week 5-6)

**Deliverables**:
- [ ] CLI framework setup (Click/Typer or Cobra)
- [ ] `moe decide` command
- [ ] `moe use` command
- [ ] `moe answer` command (interactive)
- [ ] `moe apply` command
- [ ] Session management (create, load, save)
- [ ] Basic output formatting
- [ ] MCP client integration

**Success Criteria**:
- Can complete full Scenario B flow end-to-end
- Sessions persist correctly
- Error handling for missing inputs
- Readable terminal output with colors

---

### Phase 3: Polish & UX (Week 7-8)

**Deliverables**:
- [ ] Rich terminal formatting (tables, markdown)
- [ ] `moe quick` fast-path command
- [ ] `moe list`, `moe show`, `moe delete` commands
- [ ] Input validation and helpful error messages
- [ ] Progress indicators for LLM calls
- [ ] Configuration file support
- [ ] Bash/Zsh completion scripts
- [ ] Documentation and examples

**Success Criteria**:
- All 3 scenarios work smoothly
- Professional-looking reports
- Helpful error messages guide users
- Sub-second response for non-LLM operations

---

### Phase 4: Model Library Expansion (Week 9-10)

**Deliverables**:
- [ ] 10 additional mental models in registry
  - Risk Matrix
  - Expected Value
  - Scenario Planning
  - SWOT Analysis
  - Pareto Analysis (80/20)
  - Opportunity Cost
  - Sunk Cost Fallacy Check
  - Circle of Competence
  - Base Rate Analysis
  - Regression to the Mean
- [ ] Model combinations/sequences
- [ ] Cross-model recommendations
- [ ] Model selection algorithm improvements

**Success Criteria**:
- 15+ models total
- Can suggest model combinations
- High relevance scores (>80% user agreement)

---

### Phase 5: Advanced Features (Week 11-12)

**Deliverables**:
- [ ] Batch/non-interactive mode for CI/CD
- [ ] Session import/export (JSON, YAML)
- [ ] Report templates (PDF, HTML exports)
- [ ] Multi-model analysis (apply 2+ models to same problem)
- [ ] Bias checking in recommendations
- [ ] Decision journal (track outcomes over time)
- [ ] Sensitivity analysis for weighted models

**Success Criteria**:
- Can be used in automated pipelines
- Professional report exports
- Decision quality scoring implemented

---

### Phase 6: Beta & Iteration (Week 13-16)

**Deliverables**:
- [ ] Beta testing with 10-20 users
- [ ] Feedback collection and prioritization
- [ ] Performance optimization
- [ ] Bug fixes and edge cases
- [ ] Documentation polish
- [ ] Video tutorials
- [ ] Public repository release

**Success Criteria**:
- <5 critical bugs reported
- >80% user satisfaction
- <1s latency for 95% of operations
- Complete documentation

---

## Technical Stack

### Recommended Stack (Python)

**CLI**:
- **Framework**: [Typer](https://typer.tiangolo.com/) (modern, type-safe CLI framework)
- **Terminal UI**: [Rich](https://rich.readthedocs.io/) (beautiful formatting, tables, markdown)
- **Prompts**: [Questionary](https://questionary.readthedocs.io/) (interactive prompts)
- **Config**: [Pydantic Settings](https://docs.pydantic.dev/latest/concepts/pydantic_settings/)

**MCP Server**:
- **Framework**: [FastMCP](https://github.com/jlowin/fastmcp) (Python MCP SDK)
- **LLM**: [Anthropic Python SDK](https://github.com/anthropics/anthropic-sdk-python)
- **Validation**: [Pydantic](https://docs.pydantic.dev/)
- **Registry**: [PyYAML](https://pyyaml.org/) + [jsonschema](https://python-jsonschema.readthedocs.io/)

**Shared**:
- **Language**: Python 3.11+
- **Package Manager**: Poetry or uv
- **Testing**: pytest + coverage
- **Linting**: ruff
- **Type Checking**: mypy

### Alternative Stack (TypeScript/Go)

**CLI (Go)**:
- **Framework**: [Cobra](https://cobra.dev/)
- **Terminal UI**: [Bubble Tea](https://github.com/charmbracelet/bubbletea)
- **Config**: [Viper](https://github.com/spf13/viper)

**MCP Server (TypeScript)**:
- **Framework**: [@modelcontextprotocol/sdk](https://www.npmjs.com/package/@modelcontextprotocol/sdk)
- **LLM**: Anthropic TypeScript SDK
- **Validation**: Zod

**Why Python?**
- Faster initial development
- Rich ecosystem for LLM integration
- Easier for contributors from ML/data science background
- Excellent terminal UI libraries

---

## File Structure

```
mixture-of-experts/
├── README.md
├── IMPLEMENTATION_PLAN.md          # This document
├── pyproject.toml                   # Python dependencies (Poetry)
│
├── cli/                             # CLI application
│   ├── moe/
│   │   ├── __init__.py
│   │   ├── main.py                  # CLI entry point
│   │   ├── commands/
│   │   │   ├── __init__.py
│   │   │   ├── decide.py            # moe decide
│   │   │   ├── use.py               # moe use
│   │   │   ├── answer.py            # moe answer
│   │   │   ├── apply.py             # moe apply
│   │   │   ├── quick.py             # moe quick
│   │   │   └── session.py           # list/show/delete
│   │   ├── session/
│   │   │   ├── __init__.py
│   │   │   ├── manager.py           # Session CRUD
│   │   │   └── models.py            # Session data models
│   │   ├── mcp_client/
│   │   │   ├── __init__.py
│   │   │   └── client.py            # MCP client wrapper
│   │   ├── ui/
│   │   │   ├── __init__.py
│   │   │   ├── formatters.py        # Rich formatting
│   │   │   └── prompts.py           # Interactive prompts
│   │   └── config.py                # Config management
│   └── tests/
│
├── server/                          # MCP Server
│   ├── moe_server/
│   │   ├── __init__.py
│   │   ├── main.py                  # MCP server entry point
│   │   ├── tools/
│   │   │   ├── __init__.py
│   │   │   ├── suggest_models.py
│   │   │   ├── generate_questions.py
│   │   │   ├── apply_model.py
│   │   │   └── validate_inputs.py
│   │   ├── registry/
│   │   │   ├── __init__.py
│   │   │   ├── loader.py            # Load YAML models
│   │   │   ├── query.py             # Search/filter models
│   │   │   └── validator.py         # Validate model definitions
│   │   ├── llm/
│   │   │   ├── __init__.py
│   │   │   ├── client.py            # Anthropic client
│   │   │   └── prompts.py           # Prompt templates
│   │   └── models.py                # Pydantic models
│   └── tests/
│
├── registry/                        # Mental Model Registry
│   ├── schema/
│   │   └── model.schema.json        # JSON Schema for models
│   ├── models/
│   │   ├── inversion.yaml
│   │   ├── weighted_decision_matrix.yaml
│   │   ├── pre_mortem.yaml
│   │   ├── first_principles.yaml
│   │   ├── second_order_thinking.yaml
│   │   └── ... (more models)
│   ├── index.yaml                   # Registry index
│   └── README.md                    # How to add models
│
├── docs/                            # Documentation
│   ├── CLI_GUIDE.md
│   ├── MCP_SERVER_API.md
│   ├── MENTAL_MODELS_GUIDE.md
│   ├── CONTRIBUTING.md
│   └── examples/
│       ├── scenario_a.md
│       ├── scenario_b.md
│       └── scenario_c.md
│
└── examples/                        # Example sessions
    ├── session_examples/
    │   ├── vendor_selection.json
    │   ├── product_pivot.json
    │   └── career_decision.json
    └── scripts/
        └── demo.sh                  # Demo walkthrough
```

---

## Success Metrics

### User Experience Metrics

**Primary**:
- **Task Success Rate**: >90% of users complete decision flow without errors
- **Time to First Report**: <5 minutes from `moe decide` to `moe apply`
- **User Satisfaction**: >4.0/5.0 rating on usefulness

**Secondary**:
- **Model Relevance**: >80% agreement that suggestions are relevant
- **Question Clarity**: >85% find questions clear and answerable
- **Report Quality**: >75% rate reports as "helpful" or "very helpful"

### Technical Performance Metrics

- **Suggestion Latency**: <2s for `suggest_models`
- **Question Generation**: <1s for `generate_questions`
- **Report Generation**: <5s for `apply_model`
- **CLI Responsiveness**: <100ms for non-MCP commands
- **Error Rate**: <1% of requests fail with errors

### Adoption Metrics (Post-Launch)

- **Daily Active Users**: Track growth
- **Models Per Decision**: Average 1.3-1.5 (shows multi-model use)
- **Session Completion Rate**: >60% of started sessions complete
- **Repeat Usage**: >40% of users return within 7 days

### Quality Metrics

- **Code Coverage**: >80% test coverage
- **Documentation Coverage**: All commands and models documented
- **Model Library Size**: 15+ models by v0.1, 50+ by v1.0
- **User-Contributed Models**: >5 community submissions within 3 months

---

## Next Steps

### Immediate Actions (This Week)

1. **Review & Approve Plan**: Stakeholder sign-off on approach
2. **Tech Stack Decision**: Python vs Go/TS (recommend Python)
3. **Repository Setup**: Initialize mono-repo with cli/ and server/
4. **First 5 Models**: Define in YAML format
   - Inversion
   - Weighted Decision Matrix
   - Pre-Mortem
   - First Principles
   - Second-Order Thinking

### Week 1 Deliverables

- [ ] Registry schema finalized
- [ ] 5 models fully defined with examples
- [ ] Project scaffolding complete
- [ ] Development environment documented
- [ ] First MCP server prototype (suggest_models only)

### Open Questions

1. **LLM Provider**: Anthropic only or support multiple (OpenAI, Gemini)?
2. **Model Customization**: Allow users to create private model libraries?
3. **Collaboration**: Multi-user sessions for team decisions?
4. **Analytics**: Track anonymous usage for model improvement?
5. **Pricing**: Open source CLI + hosted MCP server option?

---

## Appendix: Example Prompt Templates

### Suggest Models Prompt

```
You are a decision-making expert helping users find the right mental model.

Problem: {{problem_description}}
Domain: {{domain}}
Context: {{context}}

Analyze this problem and suggest 3-5 mental models from the registry below
that would be most helpful.

Available Models:
{{model_registry_summary}}

For each suggestion, provide:
1. Model ID
2. Relevance score (0-1)
3. 1-sentence reason why it fits
4. Estimated time needed

Return as JSON matching this schema:
{
  "suggestions": [
    {
      "model_id": "string",
      "relevance_score": float,
      "reason": "string",
      "estimated_time_minutes": int
    }
  ]
}
```

### Apply Model Prompt (Inversion Example)

```
You are applying the Inversion mental model to analyze a decision.

FRAMEWORK: Inversion
PRINCIPLE: Instead of asking "how to succeed", ask "how to fail"
          to identify risks and pitfalls.

PROBLEM: {{problem_description}}

USER INPUTS:
Goal: {{answers.goal}}
Failure Modes: {{answers.failure_modes}}
Current Mitigations: {{answers.current_mitigations}}

TASK:
Provide a comprehensive inversion analysis with these sections:

1. FAILURE MODE ANALYSIS
   For each failure mode, assess:
   - Probability (1-10 scale)
   - Impact if it occurs (1-10 scale)
   - Current mitigation strength (none/weak/moderate/strong)

2. HIDDEN FAILURE MODES
   Identify 3-5 additional failure modes the user may have overlooked.
   Focus on:
   - Second-order effects
   - Systemic risks
   - Timing/sequencing failures

3. MITIGATION GAPS
   For each failure mode, evaluate if current mitigation is adequate.
   Highlight the 3-5 highest-priority gaps.

4. INVERSION INSIGHTS
   - What does inverting the question reveal?
   - What should absolutely be avoided?
   - Which assumptions are most dangerous?

5. RECOMMENDATION
   - Proceed / Delay / Pivot / Cancel
   - Confidence level (0-100%)
   - Conditions required to proceed safely
   - Top 3 priority actions

Format as structured JSON matching the schema.
Be specific, actionable, and honest about risks.
```

---

**End of Implementation Plan**

*This plan is a living document and will be updated as we progress through implementation.*
