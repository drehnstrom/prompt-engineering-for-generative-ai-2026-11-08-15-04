# Solution: Prompt Engineering with Google Gemini

## End State

A set of tested, repeatable prompt patterns demonstrated in Google Gemini that showcase:
1. A structured multi-component prompt (Role, Task, Audience, Context, Constraints, Format) that converts raw incident notes into an executive status update.
2. Two persona-driven prompts applied to the same technical incident (Chief Information Security Officer vs Lead Security Engineer) producing calibrated technical depth and tone.
3. A constrained prompt extracting structured JSON matching an exact schema with negative constraints preventing markdown commentary or fences.
4. A few-shot prompt using three consistent input-output exemplars to classify ambiguous support tickets into Category, Urgency, and Action.
5. An iteratively refined prompt that handles noisy and adversarial input text without hallucinating or leaking formatting.

## Verification Checklist

1. **Structured Prompt**:
   - Paste the structured incident prompt into Gemini.
   - Confirm the response contains exactly one summary paragraph and two bulleted next steps.
   - Confirm no internal server hostnames (`db-prod-04`) or engineer names appear in the output.
   - Confirm word count is under 120 words.

2. **Persona Shift**:
   - Run the CISO prompt: output focuses on enterprise risk, regulatory impact, and high-level timelines without low-level command logs.
   - Run the Security Engineer prompt: output focuses on root cause, reproduction commands, patch validation, and specific CVE or payload details.

3. **Schema Enforcement**:
   - Run the JSON extraction prompt.
   - Confirm the output is valid, parseable JSON matching the schema with keys `tasks`, `task_id`, `description`, `owner`, and `due_date`.
   - Confirm the model omits markdown backticks and conversational greetings when instructed.

4. **Few-Shot Classification**:
   - Run the few-shot prompt with the target test ticket: `"Credit card charged twice for annual subscription renewal."`
   - Confirm Gemini outputs the exact single-line pipe-delimited format: `Category: Billing | Urgency: High | Action: Issue refund or verify duplicate transaction`.

5. **Iterative Refinement**:
   - Run the refined prompt against noisy notes containing unrelated banter and unverified rumors.
   - Confirm Gemini extracts only grounded facts, ignores conversational noise, and outputs the requested schema.

## Built With

- Google Gemini (Gemini 1.5 Flash / Gemini 2.0 Flash web interface at `gemini.google.com`)
- Verified date: 2025-05-15
- Unverified: Specific future UI redesigns of the consumer Gemini web interface.
