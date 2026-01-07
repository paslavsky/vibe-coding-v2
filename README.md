# vi2: Cursor AI Workflow Commands

Structured commands for Cursor AI to manage complex development tasks using the **vi2** framework.

### Summary
The **vi2** framework manages LLM-driven development through a temporary `./.vi2/` directory. It maintains a knowledge snapshot (`llm_context.md`), an execution checklist (`tasks.md`), and a question log (`questions.md`). This ensures consistency and code stability across multiple AI interactions.

### Command List

| Command | Purpose | When to Use |
| :--- | :--- | :--- |
| `/vi2-plan` | **Setup** | Analyze requirements and generate the initial plan. |
| `/vi2-do-next` | **Execute** | Implement the next available task from the checklist. |
| `/vi2-status` | **Monitor** | Check project progress and identify blockers. |
| `/vi2-test` | **Verify** | Run tests and analyze code coverage. |
| `/vi2-review` | **Audit** | Review recently implemented code for quality and bugs. |
| `/vi2-refactor` | **Clean** | Systematically improve code and reduce technical debt. |
| `/vi2-update` | **Adjust** | Integrate new requirements into the existing plan. |
| `/vi2-rollback` | **Revert** | Restore the codebase to a previous stable state. |
| `/vi2-debrief` | **Process** | Update the plan based on answers to previous questions. |
| `/vi2-validate` | **Check** | Verify the integrity of internal framework files. |
| `/vi2-done` | **Finish** | Generate a final report and remove the `./.vi2/` directory. |

### Usage Example

1.  **Initialize:** `@codebase Create a REST API. /vi2-plan`
2.  **Develop:** `/vi2-do-next` (Repeat for each task)
3.  **Change:** `Change the API to use GraphQL instead. /vi2-update`
4.  **Finalize:** `/vi2-done`

### License
Distributed under the [MIT License](LICENSE).
