---
description: "Conducts an automated review of a GitHub Pull Request."
argument-hint: "[PR number or URL]"
---

# /reviewPR

This command conducts a comprehensive review of a GitHub Pull Request. If no PR number or URL is provided as an argument (`$1`), it attempts to find the PR associated with the current git branch.

## When to use

- **Use when:** The user explicitly asks to review a pull request, e.g., "review this PR", "can you check PR #123?".
- **Suggest when:** The user mentions merging code, a pull request, or asks for a code quality check on a branch that has an open PR.
- **Example:** "User: My feature is ready for review." -> Assistant checks for a PR and suggests `/reviewPR`.
- **Example:** "User: /reviewPR 123"

## Actions

1.  **Step 1: Obtain PR Information**

    - If an argument (`$1`) is provided, use it as the PR identifier.
    - If no argument is provided, use a `worker` agent to run `gh pr status` to find the current branch's PR number.
    - If no PR is found, inform the user and stop.
    - Use a `worker` agent to run `gh pr view <PR_NUMBER> --json ...` and `gh pr diff <PR_NUMBER>` in parallel to fetch PR details.

2.  **Step 2: Parallel Analysis Phase**

    - Deploy `investigator` agents concurrently to analyze different aspects of the PR:
    - **Investigator A (Code Quality):** Analyze style inconsistencies, complexity, duplication, naming, and error handling.
    - **Investigator B (Architecture):** Verify alignment with project structure, new dependencies, design patterns, and separation of concerns.
    - **Investigator C (Tests & Docs):** Check for appropriate test coverage and documentation updates.

3.  **Step 3: Synthesize and Generate Report**

    - Integrate the findings from all investigators.
    - Categorize issues by severity (Critical, Important, Suggestion).
    - Generate a structured review comment in Markdown format, including a summary, detailed recommendations, and an overall assessment.

4.  **Step 4: Submit Review**
    - Use the `AskUserQuestion` tool to show the generated review to the user and ask for confirmation before submitting.
    - If confirmed, use a `worker` agent to run `gh pr review <PR_NUMBER> --<state> --body "<comment>"` to post the review to GitHub.
