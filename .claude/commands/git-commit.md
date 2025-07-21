# 自动化 GIT 提交

## 中文版

```markdown
# 自动化 Git 提交指令

请以自动化、标准化和智能化的方式执行 Git 提交：

1.  **智能分析与交互**:
    - **提交拆分**: 分析代码变更，如果你认为这些变更包含多个独立的逻辑单元（例如，同时修复了一个 bug 并开发了一个新功能），请将它们拆分成多个独立的提交。

2.  **生成并执行提交**:
    - **生成提交信息**: 遵循**约定式提交 (Conventional Commits)**规范，并参考项目已有的风格，生成结构清晰、语义准确的提交信息，你可以根据变更内容的长短来自行决定提交信息的长度，单行或多行（摘要 + 详细描述）。
    - **格式要求**:
        - **描述性**: 信息应清晰、简洁地概括变更的目的。
        - **无页脚**: 确保最终的提交信息中不包含任何 AI 工具自动添加的署名或页脚（例如 "Generated with" 或 "Co-Authored-By" 或 "Claude co-Contributorship" 等）。
    - **自动提交**: 生成提交信息后，**直接使用该信息执行提交**，无需等待我手动确认。

**总而言之**: 你的默认行为是全自动完成 `add` 和 `commit`。只有当你对文件是否应该被版本控制时才需要与我互动。
```

---

## English Version

```markdown
# Automated Git Commit Instructions

Please perform Git commits in an automated, standardized, and intelligent manner:

1. **Smart Analysis & Interaction**
    - **Split Commits**: Analyze the code diffs; if you determine the changes encompass multiple independent logical units (for example, both fixing a bug and developing a new feature), split them into separate commits.

2. **Generate and Execute Commits**
    - **Generate Commit Message**: Follow the **Conventional Commits** specification, and based on the existing style of the project, generate a clear and semantically accurate commit message. You can decide the length of the commit message, whether it's a single line or multiple lines (summary + detailed description), based on the length of the changes.
    - **Formatting Requirements**:
        - **Descriptive**: The message should clearly and concisely summarize the purpose of the change.
        - **No Footers**: Ensure the final commit message contains no AI-generated signatures or footers (e.g., "Generated with", "Co-Authored-By", "Claude co-Contributorship", etc.).

    - **Automatic Commit**: Once the commit message is generated, **directly execute the commit** using that message—no further manual confirmation is required.

**In Summary**: Your default behavior should be to fully automate `git add` and `git commit`. Only interact with me when you're uncertain whether a file should be tracked.
```
