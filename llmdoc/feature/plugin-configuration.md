# 插件配置与部署

## 1. Purpose

TokenRoll Claude Code Plugin采用基于JSON的配置系统和Claude Code原生插件市场机制，提供标准化的插件安装、版本管理和部署流程。该系统确保插件能够无缝集成到Claude Code环境中，并支持团队内部的插件分发和更新。

## 2. How it Works / Step-by-Step Guide

### 插件配置结构

插件配置包含两个核心文件：

1. **plugin.json** - 插件元数据配置，定义插件基本信息
2. **marketplace.json** - 插件市场配置，管理插件分发机制

### 安装部署流程

1. **添加插件市场**: 使用`/plugin marketplace add`命令添加TokenRoll插件市场
2. **安装插件**: 通过`/plugin install tr@cc-plugin`安装tr插件
3. **用户配置**: 在用户级别CLAUDE.md中添加插件使用规则
4. **可选集成**: 安装CCR以获得GLM-4.6驱动的子代理支持

### 版本管理机制

- **语义化版本**: 遵循Semantic Versioning规范(当前版本: 1.0.24)
- **市场更新**: 通过`/plugin marketplace update`命令更新插件版本
- **向后兼容**: 配置文件格式保持向后兼容性

### 配置文件规范

- **plugin.json**: 包含name、description、version、author等元数据
- **marketplace.json**: 包含marketplace信息、owner信息和plugins列表
- **JSON格式**: 严格遵循JSON语法规范，确保解析正确性

## 3. Relevant Code Modules

- `.claude-plugin/plugin.json` - 插件元数据配置文件，定义插件基本信息和版本
- `.claude-plugin/marketplace.json` - 插件市场配置文件，管理插件分发和版本
- `README.md` / `README.zh-CN.md` - 项目主文档，包含安装配置详细说明
- `agents/scout.md` - 包含CCR模型配置示例和集成说明
- `commands/withScout.md` - 包含CCR路由配置的完整示例

## 4. Attention

- **配置格式**: JSON文件必须严格符合语法规范，任何格式错误都会导致插件安装失败
- **版本同步**: plugin.json和marketplace.json中的版本信息需要保持同步
- **市场地址**: 插件市场地址必须是有效的GitHub仓库URL
- **用户配置**: CLAUDE.md配置需要准确反映插件功能和工作流程
- **CCR依赖**: GLM-4.6模型集成需要额外安装和配置CCR工具
- **权限要求**: 插件安装需要Claude Code的插件管理权限
- **更新机制**: 插件更新需要手动执行marketplace update命令