# 版本发布流程

## 1. Purpose

规范TokenRoll Claude Code Plugin的版本更新、测试验证和发布流程，确保插件更新的质量和稳定性，为用户提供可靠的升级体验。

## 2. How it Works / Step-by-Step Guide

### Step 1: 版本规划
1. 确定版本号遵循Semantic Versioning规范
2. 评估变更类型：
   - Major版本：不兼容的API变更
   - Minor版本：向后兼容的新功能
   - Patch版本：向后兼容的错误修复

### Step 2: 代码变更准备
1. 使用`/tr:commit`生成符合规范的提交信息
2. 确保所有变更都有相应的文档更新
3. 运行完整的功能测试验证变更

### Step 3: 版本号更新
1. 更新 `.claude-plugin/plugin.json` 中的版本号
2. 确保版本号格式正确(例如：1.0.25)
3. 检查版本号与实际变更范围匹配

### Step 4: 文档更新
1. 更新README文件中的版本信息
2. 使用`/tr:withDoc`更新相关文档
3. 确保所有文档中的版本引用保持一致

### Step 5: 本地测试
1. 在测试环境验证插件安装过程：
   ```
   /plugin marketplace update https://github.com/TokenRollAI/cc-plugin
   ```
2. 测试所有核心命令功能：
   - `/tr:commit`
   - `/tr:withScout`
   - `/tr:withDoc`
3. 验证agent和command配置正确性

### Step 6: Git提交和标记
1. 提交所有变更到版本控制系统
2. 创建Git tag标记新版本：
   ```
   git tag -a v1.0.25 -m "Release version 1.0.25"
   git push origin v1.0.25
   ```

### Step 7: 发布验证
1. 验证插件市场中的更新是否可用
2. 进行用户环境下的安装测试
3. 确认所有功能正常运行

### Step 8: 发布通知
1. 更新GitHub Release信息
2. 通知团队新版本发布
3. 记录版本变更日志

## 3. Relevant Code Modules

- `.claude-plugin/plugin.json` - 插件版本号配置文件
- `README.md` / `README.zh-CN.md` - 包含版本信息的主文档
- `commands/commit.md` - 用于生成版本更新的提交信息
- `commands/withDoc.md` - 用于更新相关文档
- `commands/withScout.md` - 用于测试插件功能

## 4. Attention

- **版本规范**: 严格遵循Semantic Versioning，确保版本号准确反映变更范围
- **测试完整**: 每次发布前必须进行完整的功能测试，避免引入新问题
- **文档同步**: 版本号更新必须同步到所有相关文档中
- **Git标记**: 创建Git tag是版本发布的标准流程，便于版本回溯
- **向后兼容**: Minor和Patch版本必须保持向后兼容性
- **市场更新**: 插件市场更新可能需要时间，确保用户能够获取到新版本
- **环境清理**: 测试后确保清理测试环境，避免影响正常开发工作
- **变更记录**: 维护详细的变更日志，便于用户了解版本间的差异