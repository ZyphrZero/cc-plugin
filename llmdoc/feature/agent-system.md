# Agent系统架构

## 1. Purpose

Agent系统是TokenRoll Claude Code Plugin的核心组件，通过三个专业化代理(scout、worker、recorder)的协作机制，实现代码库调研、任务执行和文档管理的自动化处理。该系统采用模块化设计，每个代理都有明确的职责分工和标准化的工作流程。

## 2. How it Works / Step-by-Step Guide

### 代理架构设计

系统包含三个核心代理，形成完整的工作闭环：

1. **scout agent** - 深度代码库调研代理
2. **worker agent** - 任务执行代理
3. **recorder agent** - 文档管理代理

### 协作工作流程

1. **调研阶段**: scout agent进行结构化代码分析，生成基于证据的调查报告
2. **执行阶段**: worker agent基于scout的报告执行具体任务(文件操作、代码编写、Git命令等)
3. **文档阶段**: recorder agent将工作成果转化为结构化文档，更新项目知识库

### 技术实现特性

- **模型配置**: 所有代理都使用haiku模型，支持CCR子代理模型(GLM-4.6)
- **工具权限**: 根据代理职责分配不同的工具权限集
- **并发执行**: 支持多代理并行处理，提高任务执行效率
- **颜色编码**: 绿色(recorder)、红色(scout)、粉色(worker)便于识别

## 3. Relevant Code Modules

- `agents/scout.md` - scout agent定义，实现深度代码分析和客观报告生成
- `agents/worker.md` - worker agent定义，处理明确定义的任务执行
- `agents/recorder.md` - recorder agent定义，维护llmdoc文档系统完整性
- `commands/withScout.md` - scout agent调用命令，提供结构化探索框架
- `commands/withDoc.md` - recorder agent调用命令，管理文档生成流程

## 4. Attention

- **工作流依赖**: scout agent依赖`<ProjectRootPath>/llmdoc/index.md`作为文档入口点
- **输出限制**: scout agent生成的文档有硬性200行长度限制
- **内容规范**: recorder agent严格禁止编造内容，必须基于实际代码生成文档
- **并发控制**: withScout命令建议最多同时启动2-3个scout agent避免管理开销
- **工具权限**: 各代理工具权限不同，recorder不支持WebSearch，worker支持AskUserQuestion
- **模型一致性**: 所有代理都需要配置GLM-4.6模型访问权限以获得最佳性能