<!-- course-title: Prompt Engineering for Generative AI -->
<!-- course-theme: roi-alt-theme -->

<!-- layout: title -->
![ROI Logo](images/roi-logo-with-name.png)

Prompt Engineering for Generative AI

# Chapter 1: Prompt Engineering Fundamentals

---

# Chapter 1: Objectives

- Apply core prompt engineering techniques, personas, and structured formats in Google Gemini
- Explain what prompt engineering is and why structured prompts improve AI responses
- Identify the core components that make up a clear and effective prompt
- Assign personas and system roles to guide tone, expertise, and perspective
- Set explicit constraints and request structured formats like tables or JSON
- Use few-shot prompting with input-output pairs to guide model behavior
- Refine and evaluate prompts iteratively to fix ambiguities and improve accuracy
- Apply prompt engineering techniques in Google Gemini to solve practical tasks

---

<!-- layout: navigation -->
# Chapter 1

- **Introduction to Prompt Engineering**
- Anatomy of an Effective Prompt
- Defining Personas and Roles
- Specifying Constraints and Output Formats
- Providing Few-Shot Examples
- Iterative Refinement and Evaluation
- Lab: Prompt Engineering with Google Gemini

---

# What is Prompt Engineering?

- **Directing model behavior**: structuring input text to guide generative models toward accurate, relevant, and consistent outputs
- Large language models predict the most probable next tokens based on context
- Underspecified inputs force the model to guess tone, audience, and format
- Systematic prompt design turns unpredictable text generation into a repeatable engineering practice

> [!NOTE]
> Generative AI models do not understand business intent or unspoken context. They respond solely to the tokens provided.

---

<!-- layout: 2-column -->
# Why Prompts Fail: The Underspecified Request

### Vague Prompt
- “Write an update on the project delay.”
- Model guesses the audience (client vs internal engineering)
- Output mixes excuses, technical jargon, and uncertain timelines
- Requires multiple rounds of manual cleanup

### Structured Prompt
- States the exact role, target audience, and business objective
- Specifies key facts: milestone missed, new ship date, mitigation steps
- Enforces an executive tone with three concise bullet points
- Yields a usable communication draft on the first attempt

---

<!-- layout: card-layout -->
# Core Principles for Better Results

### Be Direct
- State the primary objective clearly in the opening sentence.
- Avoid burying the main request beneath paragraphs of background detail.

### Provide Context
- Supply the specific facts, assumptions, and target audience upfront.
- Eliminate guesswork so the model does not invent missing details.

### Bound the Scope
- Define explicit limits on length, topics, and forbidden phrasing.
- Clarify what to exclude just as strictly as what to include.

---

<!-- layout: navigation -->
# Chapter 1

- Introduction to Prompt Engineering
- **Anatomy of an Effective Prompt**
- Defining Personas and Roles
- Specifying Constraints and Output Formats
- Providing Few-Shot Examples
- Iterative Refinement and Evaluation
- Lab: Prompt Engineering with Google Gemini

---

<!-- layout: 3-column -->
# Components of a Production Prompt

### Role and Goal
- **Persona**: identity and perspective
- **Task**: the exact action to perform
- **Audience**: who reads the output

### Context and Source
- **Background**: relevant project details
- **Inputs**: raw data, notes, or text
- **Assumptions**: operational baselines

### Rules and Schema
- **Constraints**: length and negative bounds
- **Format**: JSON, table, or bullets
- **Tone**: formal, critical, or concise

---

# Assembling a Structured Prompt

- Clear delimiters separate instructions from reference data
- Labeled sections allow the model to distinguish background facts from direct commands

```text
Role: You are a technical documentation lead at a cloud software company.
Task: Summarize the incident notes below into a customer-facing status update.
Audience: Enterprise customers affected by the service disruption.
Constraints:
- Keep the total response under 120 words.
- Do not mention internal server hostnames or engineer names.
- Use a calm, reassuring, and professional tone.
Format: A single paragraph followed by two bullet points for next steps.

Incident Notes:
Database cluster db-prod-04 experienced memory exhaustion at 14:10 UTC.
Failover completed at 14:28 UTC. Normal query latency restored.
```

