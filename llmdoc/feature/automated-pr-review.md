# 自动化PR审查

## 1. Purpose

PR自动化审查功能通过并行部署scout代理对GitHub Pull Request进行多维度深度分析，包括代码质量、架构一致性和测试覆盖等方面。该功能将分散的审查工作流程整合为一个结构化、可重复的自动化流程，提高代码审查的效率和一致性。

## 2. How it Works / Step-by-Step Guide

### 工作流程概览

自动化审查流程分为五个核心阶段：

**第一阶段：PR信息获取**
1. 支持手动指定PR编号或自动检测当前分支关联的PR
2. 使用worker agent并行执行`gh pr view`和`gh pr diff`获取PR详情和代码变更

**第二阶段：并行多维度分析**
1. **代码质量分析(Scout A)**: 检查代码风格、函数复杂度、代码重复、命名清晰度和错误处理
2. **架构一致性审查(Scout B)**: 验证模块组织、依赖引入、设计模式遵循和SOLID原则合规
3. **测试覆盖检查(Scout C)**: 评估测试完整性、边界情况覆盖和文档更新

**第三阶段：结果合成**
1. 整合三个scout的分析报告，识别关键发现
2. 按严重程度分类：
   - 🔴 严重问题(必须修复)：安全隐患、破坏性变更、重大缺陷
   - 🟡 重要问题(应该修复)：代码质量、架构违反
   - 🟢 建议(可选改进)：轻微优化、风格建议

**第四阶段：生成结构化审查评论**
生成包含以下结构的markdown评论：
- 概览：PR目的和范围总结
- 代码质量：优势和问题列表
- 架构一致性：对齐情况和关注点
- 测试和文档：覆盖状态和遗漏
- 详细建议：按严重程度分组的改进建议

**第五阶段：提交审查**
1. 预览生成的审查评论
2. 使用AskUserQuestion获取用户确认
3. 根据问题严重程度确定评论状态(APPROVE/REQUEST_CHANGES/COMMENT)
4. 通过`gh pr review`命令提交到GitHub

### 关键设计要点

- **证据导向**：所有发现必须基于实际代码分析，禁止假设推测
- **并行高效**：并行部署2-3个scout agent进行多维度分析
- **建构性反馈**：提供可执行、具体的改进建议，包括代码示例
- **上下文感知**：考虑PR的具体场景(bug修复/新功能/重构)
- **规范对齐**：建议基于项目现有约定和代码模式
- **安全优先**：特别关注潜在的安全漏洞和性能影响

## 3. Relevant Code Modules

- `commands/reviewPR.md` - reviewPR命令的完整定义和执行流程
- `agents/scout.md` - scout agent实现，提供深度代码分析能力
- `agents/worker.md` - worker agent实现，处理GitHub CLI命令执行
- `llmdoc/feature/command-system.md` - Commands系统整体架构
- `llmdoc/feature/deep-codebase-investigation.md` - scout agent的调研方法论

## 4. Attention

- **GitHub CLI依赖**: 需要安装并配置gh CLI工具，且用户已通过`gh auth login`认证
- **API速率限制**: 频繁的大型PR分析可能触发GitHub API限流，需要提醒用户稍后重试
- **分析耗时**: 3个并行scout的深度分析通常需要2-5分钟，依赖代码量和复杂度
- **评论冲突**: 多次提交评论可能导致重复意见，应提醒用户更新已提交的评论
