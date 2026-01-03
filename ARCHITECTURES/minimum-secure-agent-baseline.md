# Minimum Secure Agent Baseline

> **Status:** Draft  
> **Category:** AI Security Baseline  
> **Applies to:** AI agents, LLM-based automation, tool-enabled AI systems  
> **Version:** v0.1  

---

## 1. Purpose

This document defines the **Minimum Secure Agent Baseline** — a set of **non-optional security controls** required for deploying AI agents safely in production environments.

It is intended to provide:
- A clear adoption threshold
- A defensible security baseline
- A checklist suitable for audit, compliance, and third-party risk reviews

This baseline is **derived directly** from SnowcrashAI playbooks, reference architecture, and assurance metrics.

---

## 2. Baseline Applicability

This baseline applies to AI systems that:
- Accept natural language input
- Perform reasoning or planning
- Invoke tools, APIs, or automated actions
- Influence real-world decisions or operations

If an AI system can **act**, this baseline applies.

---

## 3. Mandatory Control Domains

### 3.1 Prompt and Instruction Controls

**Required Controls**
- System instructions are immutable and isolated from user input
- User content is clearly separated from control instructions
- Prompt injection testing is performed prior to production

**Baseline Requirement**
- ❑ Instruction hierarchy enforced
- ❑ Prompt injection playbook executed
- ❑ Prompt context logged (with privacy controls)

**Mapped Risks**
- Prompt Injection (A01)

---

### 3.2 Retrieval and Knowledge Integrity (If RAG Is Used)

**Required Controls**
- All retrieved content has provenance metadata
- Instruction-like content in documents is sanitized or filtered
- RAG poisoning testing is performed

**Baseline Requirement**
- ❑ Trusted sources defined
- ❑ Retrieval logs enabled
- ❑ RAG poisoning playbook executed

**Mapped Risks**
- RAG Knowledge Base Poisoning (A06)

---

### 3.3 Deterministic Authorization

**Required Controls**
- AI models do not authorize actions
- A deterministic policy engine evaluates all actions
- Deny-by-default logic is enforced

**Baseline Requirement**
- ❑ Policy engine implemented
- ❑ Role- and context-based authorization
- ❑ Explicit allowlists for actions

**Mapped Risks**
- Agent Tool Abuse (A05)

---

### 3.4 Tool and Action Execution Controls

**Required Controls**
- Tools operate with least-privilege credentials
- Sensitive actions require human approval
- Tool usage is rate-limited and monitored

**Baseline Requirement**
- ❑ Scoped credentials per tool
- ❑ Approval gates for high-risk actions
- ❑ Tool invocation logging enabled

**Mapped Risks**
- Unauthorized actions
- Privilege escalation

---

### 3.5 Monitoring, Logging, and Auditability

**Required Controls**
- End-to-end traceability from input to action
- Logs are tamper-resistant
- Actions are attributable to prompts and decisions

**Baseline Requirement**
- ❑ Trace IDs across all layers
- ❑ Immutable audit logs
- ❑ Prompt → decision → action correlation

**Mapped Risks**
- Silent failures
- Undetected misuse

---

### 3.6 Operational Security and Resilience

**Required Controls**
- Security tests re-run after model or tool changes
- Behavioral drift is monitored
- Controls are periodically revalidated

**Baseline Requirement**
- ❑ Regression testing cadence defined
- ❑ Drift monitoring in place
- ❑ Change management enforced

**Mapped Risks**
- Security regression
- Control degradation over time

---

## 4. Baseline Compliance Assessment

Baseline compliance may be evaluated as:
- **Compliant** — All required controls implemented
- **Conditionally Compliant** — Controls present with documented compensating measures
- **Non-Compliant** — One or more mandatory controls missing

This baseline is intentionally **binary at the control level**.

---

## 5. Relationship to SnowcrashAI Artifacts

| Artifact | Role |
|---|---|
| SnowcrashAI Top 10 | Risk identification |
| Pentesting Playbooks | Control validation |
| Secure Agent Reference Architecture | Control design |
| Assurance Metrics | Evidence collection |
| **Minimum Secure Agent Baseline** | Adoption threshold |

---

## 6. Summary

AI agents must not be deployed based on trust in prompts or models alone.

This baseline defines the **minimum controls required** to ensure AI systems:
- Act within authorization boundaries
- Resist manipulation
- Remain observable and auditable
- Maintain security over time

Anything less represents **unmanaged operational risk**.
