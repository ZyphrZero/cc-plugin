# TokenRoll Claude Code 插件

<div align="center">

**TokenRoll Claude Code Plugin: CC Coding 的最佳实践**

[![GitHub](https://img.shields.io/badge/GitHub-TokenRollAI%2Fcc--plugin-blue?logo=github)](https://github.com/TokenRollAI/cc-plugin)

[English](README.md) | [简体中文](README.zh-CN.md)

</div>

---

## 安装

### Step 1: 安装插件

```
# 添加 TokenRoll 插件市场
/plugin marketplace add https://github.com/TokenRollAI/cc-plugin

# 下载tr插件
/plugin install tr@cc-plugin
```

### Step 2: 使用插件

1. 在用户级别的 CLAUDE.md(通常是: `~/.claude/CLAUDE.md`) 中添加

   ```
    <ALWAYS_STEP_ONE>Read {ProjectRootPath}/llmdoc/index.md Then, based on the document links and their descriptions, continue reading other related documents (>=1)</ALWAYS_STEP_ONE>
    <SYSTEM_REMINDER>**Use Scout instead of Explore Agent.**</SYSTEM_REMINDER>

    - **Use Scout instead of Explore Agent.**
    - **The last TODO for any programming task is always to update the project's documentation system using the docer agent.**
    - Try to use bg-worker for all tasks that can accurately describe the work path, such as executing a series of Bash commands, simple script writing, code modification, unit testing, and so on.
    - If you only care about how a task is executed and its results, you should consider using a docker agent.
    - Always use rule: `ALWAYS_STEP_ONE`
   ```

   好了, 现在你可以正常使用了

2. 强制使用 Scout Agent 加强上下文紧凑程度
   ```
   /withScout xxx(你要做的任务)
   ```

### (强烈推荐) 安装 CCR: 使用 GLM4.6 驱动 SubAgent

[参考](https://github.com/musistudio/claude-code-router)

```
npm install -g @musistudio/claude-code-router
```

在 `~/.claude-code-router/config.json` 中填写配置, 参考如下

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

## 更新插件

```
/plugin marketplace update https://github.com/TokenRollAI/cc-plugin
```

## 关于

由 **DJJ** 和 **Danniel** 为 TokenRoll 团队开发的强大 Claude Code 插件。本插件通过智能 Git 自动化、研究优先开发模式和创意构思工具，彻底改变你的开发工作流。

## 核心功能

- **`/tr:commit`** - 从你的 Git 历史中学习的智能提交信息生成器

- **`/tr:withScout`** - **通过 sub-agent 架构节省大量的主 Agent 上下文** .(中大型项目的重构、bug 修复、功能规划、文档编写)

- **Super-Idea Agent** - 将一个简单的点子转化为病毒式产品概念

<div align="center">

Made with ❤️ by DJJ & Danniel

</div>
