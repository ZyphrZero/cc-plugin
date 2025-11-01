# 文档系统架构

## 1. Purpose

文档系统架构定义了TokenRoll Claude Code Plugin项目知识管理的标准化结构，通过层次化的目录组织、索引管理和统一的文档格式规范，确保项目文档的完整性、一致性和可维护性，为开发团队提供可靠的技术参考。

## 2. How it Works / Step-by-Step Guide

### 目录结构设计

文档系统采用四层目录结构：
```
llmdoc/
├── index.md          # 主索引文件(单一入口点)
├── sop/              # 标准操作流程目录
├── feature/          # 功能特性文档目录
└── agent/            # 代理输出文档目录
```

### 索引管理系统

#### 主索引文件(index.md)
- 作为文档系统的单一入口点
- 包含所有文档的链接和详细描述
- 格式：`[Document Title](path/to/document.md): <详细描述>`

#### 索引原子性原则
- 任何文档的创建、修改或删除必须同步更新index.md
- 在同一操作中完成内容修改和索引更新
- 无例外地维护索引与内容的一致性

### 文档分类标准

#### SOP目录(标准操作流程)
- **用途**: 存储关键、多步骤、易错的手动操作流程
- **内容**: 基础设施设置、发布检查表、紧急回滚流程等
- **命名**: 使用描述性的kebab-case文件名
- **示例**: `how-to-onboard-a-new-service.md`, `emergency-database-rollback-procedure.md`

#### Feature目录(功能特性)
- **用途**: 存储特定产品功能的技术设计和实现文档
- **内容**: 技术架构、设计目的、代码模块关联
- **组织**: 复杂功能可创建子目录结构
- **示例**: `real-time-analytics-dashboard/architecture.md`

#### Agent目录(代理输出)
- **用途**: 存储各类代理生成的调查和分析文档
- **内容**: scout agent的代码分析报告
- **结构**: 按代理名称组织子目录
- **示例**: `agent/scout/authentication-flow-analysis.md`

### 标准化文档格式

所有文档遵循统一四段式结构：
```markdown
# [Document Title]

## 1. Purpose
简明解释功能/流程及其解决的问题

## 2. How it Works / Step-by-Step Guide
技术架构描述或步骤指南

## 3. Relevant Code Modules
相关代码文件或目录的相对路径列表

## 4. Attention(if have)
注意事项列表(不超过10行)
```

## 3. Relevant Code Modules

- `llmdoc/index.md` - 主索引文件，文档系统的入口点
- `agents/recorder.md` - 文档管理代理，负责维护文档系统
- `commands/withDoc.md` - 文档生成命令，管理文档创建流程
- `llmdoc/sop/` - 标准操作流程文档目录
- `llmdoc/feature/` - 功能特性文档目录
- `llmdoc/agent/` - 代理输出文档目录

## 4. Attention

- **索引同步**: 任何文档操作都必须立即更新index.md，这是强制要求
- **路径规范**: 文档中必须使用相对路径，绝对路径仅用于内部处理
- **内容控制**: 每个文档控制在250行以内，超长文档需拆分或精简
- **真实性强**: 严格禁止编造内容，必须基于实际代码生成文档
- **开发者导向**: 专注于代码设计、架构、维护等开发者需求
- **命名规范**: 文件名使用kebab-case，必须清晰描述内容
- **目录分类**: 严格按照sop/feature/agent的用途分类存储
- **版本一致性**: 确保index.md中的链接始终与实际文件位置同步
- **无教程内容**: 排除教程、指南、快速入门等非开发团队内容
- **更新顺序**: 先完成内容修改，再更新index.md，顺序不可颠倒