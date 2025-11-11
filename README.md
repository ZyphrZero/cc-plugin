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

### Step 2: Configure System Prompt

Copy the entire contents of the `CLAUDE.example.md` file from this repository into your user-level `~/.claude/CLAUDE.md` file. This file contains the necessary system prompts to enable the agents and commands.

Done! Now you can use it normally.

2. Force using Scout Agent to enhance context efficiency
   ```
   /withScout xxx(your task)
   ```

### Update Plugin

```
/plugin marketplace update https://github.com/TokenRollAI/cc-plugin
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

### 🤖 Multi-Agent System

- **`worker`** - Execution agent: Executes a given plan of actions, such as running commands or modifying files.
- **`scout`** - Investigation agent: Performs a deep investigation of the codebase and saves the detailed report to a file.
- **`recorder`** - Documentation agent: Creates and maintains high-quality technical documentation about the codebase.

### 📝 Documentation-Driven Development

- **`/tr:initDoc`** - Initializes a lean, essential set of documentation for the project.
- **`/tr:updateDoc`** - Update documentation system, synchronize technical documentation based on code changes
- **`/tr:what`** - Smart instruction enhancement, provides clear technical guidance and suggestions for programming tasks

### 🔧 Development Workflow

- **`/tr:commit`** - Intelligent commit message generator that learns from your Git history
- **`/tr:withScout`** - Handles a complex task by first investigating the codebase, then executing a plan.
- **`/tr:reviewPR`** - Conducts an automated review of a GitHub Pull Request.

## Recommended Workflow

### 1. Initialize New Project

```bash
# First time use, establish complete documentation system for your project
/tr:initDoc
```

### 2. Daily Development Flow

```bash
# Get clear programming guidance
/tr:what "I need to implement user authentication feature"

# Perform deep code analysis
/tr:withScout "Analyze existing code architecture and find the best integration point"

# Generate intelligent commit message
/tr:commit
```

### 3. Documentation Maintenance

```bash
# Update documentation system after code changes
/tr:updateDoc
```

### 4. Code Quality Assurance

```bash
# Review Pull Request
/tr:reviewPR 123
```

---

<div align="center">

Made with ❤️ by DJJ & Danniel

</div>
