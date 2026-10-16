---
name: implement-step-by-step
description: Manages the entire lifecycle of a project plan. It reads or creates a comprehensive IMPLEMENTATION.md, analyzes system-wide dependencies, and executes exactly one sequential micro-step with strict human validation.
---

<what-to-do>

You are operating under strict sandbox constraints to prevent architectural drifting or sprinting ahead. When the user runs `/step-by-step`, execute this precise workflow:

### Phase 1: Initialize or Read the Plan
1. **Check for Existing Plan:** Look for `IMPLEMENTATION.md` or `IMPLEMENTATION.md` in the workspace root.
2. **Create If Missing:** If it does not exist, interview the user by asking clarifying questions *one at a time* regarding project scope, target models, scaling requirements, and infrastructure bounds. Use this information to write the file using the schema below.
3. **Reformat if Not Aligned:** If the file is present but does not follow the format as outlined below, rewrite to ensure it does follow the prescribed outline below. Ensure that it is ordered so that each step can be completed satisfactorily without needed any of the subsequent steps needing to be completed i.e. the order can be followed sequentially. 
4. **Analyze Holistic Context:** If the file exists, read the entire document from top to bottom before modifying code. You must identify cross-phase dependencies (e.g., verifying that the target LLM model size matches the allocated storage volumes or hardware tier specified in the infrastructure steps). If information is missing or mismatched, pause and ask the user to clarify.

### Phase 2: Execute the Next Micro-Step
1. **Locate the Task:** Identify the very first uncompleted checkbox (`- [ ]`) in the plan. Strictly ignore all subsequent tasks.
2. **Explain Intent:** Before making any file changes, explicitly print out the specific files you intend to create or modify for this single task, along with a brief explanation of why.
3. **Execute:** Perform the exact code modifications, file creations, or configuration changes required for this single step. Do not touch, refactor, or optimize anything unrelated.
4. **Validate:** Execute the exact verification step or command specified under the **Validation** block for this specific task.
5. **Update State:** Modify the plan file inline, changing that specific task's checkbox from uncompleted (`- [ ]`) to completed (`- [x]`).
6. **Yield Control:** Output a precise summary of the changes made, present validation command outputs, and explicitly state that you are stopping for review. Ask the user for permission to proceed. Do not execute further actions until explicitly instructed to do so by the user.
7. **Repeat:** Repeat the entire process above until all items have been completed or the user has halted the process.

</what-to-do>

<supporting-info>

## Required Blueprint Structure

The `IMPLEMENTATION.md` file must strictly follow this schema:

```markdown
# Implementation Plan: [Project Name]

## Project Description
[Provide a detailed, explicit description of the project, including architecture, target software/models, constraints, and exactly what is going to be built. This section must contain enough structural context for the agent to validate step dependencies.]

## Phase 1: Pre-flight & Configurations
- [ ] Step 1.1: [Descriptive Title]
  - **Details:** [Precise files to modify/create, configurations to apply, or code structures to build]
  - **Validation:** [The specific local check, CLI command, or test script required to verify success]

## Phase 2: Core Development
- [ ] Step 2.1: [Descriptive Title]
...