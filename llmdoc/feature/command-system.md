# Commands命令系统

## 1. Purpose

Commands系统是TokenRoll Claude Code Plugin的用户交互接口，提供三个核心命令来处理不同类型的开发任务。每个命令都定义了标准化工作流程，通过调用相应的Agent实现复杂任务的自动化处理，确保开发流程的一致性和可重复性。

## 2. How it Works / Step-by-Step Guide

### 命令架构设计

系统包含四个核心命令，覆盖开发的主要工作场景：

1. **commit命令** - 智能Git提交信息生成
2. **withScout命令** - 复杂任务的探索式处理
3. **withDoc命令** - 项目文档的生成和管理
4. **reviewPR命令** - 自动化GitHub Pull Request代码审查

### 命令执行流程

#### commit命令执行流程
1. 使用worker agent并行获取Git状态(diff、staged、log等)
2. 分析当前分支、文件类型和变化性质
3. 基于历史提交格式生成符合项目风格的提交信息
4. 通过AskUserQuestion让用户确认或修改提交信息

#### withScout命令执行流程
1. 解构复杂任务为独立的调研领域
2. 部署2-3个scout agent并行收集信息
3. 整合各scout的报告，识别关键联系
4. 基于完整性评估决定迭代或执行
5. 执行具体任务并提供详细报告

#### withDoc命令执行流程
1. 请求分诊：特定请求 → 项目初始化 → 增量更新
2. 根据分诊结果委托给相应子代理处理
3. 协调文档生成过程，确保质量和一致性

#### reviewPR命令执行流程
1. 解析PR编号：手动指定或通过`gh pr status`自动检测
2. 并行获取PR信息：执行`gh pr view`和`gh pr diff`获取详情和代码变更
3. 并行部署scout agent：分配代码质量、架构一致性、测试覆盖三个分析维度
4. 合成分析结果：整合scout报告，按严重程度分类问题
5. 生成结构化评论：包含概览、多维度分析和改进建议
6. 用户确认与提交：预览评论，获取用户确认后通过`gh pr review`提交

### 命令与Agent映射关系

- commit命令 → worker agent (Git信息收集和分析)
- withScout命令 → scout agent (深度代码库调研)
- withDoc命令 → recorder agent (文档系统管理)
- reviewPR命令 → worker agent (PR信息获取) + scout agent (代码分析)

## 3. Relevant Code Modules

- `commands/commit.md` - commit命令定义，实现智能Git提交信息生成
- `commands/withScout.md` - withScout命令定义，提供结构化探索框架
- `commands/withDoc.md` - withDoc命令定义，作为技术项目经理协调文档生成
- `commands/reviewPR.md` - reviewPR命令定义，实现自动化GitHub PR审查
- `agents/worker.md` - worker agent定义，被commit和reviewPR命令调用
- `agents/scout.md` - scout agent定义，被withScout和reviewPR命令调用
- `agents/recorder.md` - recorder agent定义，被withDoc命令调用

## 4. Attention

- **执行顺序**: withDoc命令的三种路径有严格优先级(特定请求 > 项目初始化 > 默认增量更新)
- **Git依赖**: commit命令需要Git仓库状态检查的准确性
- **GitHub CLI依赖**: reviewPR命令需要gh CLI工具且用户已完成认证
- **迭代复杂度**: withScout命令可能需要多个迭代周期才能完成复杂任务
- **Agent可用性**: 所有命令都假设相应的agent已经正确定义并可调用
- **用户交互**: commit命令、reviewPR命令和部分worker任务需要通过AskUserQuestion进行用户确认
- **并发管理**: withScout和reviewPR命令需要合理控制并行scout数量，避免管理开销过大