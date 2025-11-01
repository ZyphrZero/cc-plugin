# 项目初始化指南

## 1. Purpose

规范新项目环境中TokenRoll Claude Code Plugin的配置和初始化流程，确保插件系统能够正确集成到开发工作流中，并为团队提供统一的最佳实践工具集。

## 2. How it Works / Step-by-Step Guide

### Step 1: 插件市场配置
1. 添加TokenRoll插件市场到Claude Code环境
   ```
   /plugin marketplace add https://github.com/TokenRollAI/cc-plugin
   ```

### Step 2: 插件安装
1. 安装tr插件到当前环境
   ```
   /plugin install tr@cc-plugin
   ```

### Step 3: 用户配置设置
1. 编辑用户级别CLAUDE.md文件(通常位于 `~/.claude/CLAUDE.md`)
2. 添加以下配置块：
   ```
   <language>Always answer in 简体中文</language>

   <system-reminder>
   <always-step-one>Use Read tool read {ProjectRootPath}/llmdoc/index.md...</always-step-one>
   <tool-usage-exention>**Use tr:scout agent instead of Explore Agent.**</tool-usage-exention>
   <optional-coding>Option-based programming never jumps to conclusions...</optional-coding>
   ```
3. 添加核心工作流规则：
   - 使用tr:scout替代Explore Agent
   - 编程任务最后使用recorder agent更新文档
   - 优先使用worker agent处理具体执行任务
   - 遵循always-step-one和optional-coding原则

### Step 4: CCR集成(可选但推荐)
1. 安装CCR工具：
   ```
   npm install -g @musistudio/claude-code-router
   ```

2. 配置CCR路由文件 `~/.claude-code-router/config.json`：
   - 添加GLM-4.6模型配置
   - 设置代理URL(如需要)
   - 配置路由规则
   - 设置超时和日志级别

### Step 5: 文档系统初始化
1. 在项目根目录创建llmdoc目录结构：
   ```
   llmdoc/
   ├── index.md
   ├── sop/
   ├── feature/
   └── agent/
   ```

2. 初始化index.md文件，添加基础文档结构

### Step 6: 验证测试
1. 测试commit命令：`/tr:commit`
2. 测试withScout命令：`/tr:withScout [简单任务]`
3. 测试withDoc命令：`/tr:withDoc init`

## 3. Relevant Code Modules

- `README.md` / `README.zh-CN.md` - 包含详细的安装和配置说明
- `commands/withScout.md` - 包含CCR配置的完整示例
- `agents/scout.md` - 包含GLM-4.6模型配置示例
- `commands/withDoc.md` - 项目初始化的文档生成流程
- `.claude-plugin/plugin.json` - 插件版本和依赖信息

## 4. Attention

- **配置顺序**: 必须按照市场添加 → 插件安装 → 用户配置的顺序执行
- **文件路径**: CLAUDE.md文件路径因操作系统而异，确保找到正确的用户级别配置文件
- **CCR依赖**: GLM-4.6集成需要额外的网络配置和API密钥
- **权限要求**: 插件安装需要Claude Code的管理权限
- **文档路径**: 项目文档系统必须在项目根目录下的llmdoc目录中初始化
- **测试验证**: 初始化完成后必须进行功能测试，确保所有命令正常工作
- **团队一致性**: 团队成员应使用相同的配置模板，确保工作流一致性