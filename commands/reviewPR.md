---
description: Automatically review GitHub PR with code quality and architecture analysis
---

# Review PR Command

You are responsible for conducting a comprehensive review of a GitHub Pull Request. Your goal is to analyze code changes, check code quality, verify architectural consistency, and provide actionable improvement suggestions.

## 0. Use worker agents for parallel execution

## 1. Obtain PR Information

### Step 1.1: Determine PR Number

**If the user provides a PR number** (e.g., `/tr:reviewPR 123`):

- Use the provided PR number directly

**If no PR number is provided**:

- Use worker agent to run `gh pr status` to check if the current branch has an associated PR
- If a PR is found, extract its number
- If no PR is found, inform the user and ask them to provide a PR number

### Step 1.2: Fetch PR Details

Use worker agent to run the following commands in parallel:

- `gh pr view <PR_NUMBER> --json title,body,author,baseRefName,headRefName,commits,files`
- `gh pr diff <PR_NUMBER>`

## 2. Parallel Analysis Phase

Deploy 2-3 scout agents concurrently to analyze different aspects of the PR:

### Scout A: Code Quality Analysis

**Responsibility**: Analyze code quality issues in the PR

**Research Questions**:

1. Are there any code style inconsistencies or violations of project conventions?
2. Are there overly complex functions or methods that should be refactored?
3. Are there duplicated code blocks that could be abstracted?
4. Are variable and function names clear and semantic?
5. Is error handling implemented properly?

### Scout B: Architecture Consistency Check

**Responsibility**: Verify that PR changes align with project architecture

**Research Questions**:

1. Do the changes follow the existing project structure and module organization?
2. Are new dependencies introduced? Are they necessary and appropriate?
3. Do the changes follow established design patterns in the codebase?
4. Are there any violations of separation of concerns or SOLID principles?
5. How do the changes integrate with existing components/modules?

### Scout C (Optional): Test Coverage and Documentation

**Responsibility**: Check test coverage and documentation quality

**Research Questions**:

1. Are new features or bug fixes accompanied by appropriate tests?
2. Are edge cases and error scenarios covered in tests?
3. Is the code properly documented (comments, docstrings, README updates)?
4. Are there breaking changes that need to be documented?

## 3. Synthesize Analysis Results

After all scout agents complete their investigation:

1. **Integrate Reports**: Combine findings from all scout agents
2. **Identify Critical Issues**: Categorize findings by severity:
   - 🔴 Critical: Must be fixed (security issues, breaking changes, major bugs)
   - 🟡 Important: Should be fixed (code quality, architecture violations)
   - 🟢 Suggestions: Nice to have (minor improvements, style suggestions)
3. **Generate Improvement Suggestions**: For each identified issue, provide:
   - Clear description of the problem
   - Explanation of why it matters
   - Specific code suggestions or refactoring approaches
   - Code examples where applicable

## 4. Generate Review Comment

Create a structured review comment in the following markdown format:

```markdown
## PR Review Summary

### Overview

[Brief summary of the PR's purpose and scope]

### Code Quality Analysis

[Findings from Scout A]

- ✅ Strengths: [What was done well]
- ⚠️ Issues Found: [List of code quality issues with severity indicators]

### Architecture Consistency

[Findings from Scout B]

- ✅ Alignment: [How changes align with existing architecture]
- ⚠️ Concerns: [Architectural issues or inconsistencies]

### Test Coverage & Documentation

[Findings from Scout C if applicable]

- ✅ Coverage: [Test coverage status]
- ⚠️ Gaps: [Missing tests or documentation]

### Detailed Recommendations

#### 🔴 Critical Issues

[List critical issues that must be addressed]

#### 🟡 Important Improvements

[List important improvements]

#### 🟢 Suggestions

[List optional suggestions for enhancement]

### Conclusion

[Overall assessment and recommendation: APPROVE / REQUEST_CHANGES / COMMENT]

---

🤖 Generated with Claude Code Review Assistant
```

## 5. Submit Review

Use worker agent to submit the review comment:

1. **Preview the review**: Show the generated review comment to the user
2. **Ask for confirmation**: Use AskUserQuestion to ask the user:

   - "Submit this review to GitHub?"
   - "Modify the review before submitting?"
   - "Cancel and exit"

3. **If user confirms submission**:
   - Determine review state based on findings:
     - `APPROVE` if no critical or important issues found
     - `REQUEST_CHANGES` if critical issues exist
     - `COMMENT` if only suggestions exist
   - Run: `gh pr review <PR_NUMBER> --<state> --body "<review_comment>"`

## Important Notes

- **Evidence-Based**: All findings must be based on actual code analysis, not assumptions
- **Constructive Tone**: Feedback should be constructive and actionable
- **Code Examples**: Provide specific code examples for suggested improvements
- **Context Awareness**: Consider the PR's context (bug fix, new feature, refactor, etc.)
- **Project Standards**: Base recommendations on the project's existing conventions and patterns
- **Respect Author**: Be respectful and acknowledge good practices in the PR
- **Security Focus**: Pay special attention to potential security vulnerabilities
- **Performance Impact**: Consider performance implications of the changes

## Error Handling

- **No gh CLI**: If `gh` command is not available, inform the user to install GitHub CLI
- **Authentication Issues**: If `gh` authentication fails, guide the user to run `gh auth login`
- **PR Not Found**: If PR doesn't exist, inform the user and ask for a valid PR number
- **API Rate Limiting**: If GitHub API rate limit is hit, inform the user and suggest trying later
