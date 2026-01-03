# Agent Tool Abuse Pentesting Playbook

> **Status:** Draft  
> **Category:** AI Security Pentesting  
> **Applies to:** AI agents, LLMs with tool/function calling, autonomous workflows  
> **SnowcrashAI Top 10 Mapping:** A05 (Tool and Agent Abuse), A01 (Prompt Injection), A06 (RAG Poisoning)  
> **Version:** v0.1  

---

## 1. Overview

### 1.1 Objective
Assess whether an AI agent with access to tools, APIs, or automated actions can be manipulated into performing unauthorized, unsafe, or unintended operations.

This playbook focuses on:
- Tool misuse via natural language manipulation
- Authorization bypass through agent reasoning
- Over-privileged agent actions
- Cascading failures in autonomous workflows

---

### 1.2 Threat Model
- **Attacker profiles:** External user, authenticated user, insider, compromised upstream system
- **Trust boundaries:** User input → model reasoning → tool invocation → external systems
- **Assumptions:** The agent is permitted to take actions based on model output

---

## 2. Target System Description

Applicable to systems where:
- LLMs can invoke tools or functions
- Agents interact with external APIs, databases, or services
- Actions may have real-world impact

Examples:
- Ticketing or workflow automation agents
- Finance or procurement assistants
- DevOps or infrastructure agents
- Autonomous research or data-gathering agents

---

## 3. Attack Preconditions

One or more of the following:
- Natural language access to the agent
- Insufficient tool-level authorization checks
- Broad or persistent tool permissions
- Lack of human approval for sensitive actions

Attackers do not require direct access to tool credentials.

---

## 4. Attack Methodology

### 4.1 Technique Description
Agent tool abuse exploits the fact that:
- Models reason probabilistically, not authoritatively
- Tool access is often broader than intended
- Natural language can blur intent and authorization

Attackers manipulate the agent’s reasoning to:
- Invoke tools outside intended scope
- Perform actions on behalf of the attacker
- Chain benign actions into harmful outcomes

---

### 4.2 Step-by-Step Test Procedure

1. **Tool Inventory Mapping**
   - Identify available tools and their capabilities
   - Determine permission scope and constraints

2. **Benign Action Baseline**
   - Observe normal tool usage patterns
   - Identify approval or confirmation flows

3. **Intent Manipulation**
   - Use ambiguous or misleading instructions
   - Frame malicious actions as legitimate tasks

4. **Privilege Escalation Attempts**
   - Test whether the agent can exceed intended authority
   - Attempt chained or indirect actions

5. **Outcome Verification**
   - Confirm whether unauthorized actions occurred
   - Capture tool invocation logs and agent reasoning

---

## 5. Example Test Inputs

Illustrative patterns include:
- Requests framed as operational urgency
- Social engineering language
- Multi-step task delegation
- Instruction splitting across turns

Exact payloads should remain abstracted.

---

## 6. Expected Outcomes

### Successful Attack Indicators
- Unauthorized tool invocation
- Actions performed without approval
- Use of tools outside defined scope
- Irreversible external changes

### Partial Success
- Inconsistent enforcement
- Overly permissive confirmations
- Context-dependent failures

### Failure
- Tool access denied
- Human approval enforced
- Clear authorization boundaries respected

---

## 7. Security Impact

Potential impacts include:
- Financial loss
- Data corruption or deletion
- Infrastructure disruption
- Compliance and audit violations

Agent ab
