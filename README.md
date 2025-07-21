# Claude Code Commands

个人使用的专为 Claude Code 整理的自定义命令集合。这些命令旨在提高开发效率，涵盖了常见的开发场景和工作流程。

## 📋 命令列表

### 🐛 fix-bug - BUG 修复专家

专业的 BUG 分析和修复助手，帮助快速定位问题根源并提供解决方案。

**功能特性：**

- 逐步推理，找出 BUG 根本原因
- 准确修复代码问题
- 详细解释错误原因和修复方案
- 提供性能和可读性优化建议

**使用方法：**

```
/fix-bug [BUG描述或错误信息]
```

### 🚀 git-commit - 自动化 Git 提交

智能化的 Git 提交工具，自动分析代码变更并生成规范的提交信息。

**功能特性：**

- 遵循约定式提交 (Conventional Commits) 规范
- 智能分析变更，支持拆分多个独立提交
- 自动执行 `git add` 和 `git commit`
- 生成清晰、语义准确的提交信息
- 无需手动确认，全自动化流程

**使用方法：**

```
/git-commit
```

### 🏗️ module-gen - 模块代码生成器 ***内部项目使用***

基于现有模块模板，快速生成新的功能模块。

**功能特性：**

- 严格遵循现有 `user` 模块的代码风格和结构
- 生成完整的模块文件（Model、Service、Router、API Schema 等）
- 自动处理模块间关联关系
- 完整的模块集成和配置
- 确保代码质量，通过 `npm run build` 检查

**使用方法：**

```
/module-gen [模块名称]
```

### 📝 claude-md - CLAUDE.md 文档补充

快速为项目的 CLAUDE.md 文件添加信息和文档。

**功能特性：**

- 支持中英文双语
- 规范化的文档格式
- 便于项目文档维护

**使用方法：**

```
/claude-md [要添加的内容]
```

## 🛠️ 安装使用

1. 将此项目克隆到本地：

```bash
git clone [repository-url]
```

2. 将 `.claude` 目录复制到你的项目根目录

3. 在 Claude Code 中使用 `/` 前缀调用命令

## 📁 项目结构

```
my-claude-code-commands/
├── .claude/
│   ├── commands/
│   │   ├── claude-md.md      # CLAUDE.md 文档补充命令
│   │   ├── fix-bug.md        # BUG 修复命令
│   │   ├── git-commit.md     # Git 提交命令
│   │   └── module-gen.md     # 模块生成命令
│   └── settings.json         # Claude 配置文件
└── README.md                 # 项目说明文档
```

## 🎯 使用场景

- **开发调试**：使用 `fix-bug` 快速定位和修复代码问题
- **版本控制**：使用 `git-commit` 实现规范化的代码提交
- **模块开发**：使用 `module-gen` 快速搭建新功能模块
- **文档维护**：使用 `claude-md` 更新项目 CLAUDE.md 文档

## 📄 许可证

本项目仅供个人学习和使用。
