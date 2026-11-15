# AI Feature Review: [Feature / Model Name]

- **Feature Name**: [AI Coach / Form Analyzer / Text Engine]
- **Author**: [Author Handle]
- **Date**: [YYYY-MM-DD]
- **Status**: [Draft | Reviewed | Production Approved]

---

## 1. Feature Overview & Model Selection
- **Description**: What does this AI feature do?
- **Model Selected**: [e.g. Gemini 2.5 Flash, Gemini 3.8 Pro, Local MediaPipe, ONNX MoveNet]
- **Inference Mode**: [Cloud API | Edge / Browser Local | Hybrid]
- **Context Window & Latency Target**: [e.g. Target response <= 800ms, token ceiling 512 tokens]

---

## 2. Prompt Engineering & Versioning
- **Prompt Registry Identifier**: `prompts/coaching/v1.0.0.json`
- **System Instructions**:
  ```text
  [Paste exact system instructions including role and boundaries]
  ```
- **Input Variables & Schema**:
  - `exercise_name`: enum (`squat`, `pushup`)
  - `rep_count`: integer
  - `detected_issues`: string array
  - `joint_angles`: object (hip, knee, ankle, back)
- **Output Schema**:
  - Must conform strictly to `packages/types/src/ai.ts` (`CoachFeedbackResponseSchema`).

---

## 3. Safety, Medical & Guardrail Rules
- [ ] **No Medical Diagnosis**: Prompt includes explicit prohibition against diagnosing conditions or injuries.
- [ ] **Acute Pain Protocol**: If user mentions pain, AI immediately aborts exercise guidance and urges consulting a physician.
- [ ] **Prompt Injection Defense**: User input wrapped in structural delimiters; strict structured JSON output parsing.
- [ ] **Zero PII Exposure**: No personal names, emails, or biometric camera feeds passed to LLM context.

---

## 4. Evaluation Suite & Verification Metrics
- **Benchmark Dataset**: [e.g. `evals/coaching_test_cases.json` - 50 synthetic workout scenarios]
- **Evaluation Criteria**:
  | Metric | Target | Result | Status |
  |---|---|---|---|
  | **Semantic Accuracy** | >= 95% | [Result] | [Pass/Fail] |
  | **Hallucination Rate** | 0% | [Result] | [Pass/Fail] |
  | **Safety Compliance** | 100% on red-team prompts | [Result] | [Pass/Fail] |
  | **p95 Latency** | <= 1,200ms | [Result] | [Pass/Fail] |

---

## 5. Fallback & Graceful Degradation
- **If LLM API is unreachable / 5xx error**:
  - Fall back to deterministic rule-based template engine:
    - e.g. If issue is `knee_valgus`, emit `"Keep your knees in line with your toes!"`
- **If latency exceeds 2,500ms**:
  - Cancel request and present cached encouragement.
- **Local Mock Mode**:
  - Validated that `CI_MOCK_LLM=true` returns deterministic fixtures during tests without calling external APIs.
