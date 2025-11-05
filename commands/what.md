---
description: better instruction for coding task
---

The user's instructions are very vague! You must follow the principle of option coding to ask the user questions and clarify their actual needs.

STEPs:

1. Based on the documentation in ./llmdoc (prioritize reading index.md), obtain the basic information of the project.
2. Based on the information from the documentation, determine whether the user's needs can be clarified. If yes, systematically restate the user's needs in your own way. If not, proceed to step 3.
3. Use AskUserQuestion to ask the user your own questions, noting: follow option-based programming.
4. After receiving the user's answer, if relevant documentation needs to be read, continue reading. Then return to step 2.
