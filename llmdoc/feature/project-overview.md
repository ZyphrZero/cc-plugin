# TokenRoll Claude Code Plugin 项目概述与技术架构

## 1. Purpose

TokenRoll Claude Code Plugin是一个为Claude Code设计的插件系统，旨在通过多代理协作架构提升开发效率。该插件提供智能Git自动化、深度代码库分析、并行任务执行和文档管理等核心功能，专为TokenRoll团队内部开发最佳实践而设计。

## 2. How it Works / Step-by-Step Guide

### 技术架构设计

插件采用模块化设计，由四个核心组件构成：

1. **Agent系统** - 三大专业代理协作处理不同类型的任务
2. **Commands系统** - 三个核心命令提供标准化的任务处理框架
3. **配置系统** - 基于JSON的插件元数据和市场配置
4. **文档系统** - 结构化的项目知识管理和维护

### 核心工作流程

1. **调研先行**: 使用scout agent进行深度代码库分析，生成基于证据的报告
2. **任务执行**: 通过worker agent处理具体的文件操作、代码编写和Git命令
3. **文档更新**: 利用recorder agent维护项目知识库的完整性和准确性
4. **多模型支持**: 集成CCR路由系统，支持GLM-4.6等多模型并行处理

### 插件部署机制

- **插件市场**: 通过marketplace.json配置实现插件分发
- **版本管理**: 基于semantic versioning的版本控制系统
- **安装方式**: 支持Claude Code原生插件安装命令

## 3. Relevant Code Modules

- `.claude-plugin/plugin.json` - 插件元数据配置，定义名称、版本和作者信息
- `.claude-plugin/marketplace.json` - 插件市场配置，管理插件分发机制
- `agents/scout.md` - 代码调研代理定义，实现结构化代码分析功能
- `agents/worker.md` - 任务执行代理定义，处理具体的执行任务
- `agents/recorder.md` - 文档管理代理定义，维护项目知识库
- `commands/commit.md` - 智能提交命令，基于Git变化生成提交信息
- `commands/withScout.md` - 调查驱动命令，提供复杂任务的探索框架
- `commands/withDoc.md` - 文档生成命令，管理项目文档创建和更新
- `README.md` / `README.zh-CN.md` - 项目主文档，提供安装和使用指南

## 4. Attention

- **依赖要求**: 需要配置GLM-4.6模型API访问权限以获得最佳性能
- **文档系统**: 依赖`<ProjectRootPath>/llmdoc/index.md`作为文档入口点
- **Git集成**: commit命令要求项目有明确的提交信息格式规范
- **代理协作**: withScout命令建议最多同时启动2-3个scout agent
- **权限管理**: 需要文件系统读写权限、Git仓库访问权限和网络搜索权限
- **版本兼容**: 当前版本为1.0.24，升级时需注意配置文件格式兼容性