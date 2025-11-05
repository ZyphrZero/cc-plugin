# TokenRoll Claude Code Plugin 文档系统

## 核心架构文档

[项目概述与技术架构](feature/project-overview.md): TokenRoll Claude Code Plugin 项目的技术架构概述，包括核心组件、设计原则和开发工作流程

[Agent 系统架构](feature/agent-system.md): 三大核心代理(scout、worker、recorder)的功能定义、协作机制和使用场景

[Commands 命令系统](feature/command-system.md): 三大核心命令(commit、withScout、withDoc)的功能说明、执行流程和使用指南

[插件配置与部署](feature/plugin-configuration.md): 插件的安装配置、版本管理和市场部署机制

## 功能特性文档

[智能 Git 自动化](feature/intelligent-git-automation.md): commit 命令的智能提交信息生成机制和 Git 工作流程集成

[深度代码库调研](feature/deep-codebase-investigation.md): scout agent 的结构化代码分析方法和证据导向的报告生成

[并行任务执行](feature/parallel-task-execution.md): worker agent 的任务执行模型和并发处理能力

[文档知识管理](feature/documentation-knowledge-management.md): recorder agent 的文档系统维护和索引同步机制

[自动化 PR 审查](feature/automated-pr-review.md): reviewPR 命令的并行多维度代码审查机制和 GitHub 集成工作流程

## 技术集成文档

[多模型路由集成](feature/multi-model-routing.md): CCR 系统集成 GLM-4.6 模型的配置方法和路由策略

[文档系统架构](feature/documentation-system.md): llmdoc 目录结构、索引管理和标准化文档格式规范

[Agent 协作机制](feature/agent-collaboration.md): 多代理并行协作的任务分配、结果整合和错误处理机制

## 开发运维文档

[项目初始化指南](sop/project-initialization.md): 新项目环境配置和插件系统初始化的标准操作流程

[代理开发规范](sop/agent-development-guidelines.md): 创建新代理的开发规范、命名约定和工作流程定义

[命令开发规范](sop/command-development-guidelines.md): 新命令开发的标准格式、参数定义和执行流程设计

[版本发布流程](sop/version-release-process.md): 插件版本更新、测试验证和发布的完整流程
