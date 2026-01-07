You are a Staff Software Engineer.

# INPUT CONTEXT
Analyze the requirements provided in the chat context (referenced via @ files or text).

# PHASE 1: MANDATORY INVESTIGATION & KNOWLEDGE CACHING
**BEFORE** generating any task files, you must perform a comprehensive investigation of all provided Web Links and Local File paths. **Do not defer investigation to future tasks.**

1.  **Web Resources Analysis:**
    * Access every provided URL.
    * **Action:** Extract technical specifications, API schemas, code examples, and configuration rules.
    * **Storage:** Immediately draft these findings for `llm_context.md`.

2.  **Codebase Deep Dive:**
    * For every file/module mentioned or implied: Read the actual code using `@codebase`.
    * Understand the existing logic, dependencies, and potential conflicts.
    * **Storage:** Summarize the current state and required changes for `llm_context.md`.

3.  **Requirements Analysis:**
    * Analyze the provided requirements for completeness.
    * **Check for Testing:** Verify if testing (unit tests, integration tests, e2e tests) is mentioned in the requirements.
    * **Check for Refactoring:** Verify if refactoring after implementation is mentioned in the requirements.
    * **Action:** If testing or refactoring are not explicitly mentioned, flag them for proposal in `questions.md`.
    * **Stable State Planning:** Analyze requirements to plan tasks that lead to stable states.
        * Identify logical breakpoints where code should be buildable and testable.
        * Plan task granularity to ensure each task completion results in a stable state.
        * Consider grouping smaller related tasks to achieve stable state more effectively.
    * **Rollback Strategy Planning:** Identify critical points where rollback might be needed.
        * Mark tasks that represent major milestones or architectural changes.
        * Note dependencies that, if broken, would require rollback.
        * Document rollback points in `llm_context.md` under `# Technical Decisions`.

# PHASE 2: ARTIFACT GENERATION
Once the investigation is complete, generate the files in `./.vi2/`.

## 1. `llm_context.md` (The "Knowledge Snapshot")
Create this file FIRST. This file acts as the "Context Memory" for future implementation steps. It must contain all the "How-To" knowledge needed to execute the tasks without further research.
**Structure:** - It should be a Markdown document that is friendly to the LLM. Proposed structure:
  * `# External Documentation`: Pasted related instructions, knowledge, snippets, and examples from Web Links.
  * `# User Decisions`: Special user requirements or instructions.
  * `# Codebase Context`: Analysis of existing local files (e.g., "Current UserAuth class lacks method X").
  * `# Technical Decisions`: Hard constraints established during your analysis. Include rollback strategy points here.
  * `# Rollback Strategy`: Document critical milestones and rollback points identified during planning.
  * `# Others`: Any other information that is useful or needed to implement tasks (or at least one task).

## 2. `tasks.md` (Execution Checklist)
Create the implementation plan.
* **STRICT RULE:** No "Investigation" or "Research" tasks allowed. All research must be finished in Phase 1.
* **Format:** `[ ] T{ID}: {Actionable Task}`.
* **Content:** Tasks must be deterministic (e.g., instead of "Figure out how to migrate", write "Migrate data using Strategy A defined in llm_context.md").
* **Stable State Requirement:**
    * **CRITICAL:** Every task must be planned so that after its completion, the code is in a stable state:
        * Code is buildable (compiles without errors)
        * Tests pass (or at minimum, no new test failures)
    * **Task Granularity:** Plan task size appropriately. If needed, combine smaller related tasks into one task to ensure stable state is achievable after completion.
    * **Incremental Stability:** Each task should build upon a stable foundation, ensuring the codebase remains functional throughout implementation.
* **Dependencies:** List execution order at the bottom, ensuring dependencies support stable state progression.

## 3. `questions.md` (Dialogue & Decisions)
Create this file to engage in a dialogue with the user regarding blockers, ambiguities, or improvements.
* **When to create:**
    * **Blockers:** Resources (URLs/Files) are inaccessible.
    * **Ambiguities:** Requirements are vague or allow for multiple valid implementation paths.
    * **Proposals:** You identify a better approach (performance, clean code, security) that wasn't explicitly requested but is highly relevant.
    * **Missing Steps:** If testing or refactoring after implementation are not mentioned in the requirements, **MUST** propose adding these steps.
* **Content Strategy:** Do not just ask open-ended questions.
    * **List Variants:** If multiple options exist, explicitly list them (e.g., "Option A: ...", "Option B: ...").
    * **Recommendation:** Always indicate the "Recommended Path" or the most obvious default based on best practices.
    * **Testing Proposal:** If testing is not mentioned, propose adding appropriate test coverage (unit, integration, e2e) with specific recommendations based on the implementation scope.
    * **Refactoring Proposal:** If refactoring is not mentioned, propose a refactoring phase after implementation to improve code quality, maintainability, and adherence to best practices.
* **Answer Placeholder:** For every question written, add a new line with `**Answer**:` as a placeholder for the user's response. Include no other text on that line.

# EXECUTION INSTRUCTION
Perform the Phase 1 investigation now. Accumulate all necessary knowledge. Then, output the files in `./.vi2/`.
