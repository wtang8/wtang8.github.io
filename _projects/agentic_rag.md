---
layout: page
title: Agentic GCSE Physics Tutor
description: Knowledge-Graph and Symbolic AI Tutoring System
img: assets/img/agentic_rag.jpg
importance: 4
category: work
---

An **Agentic GCSE Physics Tutor** designed to generate, evaluate, and guide students through physics questions. It integrates Large Language Models (Gemini) with symbolic logic and structured knowledge graphs to ensure mathematical correctness and mitigate hallucinations.

> **Code Availability:** This is a private codebase developed for personal research. Detailed system walkthroughs and repository access are available upon request/interview.

### Core Objectives
*   **Deterministic Calculations:** Mitigates numerical errors by anchoring LLM calculations in symbolic engines rather than raw parameter memory.
*   **Structured Pedagogical Routing:** Uses a state machine to navigate conversation states, student hints, and variable difficulty levels.
*   **Formulas & Input Guardrails:** Programmatically audits student formulas and mathematical inputs against exact algebraic rules before LLM execution.

The system coordinates conversation state and symbolic anchors through two distinct execution paths:

* **The Conceptual Path:** When a student asks a qualitative question, the system queries the **NetworkX Physics Graph** to retrieve verified formulas, definitions, and curriculum-aligned relations. This data is injected directly into the LLM context to ground the response and prevent factual hallucinations.
* **The Mathematical Path:** When a student submits a formula or numerical step, the input is intercepted by the `FormulaValidator` to check for structural correctness (e.g., checking variable mappings). It is then solved exactly by the **SymPy engine** to generate deterministic evaluation and feedback.

### Core Components

1.  **Orchestration & State Management (LangGraph & LangChain):** Routes the tutoring conversation, maintains user states (e.g., active problem, hint preferences), and handles tool executions.
2.  **Knowledge Graph Engine (NetworkX):** Maps 329 physical concepts and 534 edges (Edexcel GCSE curriculum) from structured configuration files (YAML) to programmatically anchor physics formulas.
3.  **Symbolic Math Solver (SymPy):** Powers a custom `ProblemEngine` handling derivations, formula verification, and exact arithmetic (achieving a 99.1% success rate on test harnesses).
4.  **Formula Validation (`FormulaValidator`):** Structurally analyzes student formulas and inputs. If a student mentions irrelevant variables, the system catches it and provides deterministic feedback.
