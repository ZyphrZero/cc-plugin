# TokenRoll Claude Code Plugin

<div align="center">

**TokenRoll Claude Code Plugin: Best Practices for CC Coding**

[![GitHub](https://img.shields.io/badge/GitHub-TokenRollAI%2Fcc--plugin-blue?logo=github)](https://github.com/TokenRollAI/cc-plugin)

[English](README.md) | [简体中文](README.zh-CN.md)

</div>

---

## Installation

### Step 1: Install Plugin

```
# Add TokenRoll plugin marketplace
/plugin marketplace add https://github.com/TokenRollAI/cc-plugin

# Install tr plugin
/plugin install tr@cc-plugin
```

### Step 2: Use the Plugin

1. Add to your user-level CLAUDE.md(`~/.claude/CLAUDE.md`)

   ```
   <ALWAYS_STEP_ONE>Read {rootPath}/llmdoc/index.md Then, based on the document links and their descriptions, continue reading other related documents (>=1)</ALWAYS_STEP_ONE>
    <SYSTEM_REMINDER>**Use Scout instead of Explore Agent.**</SYSTEM_REMINDER>

    - **Use Scout instead of Explore Agent.**
    - **The last TODO for any programming task is always to update the project's documentation system using the docer agent.**
    - Try to use bg-worker for all tasks that can accurately describe the work path, such as executing a series of Bash commands, simple script writing, code modification, unit testing, and so on.
    - If you only care about how a task is executed and its results, you should consider using a docker agent.
    - Always use rule: `ALWAYS_STEP_ONE`
   ```

   Done! Now you can use it normally.

2. Force using Scout Agent to enhance context efficiency
   ```
   /withScout xxx(your task)
   ```

### (Recommend!) Install CCR: Power SubAgent with GLM4.6

[Reference](https://github.com/musistudio/claude-code-router)

```
npm install -g @musistudio/claude-code-router
```

Fill in the configuration in `~/.claude-code-router/config.json`, reference as follows:

```
{
    "LOG": true,
    "LOG_LEVEL": "debug",
    "CLAUDE_PATH": "",
    "HOST": "127.0.0.1",
    "PORT": 3456,
    "APIKEY": "sk-apikey",
    "API_TIMEOUT_MS": "600000",
    "PROXY_URL": "http://127.0.0.1:7890",
    "transformers": [
        "Anthropic"
    ],
    "Providers": [
        {
            "name": "claude",
            "api_base_url": "https://<BASE>/v1/messages",
            "api_key": "XXX",
            "models": [
                "claude-sonnet-4-5-20250929"
            ],
            "transformer": {
                "use": [
                    "Anthropic"
                ]
            }
        },
        {
            "name": "glm",
            "api_base_url": "https://open.bigmodel.cn/api/anthropic/v1/messages",
            "api_key": "XXX",
            "models": [
                "glm-4.6"
            ],
            "transformer": {
                "use": [
                    "Anthropic"
                ]
            }
        }
    ],
    "Router": {
        "default": "claude,claude-sonnet-4-5-20250929",
        "background": "claude,claude-sonnet-4-5-20250929",
        "think": "claude,claude-sonnet-4-5-20250929",
        "longContext": "claude,claude-sonnet-4-5-20250929",
        "webSearch": "claude,claude-sonnet-4-5-20250929"
    }
}
```

## About

A powerful Claude Code plugin developed by **DJJ** and **Danniel** for the TokenRoll team. This plugin transforms your development workflow with intelligent Git automation, research-first development patterns, and creative ideation tools.

## Core Features

- **`/tr:commit`** - Intelligent commit message generator that learns from your Git history

- **`/tr:withScout`** - **Save significant main agent context through sub-agent architecture** (ideal for refactoring, bug fixing, feature planning, and documentation in medium to large projects)

- **Super-Idea Agent** - Transform a simple idea into a viral product concept

<div align="center">

Made with ❤️ by DJJ & Danniel

</div>
