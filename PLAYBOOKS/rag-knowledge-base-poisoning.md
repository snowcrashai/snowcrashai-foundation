# RAG Knowledge Base Poisoning Pentesting Playbook

> **Status:** Draft  
> **Category:** AI Security Pentesting  
> **Applies to:** RAG systems, enterprise AI assistants, agentic workflows  
> **SnowcrashAI Top 10 Mapping:** A06 (RAG Knowledge Base Poisoning), A01 (Prompt Injection)  
> **Version:** v0.1  

---

## 1. Overview

### 1.1 Objective
Assess whether an AI system using Retrieval-Augmented Generation (RAG) can be manipulated through poisoned, malicious, or adversarial knowledge sources to influence model behavior, outputs, or downstream actions.

This playbook focuses on:
- Data-layer instruction injection
- Trust abuse of retrieved content
- Integrity failures in knowledge ingestion pipelines
- Context contamination via retrieval

---

### 1.2 Threat Model
- **Attacker profiles:** External contributor, insider, compromised data source, supply-chain attacker
- **Trust boundaries:** Knowledge ingestion → retrieval → prompt assembly → generation
- **Assumptions:** Retrieved content is implicitly trusted by the model unless explicitly controlled

---

## 2. Target System Description

Applicable to AI systems where:
- External or internal documents are indexed for retrieval
- Retrieved content is appended to prompts or context windows
- Users rely on retrieved information for decisions or actions

Examples:
- Enterprise knowledge assistants
- Policy or compliance chatbots
- Search-augmented LLM tools
- Agent systems consuming retrieved instructions

---

## 3. Attack Preconditions

One or more of the following:
- Ability to influence documents ingested into the knowledge base
- Ability to modify or upload content (directly or indirectly)
- Compromise of upstream content sources
- Weak validation or trust assumptions in ingestion pipelines

No direct access to system prompts is required.

---

## 4. Attack Methodology

### 4.1 Technique Description
RAG poisoning exploits the fact that:
- Retrieved content is treated as **authoritative**
- Models struggle to distinguish **instructions** from **reference material**
- Retrieval systems prioritize semantic similarity, not trustworthiness

Attackers embed malicious instructions, misleading guidance, or adversarial phrasing into documents that are later retrieved and injected into the model’s context.

---

### 4.2 Step-by-Step Test Procedure

1. **Baseline Retrieval Behavior**
   - Identify which documents are retrieved for common queries
   - Observe how retrieved content influences responses

2. **Poison**