---

<!-- layout: 2-column -->
# Architectural Traps to Avoid

### Overloaded Instructions
- Bundling five distinct tasks into a single prompt
- Model skips steps or answers only the final question
- Hard to debug which instruction failed
- **Fix**: split complex workflows into sequential prompt steps

### Contradictory Rules
- Requesting comprehensive detail while enforcing a 50-word cap
- Asking for creative storytelling and strict factual adherence
- Model truncates mid-sentence or ignores negative constraints
- **Fix**: align length limits with requested depth

---

<!-- layout: navigation -->
# Chapter 1

- Introduction to Prompt Engineering
- Anatomy of an Effective Prompt
- **Defining Personas and Roles**
- Specifying Constraints and Output Formats
- Providing Few-Shot Examples
- Iterative Refinement and Evaluation
- Lab: Prompt Engineering with Google Gemini

---

# How Personas Anchor Output

- **Shaping probability distributions**: assigning a role establishes vocabulary, assumed knowledge, and perspective
- Prompts without a role draw from generic internet prose
- Personas adjust technical depth for the intended recipient
- System instructions help prevent the model from drifting into conversational filler

> [!TIP]
> Tell the model what it knows and what it cares about. A financial analyst focuses on cash flow; an engineer focuses on latency.

---

<!-- layout: 2-column -->
# Comparing Persona Shifts on One Topic

### Executive Persona
- “You are a Chief Information Security Officer briefing the Board of Directors.”
- Focuses on enterprise risk, regulatory compliance, and budget impact
- Strips out raw log outputs and individual CVE numbers
- Produces concise strategic recommendations

### Security Engineer Persona
- “You are a Lead Application Security Engineer writing an incident ticket.”
- Focuses on root cause, reproduction steps, and patch validation
- Includes specific endpoint paths, payload types, and code snippets
- Produces actionable remediation instructions for developers

---

<!-- layout: card-layout -->
# Writing Effective Role Directives

### Frame Specific Expertise
- Name the exact profession, specialty, and seniority level.
- Avoid vague qualifiers like “act like a smart expert.”

### Define Communication Style
- Specify how the persona communicates: objective, skeptical, or mentoring.
- Instruct the persona to challenge weak arguments or highlight edge cases.

### Identify the Audience
- State who the persona is advising to calibrate technical complexity.
- A senior architect explains differently to an intern than to a peer.

---

<!-- layout: navigation -->
# Chapter 1

- Introduction to Prompt Engineering
- Anatomy of an Effective Prompt
- Defining Personas and Roles
- **Specifying Constraints and Output Formats**
- Providing Few-Shot Examples
- Iterative Refinement and Evaluation
- Lab: Prompt Engineering with Google Gemini

---

# Bounding Creativity with Constraints

- **Guardrails beat assumptions**: explicit constraints stop generative models from padding responses with hallucinations
- Negative constraints explicitly declare what the model must omit
- Scope limits restrict answers strictly to the provided reference text
- Length limits must be measurable (e.g., words, bullets, sentences) rather than subjective labels like “short”

> [!WARNING]
> Stating “be brief” is subjective and unreliable. Request “no more than three bullet points, each under twenty words.”

---

<!-- layout: 2-column -->
# Freeform Prose vs Structured Formats

### Freeform Prose
- Natural paragraphs with conversational introductions
- Difficult to parse programmatically or paste into spreadsheets
- Inconsistent ordering between repeated model runs
- Model frequently adds unsolicited commentary

### Structured Schemas
- Predictable field names, tables, and JSON key-value pairs
- Directly consumable by downstream tools and applications
- Forces the model to extract specific attributes consistently
- Eliminates conversational pleasantries and filler text

---

# Enforcing Output Schemas

- Explicit schema definitions require the model to populate exact keys
- Negative constraints prevent the model from wrapping data in Markdown commentary

```text
Extract the action items from the meeting transcript.

Output format rules:
- Return valid JSON only.
- Do not include markdown code fences, backticks, or introductory text.
- Follow this exact schema:
{
  "tasks": [
    {
      "task_id": 1,
      "description": "Short summary of action item",
      "owner": "Person responsible or 'Unassigned'",
      "due_date": "YYYY-MM-DD or 'TBD'"
    }
  ]
}
```

