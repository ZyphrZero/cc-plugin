---
description: Generate great doc system for this project
---

Now we need to construct a documentation system for the current project to facilitate subsequent AI Agent Coding.

Your steps:

1. Obtain the current project structure.
2. Read key files, such as various README.md / package.json / go.mod / pyproject.toml ...
3. Consider dividing exploration tasks according to the project's modules, and then Concurrently use scout agents to perform exploration tasks. The scout agents will ultimately produce report documents and the storage paths of the documents.(socut agent will automatically generate the file path and save it, please never specify the path in the Task's prompt!!!)
4. Without reading the reports, Invoke the `recorder` agent using the `Task` tool. When calling the `recorder` agent, pass in the path of the document generated in the previous step, along with the information you know, to let `recorder` initially build the document system. Be careful not to speculate; everything should be based on factual evidence.
