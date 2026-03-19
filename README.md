## Overview

This repository demonstrates a strict, product-oriented evaluation rubric for large language model outputs. The framework prioritizes instruction adherence, referential consistency, and internal logical coherence, with an emphasis on failure modes that impact real-world usability.

The goal is to model how a linguistically informed evaluator might assess LLM behavior in production-facing environments.

## Status

This project is a work in progress. Initial rubric and diagnostic prompt set have been defined. Model output collection and scoring analysis are in progress.

## Results Summary

Across three evaluation scenarios, both models performed well on structured output tasks but showed consistent weaknesses in handling underspecified prompts.

### Key Observations

- Both models successfully generated structured JSON outputs, though occasional formatting or verbosity issues appeared.
- Referential consistency errors occurred in multi-entity scenarios, particularly around role tracking and pronoun clarity.
- Neither model asked clarifying questions when given underspecified instructions, instead making implicit assumptions (e.g., defaulting to Python).

### Takeaway

These results suggest that while modern LLMs are strong at execution, they still struggle with ambiguity detection and clarification, which has implications for reliability in production systems.
