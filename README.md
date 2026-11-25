# MARA — Multimodal Agentic Robotics Assistant

**Status:** Private Research & Commercial-Development Project  
**Author:** Inderpratap Singh  
**License:** Copyright © 2026 Inderpratap Singh. All Rights Reserved. *(Source code is private)*

MARA is a Python robotics simulation and interaction framework. It accepts natural-language commands, parses them into structured goals, builds validated task graphs, and executes them against a stateful simulation backend with resource-aware gripper allocation and human-in-the-loop confirmation.

---

## Core Architecture & Workflow

MARA operates on a **Perception–Reasoning–Planning–Action (PRA)** cycle:

1. **Natural Language Parsing:** Translates user instructions into structured goals.
2. **Deterministic Task Graph Planning:** Converts goals into a dependency-ordered execution plan.
3. **Safety & Validation:** Checks for dependency cycles, invalid arguments, and dual-gripper resource feasibility before execution.
4. **Human-in-the-Loop Confirmation:** Displays a sanitized action proposal and gripper allocation to the user via a **Streamlit** dashboard before acting.
5. **Deterministic Execution:** Runs steps in dependency order—allocating, reserving, and releasing grippers while isolating failed branches.
6. **Stateful Memory:** Observes the simulated world state and updates episodic/semantic memory.

### System Flowchart

```mermaid
flowchart TD
    A[User Natural-Language Command] --> B[Resolve Context & Parse into Goals]
    B --> C{Goals Parsed?}
    C -->|No| D[Request Clarification]
    C -->|Yes| E[Observe Simulated World State & Update Memory]
    E --> F[Build Dependency-Ordered Task Graph]
    F --> G[Validate Plan & Allocate Gripper Resources]
    G --> H[Present Safe Proposal to User for Confirmation]
    H -->|Confirmed| I[Execute Commands via Controller]
    I --> J[Update World State & Return Structured Result]
