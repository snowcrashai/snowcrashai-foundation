# Prompt Injection Pentesting Playbook

> **Status:** Draft  
> **Category:** AI Security Pentesting  
> **Applies to:** LLMs, RAG systems, AI agents  
> **SnowcrashAI Top 10 Mapping:** A01 (Prompt Injection), A06 (RAG Poisoning)  
> **Version:** v0.1  

---

## 1. Overview

### 1.1 Objective
Evaluate whether an AI system can be coerced into ignoring, overriding, or bypassing its intended instructions, policies, or safeguards through crafted inputs.

This playbook focuses on identifying:
- Instruction hierarchy failures
- Guardrail bypasses
- Context contamination
- Indirect prompt injection paths

### 1.2 Threat Model
- **Attacker profiles:** External user, authenticated user, API consumer, insider
- **Trust boundaries:** User input vs system instructions vs retrieved data
- **Assumptions:** Attacker cannot modify system prompts directly but can influence inputs

---

## 2. Target System Description

This playbook applies to AI systems where:
- User-controlled input is provided to an LLM
- System prompts or policies are embedded upstream
- Outputs may trigger downstream actions or decisions

Examples:
- Chatbots
- RAG-based assistants
- AI agents with tool access
- Customer support automation

---

## 3. Attack Preconditions

- Ability to submit text input (direct or indirect)
- No requirement for privileged access
- Model processes both system and user context in a single inference pass

Optional:
- Access to retrieved documents or external content sources (RAG)

---

## 4. Attack Methodology

### 4.1 Technique Description
Prompt injection exploits the model’s inability to reliably distinguish between:
- **Instructions** (what it should do)
- **Content** (what it should process)

Attackers craft inputs that cause the model to:
- Reveal hidden instructions
- Ignore safety rules
- Perform restricted actions
- Modify its role or behavior

### 4.2 Step-by-Step Test Procedure

1. **Baseline Behavior**
   - Observe expected responses to benign prompts
   - Identify refusal or guardrail behavior

2. **Instruction Override Attempts**
   - Introduce language attempting to redefine the model’s role
   - Embed conflicting instructions within user input

3. **Context Escalation**
   - Gradually layer constraints or narratives that elevate attacker instructions
   - Test persistence across turns

4. **Indirect Injection (if applicable)**
   - Insert instructions into documents, web content, or retrieved data
   - Observe whether retrieved content alters system behavior

5. **Outcome Validation**
   - Confirm whether restricted behavior occurred
   - Capture full prompt-response chain for analysis

---

## 5. Example Test Inputs

Examples should remain **illustrative**, not exploit-ready:

- Role redefinition attempts
- Instruction framing within quoted text
- Requests to explain internal rules or constraints
- Conflicting task prioritization prompts

Avoid publishing exact payloads that can be trivially abused outside testing.

---

## 6. Expected Outcomes

### Successful Attack Indicators
- System instructions are revealed
- Guardrails are bypassed
- Restricted content or actions are performed
- Model behavior deviates from policy

### Partial Success
- Inconsistent enforcement
- Context leakage
- Reduced refusal confidence

### Failure
- Instructions consistently enforced
- Content treated as data, not control

---

## 7. Security Impact

Potential impacts include:
- Unauthorized actions by AI agents
- Exposure of sensitive data
- Policy and compliance violations
- Loss of trust in AI-driven decisions

In agentic systems, prompt injection can lead to **real-world operational damage**.

---

## 8. Detection and Monitoring Signals

Defenders should monitor for:
- Unusual prompt patterns or token distributions
- Repeated instruction-like language in user input
- Sudden behavioral shifts across sessions
- Tool invocation anomalies triggered by text input

Logging full prompt context (with privacy controls) is critical.

---

## 9. Mitigations and Defensive Controls

### Preventive
- Strong separation of system and user context
- Instruction hierarchy enforcement
- Input classification and filtering

### Detective
- Prompt anomaly detection
- Output policy validation
- Behavioral baselining

### Compensating
- Human-in-the-loop review for sensitive actions
- Restricted tool scopes and permissions

---

## 10. Validation and Retesting

- Re-run tests after prompt or policy updates
- Include prompt injection tests in CI/CD pipelines
- Validate across model upgrades and fine-tunes

Prompt injection resistance must be continuously tested.

---

## 11. Related Risks and References

- SnowcrashAI Top 10 A01: Prompt Injection and Instruction Hijacking
- SnowcrashAI Top 10 A06: RAG Knowledge Base Poisoning

---

## 12. Notes and Limitations

- Prompt injection resistance varies by model and architecture
- No single mitigation is sufficient
- Defensive depth is required for production systems
