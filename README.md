# Cursor Playbooks

A centralized collection of Cursor Rules and Skills that standardize development workflows, enforce engineering best practices, and improve consistency across teams.

## Overview

As teams increasingly adopt AI-assisted development, maintaining consistency, quality, and shared engineering standards becomes critical.

This repository serves as a single source of truth for reusable Cursor Rules and Skills that help developers:

* Follow established coding standards
* Reduce repetitive prompting
* Capture and share team knowledge
* Automate common development workflows
* Improve consistency across AI-generated code
* Accelerate onboarding and productivity

---

## What are Rules?

Rules provide persistent guidance to Cursor and define how AI should behave within a project.

Typical use cases include:

* Coding standards
* Naming conventions
* Architecture guidelines
* Logging requirements
* Testing expectations
* Documentation standards

### Example

```text
Always use pytest for Python tests.
Follow the Arrange-Act-Assert pattern.
Add type hints to all public functions.
Use structured logging.
```

**Rules answer:**

> How should code be written?

---

## What are Skills?

Skills are reusable workflows that teach Cursor how to perform specific tasks.

Typical use cases include:

* Generate unit tests
* Create API endpoints
* Perform code reviews
* Investigate failing tests
* Write release notes
* Generate database migrations

### Example

```text
Generate comprehensive unit tests:
1. Identify happy paths
2. Test edge cases
3. Validate error handling
4. Mock external dependencies
5. Ensure branch coverage
```

**Skills answer:**

> How should a task be performed?

---

## Rules vs Skills

| Rules                 | Skills                  |
| --------------------- | ----------------------- |
| Define standards      | Define workflows        |
| Project-wide guidance | Task-specific expertise |
| Ensure consistency    | Improve productivity    |
| Applied automatically | Used when needed        |
| Act as guardrails     | Act as playbooks        |


---

## Goals

* Standardize AI-assisted development
* Promote engineering best practices
* Capture institutional knowledge
* Reduce repetitive prompts
* Improve code quality
* Increase developer productivity

---

## Contributing

When adding a new Rule or Skill:

### Rules

* Keep them concise and actionable
* Focus on project-wide standards
* Avoid task-specific instructions
* Ensure they are broadly applicable

### Skills

* Define a clear objective
* Include repeatable workflows
* Break tasks into logical steps
* Document expected outputs

---
