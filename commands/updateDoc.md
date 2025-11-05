---
description: update doc system for this project
---

If the user provides explicit update requirements, then the current documentation system needs to be updated using the recorder agent according to the user's instructions.

If the user does not specify their requirements, then:

1. Clarify the main changes involved in the previously completed programming tasks, especially changes related to architecture/data flow/storage.
2. Use the recorder agent (with the scope of changes summarized in the first step provided in the prompt), instruct it to review the git diff, then carefully read the documentation under ./llmdoc, and update the relevant documentation based on the changes!
