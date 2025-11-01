# 并行任务执行

## 1. Purpose

并行任务执行功能通过worker agent提供高效的多任务并行处理能力。该功能专注于执行明确定义的任务，包括文件操作、代码编写、Git命令、数据处理和web研究等，支持多个worker agent同时处理不同职责，显著提升复杂任务的执行效率。

## 2. How it Works / Step-by-Step Guide

### 任务执行模型

1. **任务理解**: 读取目标、上下文和执行步骤
2. **并行执行**: 根据任务分配同时处理不同职责
3. **结果报告**: 提供清晰详细的执行结果报告

### 输入要求规范

每个任务必须包含以下要素：
1. **Objective**: 明确需要完成的目标
2. **Context**: 所有必要信息(文件路径、URL、数据、配置等)
3. **Execution Steps**: 要执行的具体操作列表

可选要素：
4. **Success Criteria**: 验证任务完成的标准
5. **Output Requirements**: 期望的输出格式和内容

### 并发执行机制

#### 职责分离
- 每个worker agent处理一个特定职责，避免工作重叠
- 在完整上下文支持下独立工作
- 生成完整的执行报告供调用代理整合

#### 任务分配策略
- **功能性分离**: 按照不同功能模块分配任务
- **独立性保证**: 确保各worker任务间无相互依赖
- **结果整合**: 由调用代理负责整合各worker的执行报告

### 标准化输出格式

每个worker agent必须按照以下格式报告结果：

```markdown
**Status:** [COMPLETED | FAILED]
**Summary:** [一句话结果描述]
**Artifacts:** [创建/修改的文件，执行的命令]
**Key Results:** [重要发现或观察结果]
**Notes:** [调用代理的相关上下文]
```

## 3. Relevant Code Modules

- `agents/worker.md` - worker agent完整定义，包含执行模型和输出格式
- `commands/commit.md` - commit命令，使用worker agent执行Git信息收集
- `commands/withDoc.md` - withDoc命令，使用worker agent处理文档生成任务
- `commands/withScout.md` - withScout命令，在执行阶段使用worker agent

## 4. Attention

- **输入完整性**: 任务描述必须包含Objective、Context和Execution Steps三个核心要素
- **并发管理**: 需要合理控制并行worker数量，避免资源竞争
- **独立性保证**: 并行任务间必须保持独立，避免相互依赖或冲突
- **结果整合**: 调用代理负责整合多个worker的执行报告，需要清晰的整合逻辑
- **错误处理**: 任何worker执行失败都需要在Status中明确标记
- **工具权限**: worker agent支持AskUserQuestion，可以进行交互式任务执行
- **模型依赖**: 所有worker都需要配置GLM-4.6模型访问权限以获得最佳性能
- **超时控制**: 长时间运行的任务需要设置合理的执行超时机制