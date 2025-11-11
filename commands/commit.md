---
description: "Analyzes code changes and generates a conventional commit message."
argument-hint: ""
---

# /commit

This command analyzes staged and unstaged changes to generate a high-quality commit message that follows the project's existing style.

## When to use

- **Use when:** The user wants to commit their changes, e.g., "commit my work", "create a commit".
- **Suggest when:** The user indicates they have finished a task or a set of changes.
- **Example:** "User: I'm done with the changes for the login page." -> Assistant suggests `/commit`.
- **Example:** "User: wrap this up" -> Assistant suggests `/commit`.

## Actions

1.  **Step 1: Gather Git Information**

    - Use a `worker` agent to run the following commands in parallel:
      - `git diff --staged` (to see staged changes)
      - `git diff` (to see unstaged changes)
      - `git status` (to see current branch and file status)
      - `git log --oneline -10` (to understand the project's commit message style)

2.  **Step 2: Analyze Changes and Generate Message**

    - If there are no changes, inform the user and stop.
    - If there are only unstaged changes, ask the user if they want to stage files first.
    - Based on the git information, generate a commit message that:
      - Follows the project's historical style (e.g., conventional commits, emoji usage).
      - Accurately and concisely describes the changes.
      - Explains the "why" behind the change, not just the "what".

3.  **Step 3: Propose and Commit**
    - Use the `AskUserQuestion` tool to present the generated message to the user.
    - Ask if they want to use the message to commit, edit it, or cancel.
    - If the user agrees to commit, run the `git commit -m "<message>"` command.