---

<!-- layout: navigation -->
# Chapter 1

- Introduction to Prompt Engineering
- Anatomy of an Effective Prompt
- Defining Personas and Roles
- Specifying Constraints and Output Formats
- **Providing Few-Shot Examples**
- Iterative Refinement and Evaluation
- Lab: Prompt Engineering with Google Gemini

---

<!-- layout: 2-column -->
# Zero-Shot vs Few-Shot Prompting

### Zero-Shot Prompting
- Provides instructions with zero input-output examples
- Relies solely on the model’s pre-trained knowledge and instruction tuning
- Best for straightforward summaries, drafting, and open-ended ideation
- Struggles with idiosyncratic schemas or nuanced classification rules

### Few-Shot Prompting
- Demonstrates the expected behavior using two or three sample pairs
- Establishes concrete patterns for style, reasoning, and edge-case handling
- Substantially improves adherence to unusual output structures
- Reduces ambiguity by showing the exact transformation desired

---

<!-- layout: card-layout -->
# Designing High-Quality Exemplars

### Match Real-World Variety
- Include representative variations and edge cases instead of identical simple samples.
- Show how the model should handle missing values or ambiguous input data.

### Maintain Strict Consistency
- Use identical delimiters, labels, and formatting across every exemplar.
- Inconsistent example formatting confuses the model and degrades output quality.

### Balance Context Budget
- Use two to four high-impact examples rather than a dozen repetitive ones.
- Excessive exemplars increase input token costs without boosting accuracy.

---

# Few-Shot Pattern Demonstration

- Providing input-output pairs anchors formatting and classification decisions
- The model learns the schema pattern without lengthy rule descriptions

```text
Classify customer support tickets into Category, Urgency, and Action.

Input: "My screen goes blank whenever I unplug the HDMI cable."
Output: Category: Hardware | Urgency: Medium | Action: Replace cable or adapter

Input: "Cannot log into production portal. Entire sales team is locked out."
Output: Category: Authentication | Urgency: Critical | Action: Reset tenant session

Input: "Would love to see a dark mode option in the next mobile release."
Output: Category: Feature Request | Urgency: Low | Action: Log to backlog

Input: "Credit card charged twice for annual subscription renewal."
Output:
```

---

<!-- layout: navigation -->
# Chapter 1

- Introduction to Prompt Engineering
- Anatomy of an Effective Prompt
- Defining Personas and Roles
- Specifying Constraints and Output Formats
- Providing Few-Shot Examples
- **Iterative Refinement and Evaluation**
- Lab: Prompt Engineering with Google Gemini

---

# Prompt Engineering as an Empirical Loop

- **Refinement is systematic**: production prompts require iterative tuning against realistic test cases
- Single prompt successes often fail when applied to different input data
- Inspect failures to isolate whether role, context, or constraints caused the error
- Adjust one variable at a time to measure the impact of each prompt change

> [!IMPORTANT]
> Never evaluate a prompt on a single clean input. Test boundary cases, empty inputs, and noisy real-world data.

---

<!-- layout: 3-column -->
# Diagnosing Common Breakdowns

### Hallucinations
- **Symptom**: model invents facts or citations
- **Cause**: missing context or open-ended task
- **Remedy**: restrict answers to provided text; require citations

### Formatting Leaks
- **Symptom**: conversational text around JSON
- **Cause**: weak negative constraints
- **Remedy**: specify “output valid JSON only with no commentary”

### Vague Summaries
- **Symptom**: generic bullet points lacking substance
- **Cause**: loose task verbs like “analyze”
- **Remedy**: replace with specific extraction instructions

---

<!-- layout: card-layout -->
# The Iterative Refinement Workflow

### 1. Establish Baseline
- Draft the initial prompt with task, role, context, and desired output format.
- Run against three distinct sample inputs to establish baseline performance.

### 2. Isolate Failure Modes
- Catalog errors such as hallucinated facts, dropped constraints, or tone drift.
- Identify whether the failure stems from ambiguity, missing data, or schema complexity.

