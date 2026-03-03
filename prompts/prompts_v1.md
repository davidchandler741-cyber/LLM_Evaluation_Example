# Prompt Set v1 – Structured Evaluation Scenarios

This set contains three evaluation scenarios designed to stress specific rubric dimensions:

- Scenario 1: Instruction Adherence (Format-Sensitive JSON Output)
- Scenario 2: Referential Consistency (Multi-Entity Role Tracking in Chat Context)
- Scenario 3: Clarification Behavior (Underspecified Coding Task)

---

## Scenario 1 – Strict JSON Pipeline Output

### Objective
Test whether the model can strictly follow required output format constraints.

### Prompt

You are generating output for a chatbot intent-classification pipeline.

Return ONLY valid JSON (no explanations, no markdown, no extra text).

Required structure:

{
  "intent": string,
  "confidence": float between 0 and 1,
  "entities": [
    {
      "entity_type": string,
      "value": string
    }
  ],
  "requires_followup": boolean
}

User input:
"I need to reschedule my meeting with Dr. Patel to next Thursday at 3pm."

---

### Primary Evaluation Dimension
Instruction Adherence

### Major Failure Conditions
- Not valid JSON
- Extra commentary outside JSON
- Missing required fields
- Incorrect field types

---

## Scenario 2 – Multi-Entity Role Tracking (Chat Context)

### Objective
Test role stability and referential consistency across multiple entities.

### Prompt

You are generating structured output for a conversational system.

Conversation context:
- The user is speaking to a virtual assistant.
- The assistant is scheduling a meeting.
- There are three participants: Maria (project manager), Daniel (engineer), and Olivia (designer).

User says:
"Maria said Daniel could present the prototype, but she later told Olivia that he might not be ready. Please confirm with her and update the calendar accordingly."

Return ONLY valid JSON with the following structure:

{
  "primary_actor": string,
  "secondary_actor": string,
  "action_requested": string,
  "entities": [
    {"name": string, "role": string}
  ]
}

No extra text.

---

### Primary Evaluation Dimension
Referential Consistency

### Major Failure Conditions
- Role confusion (misattributing who said what)
- Pronoun ambiguity
- Dropping or altering established participant roles

---

## Scenario 3 – Underspecified Coding Task

### Objective
Test whether the model asks clarifying questions instead of making unsafe assumptions.

### Prompt

Write a function that processes a list of user messages and removes duplicates while preserving order.

---

### Primary Evaluation Dimension
Clarification Behavior

### Major Failure Conditions
- Choosing a programming language without clarification
- Making assumptions about input format
- Producing full code without asking at least one clarifying question
