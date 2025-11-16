# Mental Model Registry

> **Structured library of mental models and decision-making frameworks for the MoE system**

This directory contains the **Mental Model Registry** - a curated, extensible library of mental models and decision-making frameworks. Each model is defined in a structured YAML format that enables the MCP server to:

1. Suggest relevant models for a given problem
2. Generate contextual questions to gather user input
3. Apply the framework to synthesize a decision recommendation

---

## Table of Contents

- [Overview](#overview)
- [Directory Structure](#directory-structure)
- [Model Format](#model-format)
- [Contributing a New Model](#contributing-a-new-model)
- [Validation](#validation)
- [Best Practices](#best-practices)
- [Examples](#examples)

---

## Overview

### What is a Mental Model?

A mental model is a framework for thinking about a problem or making a decision. Examples include:

- **Inversion**: Think backwards - identify what to avoid
- **Weighted Decision Matrix**: Score options across weighted criteria
- **First Principles**: Break down to fundamental truths
- **Pre-Mortem**: Imagine failure and work backwards

### Registry Purpose

The registry serves as:

1. **Knowledge Base**: Structured, machine-readable framework definitions
2. **Prompt Library**: LLM prompt templates for applying each framework
3. **Question Generator**: Input specifications that drive the CLI Q&A flow
4. **Documentation**: Examples and references for each model

---

## Directory Structure

```
registry/
├── README.md                    # This file
├── schema/
│   └── model.schema.json        # JSON Schema for validation
├── models/
│   ├── inversion.yaml           # Individual model definitions
│   ├── weighted_decision_matrix.yaml
│   ├── pre_mortem.yaml
│   ├── first_principles.yaml
│   └── ... (add new models here)
├── index.yaml                   # Registry index and metadata
└── examples/
    └── session_example.json     # Example session using a model
```

---

## Model Format

Each model is defined in a YAML file with this structure:

### Required Fields

```yaml
id: model_name               # Unique identifier (snake_case)
name: Model Name             # Human-readable name
category: category_name      # One of: risk_analysis, multi_criteria_decision, etc.
short_description: "Brief one-liner"
best_for:                    # List of use cases
  - Use case 1
  - Use case 2
complexity: simple|moderate|complex
estimated_time_minutes: 30
required_inputs:             # Questions to ask the user
  - id: field_name
    prompt: "Question to ask?"
    type: text|multiline|list|number|etc
    validation: { ... }
application_template: |      # LLM prompt template (Jinja2)
  You are applying {{model_name}} to help with a decision...
```

### Optional Fields

```yaml
long_description: |
  Detailed explanation with history, usage, etc.

avoid_when:
  - Situation to avoid

optional_inputs:
  - id: optional_field
    prompt: "Optional question?"

examples:
  - name: Example name
    problem: Problem description
    answers: { field: value }
    outcome: What happened

related_models:
  - id: other_model
    relationship: complementary|prerequisite|alternative
    note: Why they're related

references:
  - author: Name
    source: Book or article
    year: 2020
```

See [`schema/model.schema.json`](schema/model.schema.json) for complete specification.

---

## Contributing a New Model

### Step 1: Choose a Model

Select a mental model or framework you want to add. Consider:

- **Is it widely recognized?** (from books, research, practice)
- **Is it actionable?** (can users actually apply it?)
- **Is it distinct?** (not too similar to existing models)

### Step 2: Research the Model

Gather:

- **Definition**: What is this model?
- **Use cases**: When should it be used?
- **Process**: What steps does it involve?
- **Examples**: Real-world applications
- **References**: Books, papers, articles

### Step 3: Define Inputs

Identify what information you need from the user to apply this model:

**Example (Inversion)**:
- `goal`: What are you trying to achieve?
- `failure_modes`: What could go wrong?
- `current_mitigations`: What are you doing to prevent failure?

**Guidelines**:
- **2-6 required inputs**: Not too few (lacks depth), not too many (overwhelms user)
- **Specific prompts**: "What criteria matter?" better than "Tell me more"
- **Clear types**: text, multiline, list, number, weights, boolean, choice
- **Helpful placeholders**: Show examples of good answers

### Step 4: Write the Application Template

This is the LLM prompt that applies the framework. It should:

1. **Explain the framework** briefly
2. **Include user inputs** via Jinja2 variables `{{ answers.field_name }}`
3. **Provide clear structure** for the output (numbered sections, tables, etc.)
4. **Request specific analysis** (not generic "analyze this")
5. **Specify output format** (markdown, JSON, etc.)

**Template Structure**:
```
You are applying the [Model Name] framework.

FRAMEWORK: [Name]
PRINCIPLE: [Core idea]

PROBLEM: {{ problem_description }}

USER INPUTS:
Field1: {{ answers.field1 }}
Field2: {{ answers.field2 }}

TASK:
Provide analysis with these sections:

1. SECTION ONE
   - What to analyze
   - What to output

2. SECTION TWO
   ...

FORMAT REQUIREMENTS:
- Use markdown
- Be specific and actionable
- Show reasoning
```

### Step 5: Add Examples

Include 2-3 examples showing the model in action:

```yaml
examples:
  - name: "Product Launch"
    problem: "Should we launch in 2 weeks?"
    answers:
      goal: "Successful launch with >5K users"
      risks: "Bugs, poor UX, server overload"
    outcome: |
      Analysis revealed critical gap in load testing.
      Recommendation: Delay 1 week to fix.
```

### Step 6: Validate and Test

```bash
# Validate YAML syntax
yamllint models/your_model.yaml

# Validate against schema
jsonschema -i models/your_model.yaml schema/model.schema.json

# Test locally
python scripts/test_model.py your_model
```

### Step 7: Update Index

Add your model to `index.yaml`:

```yaml
categories:
  your_category:
    models:
      - your_model_id

tags_index:
  your_tag:
    - your_model_id
```

### Step 8: Submit PR

1. Fork the repository
2. Create a branch: `git checkout -b add-model-[name]`
3. Add your model file: `registry/models/[name].yaml`
4. Update `index.yaml`
5. Commit: `git commit -m "Add [Model Name] framework"`
6. Push and create pull request

---

## Validation

### Schema Validation

All models must validate against `schema/model.schema.json`.

**Required checks**:
- ✅ All required fields present
- ✅ `id` matches `[a-z0-9_]+` pattern
- ✅ `category` is a valid category
- ✅ `complexity` is simple/moderate/complex
- ✅ `required_inputs` has at least 1 item
- ✅ Each input has `id`, `prompt`, and `type`
- ✅ `application_template` is present

### Content Quality Checks

**Good models have**:
- ✅ Clear, jargon-free descriptions
- ✅ Specific, answerable questions (not vague)
- ✅ 2-3 concrete examples
- ✅ Actionable application templates
- ✅ References to source material

**Avoid**:
- ❌ Overly academic or theoretical models
- ❌ Models requiring specialized expertise
- ❌ Vague questions like "Tell me more"
- ❌ Generic templates that work for any model

---

## Best Practices

### Writing Good Prompts

**❌ Bad**: "What's your goal?"

**✅ Good**: "What is the primary outcome you're aiming for?"
- Longer, more specific
- Includes example: "Launch product successfully in Q2 with >1000 users"
- Provides guidance: "Be specific about what success looks like"

### Writing Good Application Templates

**Structure your template**:

1. **Framework explanation** (2-3 sentences)
2. **User inputs** clearly displayed
3. **Analysis sections** (numbered, 5-8 sections)
4. **Specific deliverables** (tables, lists, scores)
5. **Format requirements** (markdown, be specific, show reasoning)

**Ask for specifics**:
- ❌ "Analyze the options"
- ✅ "For each option, rate on scale 1-10 with reasoning"

**Request structure**:
- ❌ "Provide recommendations"
- ✅ "Provide: (1) Recommended option, (2) Confidence 0-100%, (3) Top 3 conditions required, (4) Next steps"

### Choosing Input Types

| Type | When to Use | Example |
|------|-------------|---------|
| `text` | Short answer (1 sentence) | "What's your budget?" |
| `multiline` | Multiple items or paragraphs | "List all failure modes" |
| `list` | Comma-separated items | "Options: A, B, C" |
| `number` | Numeric value | "Team size: 10" |
| `weights` | Values that sum to 1.0 | "Cost=0.3, Quality=0.7" |
| `boolean` | Yes/No question | "Is this urgent?" |
| `choice` | Select from options | "Priority: low/medium/high" |

### Adding Validation

```yaml
required_inputs:
  - id: team_size
    prompt: "How many people on your team?"
    type: number
    validation:
      min_value: 1
      max_value: 1000

  - id: criteria_weights
    prompt: "Weight each criterion (must sum to 1.0)"
    type: weights
    validation:
      sum_to: 1.0
      all_positive: true

  - id: options
    prompt: "List all options (2-10)"
    type: list
    validation:
      min_items: 2
      max_items: 10
```

---

## Examples

### Minimal Model

```yaml
id: opportunity_cost
name: Opportunity Cost
category: resource_allocation
short_description: "Consider what you're giving up when choosing one option"

best_for:
  - Resource allocation
  - Trade-off decisions

complexity: simple
estimated_time_minutes: 10

required_inputs:
  - id: chosen_option
    prompt: "What option are you considering?"
    type: text

  - id: alternative_options
    prompt: "What other options are you giving up?"
    type: multiline

application_template: |
  You are applying Opportunity Cost analysis.

  CHOSEN: {{ answers.chosen_option }}
  ALTERNATIVES FOREGONE: {{ answers.alternative_options }}

  TASK:
  1. List what the user gains from chosen option
  2. List what they lose by not choosing each alternative
  3. Calculate net opportunity cost
  4. Recommend if the trade-off is worth it
```

### Comprehensive Model

See [`models/inversion.yaml`](models/inversion.yaml) or [`models/weighted_decision_matrix.yaml`](models/weighted_decision_matrix.yaml) for full examples.

---

## FAQ

### How do I decide between categories?

Choose the **primary purpose**:

- **risk_analysis**: Identifying/mitigating risks (Inversion, Pre-Mortem)
- **multi_criteria_decision**: Comparing options with multiple factors (Weighted Matrix)
- **strategic_thinking**: Long-term planning (Second-Order Thinking)
- **creative_thinking**: Generating novel ideas (First Principles)
- **probability_estimation**: Dealing with uncertainty (Expected Value)

### Can a model fit multiple categories?

Yes, use tags! Category is primary, but tags can include `risk`, `strategy`, `innovation`, etc.

### How long should the application_template be?

**Aim for 50-200 lines**:
- Too short (<30 lines): Generic, not enough structure
- Too long (>300 lines): Hard to maintain, slow to execute
- Sweet spot: 100-150 lines with 5-8 clear sections

### Should I include formulas or calculations?

**Yes, if the model involves math**:
- Weighted Decision Matrix: Show scoring formula
- Expected Value: Show probability × impact calculation
- NPV: Show discount rate formula

**Format**:
```
Weighted Score = (Criterion1 × Weight1) + (Criterion2 × Weight2) + ...

Example:
Option A = (8 × 0.3) + (7 × 0.5) + (9 × 0.2) = 7.7
```

### How do I handle model variations?

**Option 1: Single model with variations**

```yaml
optional_inputs:
  - id: variation
    prompt: "Which variation? (standard/advanced)"
    type: choice
    choices: [standard, advanced]
```

Then use Jinja2 conditionals in template:
```jinja2
{% if answers.variation == "advanced" %}
  Perform deep analysis...
{% else %}
  Perform standard analysis...
{% endif %}
```

**Option 2: Separate models**

Create `weighted_matrix_simple.yaml` and `weighted_matrix_advanced.yaml` if variations are substantial.

---

## Resources

### Mental Model Libraries

- **Farnam Street**: https://fs.blog/mental-models/
- **Mental Models Box**: https://www.mentalmodelsbox.com/
- **Super Thinking** (book): Gabriel Weinberg & Lauren McCann
- **Poor Charlie's Almanack** (book): Charlie Munger

### Decision Frameworks

- **Decisive** (book): Chip & Dan Heath
- **Thinking in Bets** (book): Annie Duke
- **Harvard Business Review**: Decision-making articles

### Cognitive Science

- **Thinking, Fast and Slow**: Daniel Kahneman
- **Sources of Power**: Gary Klein
- **Noise**: Kahneman, Sibony, Sunstein

---

## Support

- **Questions**: Open a GitHub Discussion
- **Bugs**: Report an issue
- **Model requests**: Create an issue with "Model Request" label

---

**Happy contributing! Every model you add helps people make better decisions. 🧠**