### 3. Tighten and Lock
- Add explicit delimiters, negative constraints, or targeted few-shot exemplars.
- Verify that fixing one edge case did not break previously successful outputs.

---

<!-- layout: navigation -->
# Chapter 1

- Introduction to Prompt Engineering
- Anatomy of an Effective Prompt
- Defining Personas and Roles
- Specifying Constraints and Output Formats
- Providing Few-Shot Examples
- Iterative Refinement and Evaluation
- **Lab: Prompt Engineering with Google Gemini**

---

# Lab: Prompt Engineering with Google Gemini

Lab link: TODO

---

# What You Learned

- Applied core prompt engineering techniques, personas, and structured formats in Google Gemini
- Explained what prompt engineering is and why structured prompts improve AI responses
- Identified the core components that make up a clear and effective prompt
- Assigned personas and system roles to guide tone, expertise, and perspective
- Set explicit constraints and requested structured formats like tables or JSON
- Used few-shot prompting with input-output pairs to guide model behavior
- Refined and evaluated prompts iteratively to fix ambiguities and improve accuracy
- Applied prompt engineering techniques in Google Gemini to solve practical tasks

---

# Quiz 1 of 3

**Why do underspecified, vague prompts frequently lead to low quality AI responses?**

- A. Generative models reject prompts that do not contain code snippets
- B. The model must guess missing context, audience, and constraints, leading to generic or inaccurate outputs
- C. Underspecified prompts bypass the model’s pre-training safety guardrails
- D. Large language models can only process requests structured as JSON schemas

---

# Quiz 1: Answer

**Why do underspecified, vague prompts frequently lead to low quality AI responses?**

**Correct: B.** The model must guess missing context, audience, and constraints, leading to generic or inaccurate outputs

- Generative AI models generate text based on statistical token probabilities conditioned on the prompt
- Without clear constraints, models draw from generic pre-training data rather than specific business rules
- Explicit instructions about persona, audience, and format eliminate unnecessary model guesswork
- Adding negative bounds and concrete context anchors the response to intended facts

---

# Quiz 2 of 3

**When should you use few-shot prompting instead of zero-shot prompting?**

- A. When you need the model to output a strictly formatted schema or follow nuanced domain-specific patterns
- B. When you want the model to generate open-ended creative poetry with no rules
- C. Only when using local open-source models that lack instruction tuning
- D. Whenever you need to reduce total input token consumption to zero

---

# Quiz 2: Answer

**When should you use few-shot prompting instead of zero-shot prompting?**

**Correct: A.** When you need the model to output a strictly formatted schema or follow nuanced domain-specific patterns

- Zero-shot works well for general tasks, summaries, and standard conversational requests
- Few-shot demonstrates concrete input-output examples that clarify edge cases and formatting
- Exemplars establish an unambiguous pattern for the model to replicate
- A small set of two to three clean examples is generally sufficient to guide model behavior

---

<!-- layout: 2-column -->
# Quiz 3 of 3: Discussion

### Prompt
Your team wants to use Google Gemini to automatically categorize inbound customer feedback and output valid JSON. The initial prompt often returns conversational pleasantries and inconsistent field names.

### Discuss
- Which prompt components are missing or weakly defined?
- How would you structure constraints and examples to ensure valid JSON?
- What validation steps would you take before rolling this prompt into production?

---

<!-- layout: 2-column -->
# Quiz 3: Discussion Points

**Your team wants to use Google Gemini to automatically categorize inbound customer feedback and output valid JSON. The initial prompt often returns conversational pleasantries and inconsistent field names.**

### Strong Answers Mention
- Providing an explicit JSON schema with exact key names and expected types
- Adding negative constraints: “Return valid JSON only. Do not include markdown formatting or commentary”
- Supplying two to three few-shot examples demonstrating clean JSON outputs
- Testing against noisy, real-world customer feedback tickets to confirm parsing reliability

### Watch For
- Believing that simply asking politely for JSON guarantees clean parsing
- Relying on zero-shot instructions without negative constraints or schema definitions
- Overlooking edge cases such as empty feedback or foreign language inputs

---

# Questions and Answers

Questions?
