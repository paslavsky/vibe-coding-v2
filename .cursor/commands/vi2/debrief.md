You are a Staff Software Engineer.

# INPUT CONTEXT
Read and analyze the content of `./.vi2/questions.md`.
Focus on identifying user responses (typically marked with `A:` or written directly below the question).

# PROCESS: INTEGRATION & REFACTORING
Iterate through every Question-Answer pair found in `questions.md`.

## Step 1: Extract & Consolidate Knowledge
For every question that has a clear user answer:
1.  **Update `llm_context.md`:**
    * Translate the user's answer into a technical decision or constraint.
    * Append this to a specific section `# User Decisions` or update existing sections (`# Technical Decisions`, `# Codebase Context`) if relevant.
    * *Critically:* Ensure the knowledge is preserved here or in `tasks.md`, as the question will be deleted.

2.  **Update `tasks.md`:**
    * Review the current task list.
    * Refine, Add, or Remove tasks based on the user's decision.
    * Ensure the "Execution Order" is updated if dependencies have changed.

## Step 2: Clean up `questions.md`
1.  **Resolve & Remove:**
    * If the user's answer allows you to proceed, **DELETE** that entire Question-Answer block from `questions.md`.
    * The goal is to aim for an empty `questions.md`.
2.  **Handle Follow-ups:**
    * If the user's answer creates *new* ambiguities or requires further choice (e.g., "I choose Option A, but how will it affect X?"):
        * Keep the context of the new issue.
        * Formulate a new, specific follow-up question.
        * Append it to the end of the file.
        * **Answer Placeholder:** For every follow-up question written, add a new line with `**Answer**:` as a placeholder for the user's response. Include no other text on that line.
3.  **Unanswered Questions:**
    * Keep any questions that the user has not answered yet.

# OUTPUT INSTRUCTIONS
Apply the changes to the files in `./.vi2/` in the following order:
1.  `llm_context.md` (Update knowledge)
2.  `tasks.md` (Update plan)
3.  `questions.md` (Remove resolved items, add follow-ups)

# STYLE GUIDE FOR QUESTIONS (If adding new ones)
* If new follow-up questions are needed, follow the established format:
    * List Variants (Option A / Option B).
    * Provide a Recommendation.
    * Be specific, avoiding open-ended queries.
    * **Answer Placeholder:** Add a new line with `**Answer**:` as a placeholder for the user's response. Include no other text on that line.
