# Agent协作机制

## 1. Purpose

Agent协作机制定义了scout、worker、recorder三大代理之间的协同工作模式，通过标准化的信息传递、任务分配和结果整合流程，实现复杂开发任务的自动化处理，确保从代码调研到任务执行再到文档更新的完整工作闭环。

## 2. How it Works / Step-by-Step Guide

### 协作架构设计

三大代理形成标准的开发工作流程：
1. **调研阶段**: scout agent进行深度代码分析
2. **执行阶段**: worker agent处理具体任务
3. **文档阶段**: recorder agent更新项目知识库

### 标准协作流程

#### 流程一：复杂功能开发
1. **启动**: withScout命令触发协作流程
2. **调研**: 部署多个scout agent并行分析不同代码领域
3. **整合**: 主代理分析scout报告，制定执行计划
4. **执行**: 使用worker agent实现功能开发
5. **文档**: 调用recorder agent生成项目文档

#### 流程二：Git提交自动化
1. **触发**: commit命令启动流程
2. **信息收集**: worker agent并行执行Git命令获取状态
3. **分析生成**: 基于历史数据生成提交信息
4. **用户确认**: 通过AskUserQuestion确认或修改
5. **执行提交**: 用户确认后执行Git提交操作

#### 流程三：文档更新流程
1. **变更检测**: recorder agent检测代码变更
2. **分析影响**: 评估变更对文档系统的影响
3. **文档更新**: 创建或更新相关文档
4. **索引同步**: 立即更新index.md保持一致性

### 信息传递机制

#### 上下文文档传递
- scout agent生成结构化调研文档
- worker agent基于调研文档执行任务
- recorder agent基于执行结果更新文档

#### 参数化调用
- 命令提供明确的任务描述和执行参数
- Agent接收完整的上下文信息
- 结果按照标准化格式输出

### 并发协调策略

#### 多Scout并行
- **任务分配**: 按代码领域或功能模块分配独立调研任务
- **数量控制**: 建议2-3个scout agent避免管理开销
- **结果整合**: 主代理负责整合各scout的报告和发现

#### 多Worker协作
- **职责分离**: 每个worker处理特定类型的执行任务
- **独立性保证**: 确保各worker任务间无相互依赖
- **报告整合**: 调用代理整合各worker的执行结果

### 错误处理和恢复

#### 失败检测
- 每个agent提供明确的状态报告(COMPLETED/FAILED)
- 详细的错误信息和失败原因
- 失败场景的重试或回退机制

#### 工作流恢复
- 部分失败时的继续执行策略
- 关键路径失败的完整回滚机制
- 错误信息的文档化和知识沉淀

## 3. Relevant Code Modules

- `agents/scout.md` - scout agent定义，负责深度代码分析
- `agents/worker.md` - worker agent定义，负责任务执行
- `agents/recorder.md` - recorder agent定义，负责文档管理
- `commands/withScout.md` - 定义scout协作的工作流程
- `commands/commit.md` - 定义worker协作的Git流程
- `commands/withDoc.md` - 定义recorder协作的文档流程

## 4. Attention

- **依赖顺序**: scout → worker → recorder的标准顺序不可颠倒
- **上下文完整性**: 后续agent依赖前面agent的输出，确保信息完整性
- **并发控制**: scout和worker的并发数量需要合理控制，避免资源竞争
- **状态同步**: 各agent的状态信息需要及时传递和同步
- **错误传播**: 一个agent的失败可能影响整个协作流程
- **结果格式**: 所有agent的输出必须遵循标准化格式，便于整合
- **工具权限**: 不同agent的工具权限不同，影响协作能力
- **模型依赖**: 所有agent都需要GLM-4.6模型支持，确保性能一致性
- **文档同步**: recorder agent的索引更新是协作流程的最后一步，必须严格执行