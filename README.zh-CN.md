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

### Step 2: 配置系统提示词

将本仓库中的 `CLAUDE.example.md` 文件的全部内容，复制到您用户级的 `~/.claude/CLAUDE.md` 文件中。此文件包含了启用 Agent 和 Command 所必需的系统提示。

好了, 现在你可以正常使用了

2. 强制使用 Scout Agent 加强上下文紧凑程度
   ```
   /withScout xxx(你要做的任务)
   ```

### 更新插件

```
/plugin marketplace update https://github.com/TokenRollAI/cc-plugin
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

## 关于

由 **DJJ** 和 **Danniel** 为 TokenRoll 团队开发的强大 Claude Code 插件。本插件通过智能 Git 自动化、研究优先开发模式和创意构思工具，彻底改变你的开发工作流。

## 核心功能

### 🤖 多代理系统

- **`worker`** - 执行代理: 执行一个给定的行动计划，例如运行命令或修改文件。
- **`scout`** - 调查代理: 对代码库进行深入调查，并将详细报告保存到文件中。
- **`recorder`** - 文档代理: 创建并维护关于代码库的高质量技术文档。

### 📝 文档驱动开发

- **`/tr:initDoc`** - 为项目初始化一个精简、核心的文档集。
- **`/tr:updateDoc`** - 更新文档系统，基于代码变更同步更新技术文档
- **`/tr:what`** - 智能指令强化，为编程任务提供清晰的技术指导和建议

### 🔧 开发工作流

- **`/tr:commit`** - 智能提交信息生成器，学习您的 Git 历史并生成高质量提交信息
- **`/tr:withScout`** - 通过先调查代码库再执行计划的方式来处理复杂任务。
- **`/tr:reviewPR`** - 对 GitHub Pull Request 进行自动化审查。

## 推荐使用流程

### 1. 初始化新项目

```bash
# 首次使用，为项目建立完整的文档系统
/tr:initDoc
```

### 2. 日常开发流程

```bash
# 获得清晰的编程指导
/tr:what "我需要实现用户认证功能"

# 进行深度代码分析
/tr:withScout "分析现有代码架构，找出最佳集成点"

# 生成智能提交信息
/tr:commit
```

### 3. 文档维护

```bash
# 代码变更后更新文档系统
/tr:updateDoc
```

### 4. 代码质量保证

```bash
# 审查Pull Request
/tr:reviewPR 123
```

---

<div align="center">

Made with ❤️ by DJJ & Danniel

</div>
