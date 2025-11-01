# 多模型路由集成

## 1. Purpose

多模型路由集成功能通过CCR(Claude Code Router)系统提供GLM-4.6等多模型的并行处理能力，为TokenRoll Claude Code Plugin的子代理提供高性能的计算支持，显著提升复杂任务的执行效率和响应速度。

## 2. How it Works / Step-by-Step Guide

### CCR架构设计

CCR作为子代理路由系统，提供以下核心功能：
- **多模型支持**: 集成GLM-4.6和Claude模型
- **智能路由**: 根据任务类型自动选择最适合的模型
- **并行处理**: 支持多代理并发执行
- **配置管理**: 集中化的模型和路由配置

### 模型配置流程

1. **CCR安装**: 通过npm安装全局CCR工具
2. **配置文件设置**: 创建并编辑`~/.claude-code-router/config.json`
3. **模型提供者配置**: 添加GLM-4.6和Claude模型的API配置
4. **路由规则定义**: 设置不同任务类型的模型路由策略
5. **代理集成**: 在agent文件中指定CCR子代理模型

### 配置文件结构

CCR配置文件包含以下关键部分：
- **Providers**: 模型提供者配置(API地址、密钥、模型列表)
- **Router**: 路由规则配置(default、background、think、longContext等)
- **Transformers**: 数据格式转换器配置
- **网络配置**: 代理URL、超时设置、日志级别

### 集成实现机制

每个agent通过`<CCR-SUBAGENT-MODEL>`标签指定使用CCR模型：
```yaml
<CCR-SUBAGENT-MODEL>glm,glm-4.6</CCR-SUBAGENT-MODEL>
```

### 路由策略

- **default**: 默认使用Claude模型
- **background**: 后台任务使用Claude模型
- **think**: 复杂分析使用Claude模型
- **longContext**: 长上下文任务使用Claude模型
- **webSearch**: 网络搜索使用Claude模型

## 3. Relevant Code Modules

- `agents/scout.md` - 包含CCR模型配置示例和GLM-4.6集成说明
- `agents/worker.md` - 包含CCR子代理模型配置
- `agents/recorder.md` - 包含CCR子代理模型配置
- `commands/withScout.md` - 包含完整的CCR配置示例
- `README.md` / `README.zh-CN.md` - 包含CCR安装和配置指南

## 4. Attention

- **API密钥**: GLM-4.6模型需要有效的API密钥，确保网络访问权限
- **配置格式**: CCR配置文件必须严格遵循JSON格式，任何语法错误都会导致启动失败
- **网络依赖**: CCR路由依赖网络连接，需要配置适当的代理设置(如需要)
- **版本兼容**: 确保CCR工具版本与插件系统兼容
- **性能优化**: 合理配置路由规则，根据任务特点选择最适合的模型
- **错误处理**: 配置错误时需要检查日志输出，常见问题包括API地址错误、密钥无效等
- **并发限制**: 注意API调用频率限制，避免超出配额
- **模型可用性**: 定期检查配置的模型是否可用，及时更新模型列表