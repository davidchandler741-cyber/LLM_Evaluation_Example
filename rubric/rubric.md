# LLM Evaluation Rubric (Strict / Product Quality)

## Purpose
This rubric evaluates whether a model response is usable in a product setting. Scores prioritize correctness of execution over style.

## Evaluation Principles
- **Strict, product-quality standard:** Failures that would break usability are penalized heavily.
- **Follow explicit user intent:** The response should optimize for what the user asked for, not what the model prefers.
- **Internal consistency only:** Evaluate logical consistency and constraint adherence within the prompt context (no external fact-checking unless facts are provided).

---

## Dimension 1: Instruction Adherence (Primary)
### Definition
Measures whether the response follows the user’s explicit instructions.

### Major vs Minor Instructions
- **Major instruction:** Any explicit instruction that, if violated, would make the output unusable for the user’s intended purpose.
  - Examples: required output format (e.g., JSON), required structure, required fields, required steps, required constraints necessary for use.
- **Minor instruction:** Preferences that matter but do not break usability if missed.
  - Examples: word count, tone, minor stylistic preferences (unless they’re clearly required for use).

### Scoring
- **3 (Pass):** All major instructions satisfied; minor deviations minimal.
- **2 (Warn):** One minor instruction missed OR small deviation that does not break usability.
- **1 (Fail):** One major instruction missed OR multiple minor misses that significantly reduce usefulness.
- **0 (Severe):** Multiple major violations OR output cannot be used as intended.

---

## Dimension 2: Referential Consistency (High Priority)
### Definition
Measures whether references to people/roles/entities remain stable and clear.

### Failure types prioritized
1. **Role confusion:** Misassigning actions/attributes to the wrong person or role.
2. **Ignoring previously established constraints:** Dropping or contradicting constraints set earlier in the prompt/conversation.
3. **Pronoun ambiguity:** Using pronouns in a way that makes antecedents unclear or misleading.

### Scoring
- **3 (Pass):** References are clear and consistent; constraints maintained.
- **2 (Warn):** Minor ambiguity that is recoverable without rework.
- **1 (Fail):** Confusion/constraint loss that causes likely user error or misinterpretation.
- **0 (Severe):** Contradictions or ambiguity that make the response unreliable or unusable.

---

## Dimension 3: Coherence (Internal Logic)
### Definition
Measures internal logical consistency and completeness of reasoning relative to the prompt.

### Scoring
- **3 (Pass):** Clear, logically consistent, no internal contradictions.
- **2 (Warn):** Slight awkwardness or small gap, but overall consistent.
- **1 (Fail):** Noticeable contradictions or missing logic that harms usefulness.
- **0 (Severe):** Internally inconsistent to the point of failure.

---

## Dimension 4: Clarification Behavior (Preferred When Underspecified)
### Definition
When the prompt is missing key details, the model should ask targeted clarifying questions rather than guessing.

### Scoring
- **3 (Pass):** Asks concise, high-leverage clarifying questions before proceeding.
- **2 (Warn):** Asks some questions but also makes unnecessary assumptions.
- **1 (Fail):** Proceeds with assumptions where clarification is required for correctness.
- **0 (Severe):** Hallucinates details or invents constraints instead of asking.

---

## Overall Rating (Suggested)
- **Strong Accept:** No major misses; scores mostly 3s.
- **Accept with Edits:** Minor issues; no major instruction failures.
- **Reject:** Any major instruction failure, severe referential errors, or unusable output.
