# 模块代码生成器

## 中文版

```markdown
# 模块代码生成

## 角色

你是一位经验丰富的后端工程师。

## 背景

我正在开发一个项目，目前已经完成了 `user`（用户）模块。`user` 模块是按照我们团队的最佳实践和代码规范实现的，它的结构、代码风格、实现方式以及与主应用的集成方式，都是我最满意的标准。

## 任务

现在，我需要你为项目创建一个全新的模块：`$ARGUMENTS`。请你严格参考现有的 `user` 模块，为我创建并集成这个新模块。

## 具体要求

### 1. 严格遵循 user 模块

-   **代码风格**: 完全复制 `user` 模块的代码风格、变量命名、注释格式等。
-   **文件结构**: `$ARGUMENTS` 模块的文件和目录结构必须与 `user` 模块保持一致。
-   **设计模式**: 复用 `user` 模块中使用的设计模式。

> **一句话总结**：将 `user` 模块视为一个模板，`$ARGUMENTS` 模块是这个模板的一个新的、完整的实例。

### 2. 生成模块核心文件

你需要分析 `user` 模块包含了哪些文件（例如：数据库迁移、Model、Service、Router、API Schema 等），然后在 `$ARGUMENTS` 模块中创建出所有功能对等的文件。

**重点在于结构和职责上的完整对齐**。如果 `user` 模块有某个文件，`$ARGUMENTS` 模块也必须有对应的文件并承担相同的职责。

### 3. 处理模块间关联

如果新模块 `$ARGUMENTS` 与任何现有模块（如 `user`）之间存在逻辑关联（例如，一对多、多对多关系），你需要主动识别并实现这些关系。

在实现时，请参考项目中已有的关联实现方式，确保数据模型、数据库外键和业务逻辑中的关联代码与现有代码风格和模式保持一致。

### 4. 模块集成与配置

创建模块文件本身是不够的。你还需要分析 `user` 模块是如何被整个应用集成的（例如：在主路由文件中被引用、在数据库或依赖注入配置中被注册等）。

请在 `$ARGUMENTS` 模块上完整复现这种集成模式，确保新模块在创建后能立即被应用正确识别和使用，无需任何额外的手动配置。

### 5. 质量与验证

-   你写的代码必须是**完整且无误**的。
-   在完成编码后，你必须在内部运行 `npm run build` 命令进行自检，并修复所有可能出现的类型错误、语法错误或依赖问题。
-   最终交付给我的代码，必须能直接通过 `npm run build` 的检查，不需要我做任何修改。

---

**请开始吧。**
```

---

## 英文版

```markdown
# Module Code Generator

## Role

You are an experienced backend engineer.

## Background

I am developing a project and have successfully completed the `user` module. The `user` module has been implemented following our team's best practices and coding standards. Its structure, code style, implementation approach, and integration with the main application represent the standard I'm most satisfied with.

## Task

Now, I need you to create a brand new module for the project: `$ARGUMENTS`. Please strictly reference the existing `user` module to create and integrate this new module for me.

## Specific Requirements

### 1. Strictly Follow the user Module

-   **Code Style**: Completely replicate the code style, variable naming, comment formatting, etc. of the `user` module.
-   **File Structure**: The file and directory structure of the `$ARGUMENTS` module must be consistent with the `user` module.
-   **Design Patterns**: Reuse the design patterns used in the `user` module.

> **Summary in one sentence**: Treat the `user` module as a template, and the `$ARGUMENTS` module is a new, complete instance of this template.

### 2. Generate Module Core Files

You need to analyze what files the `user` module contains (e.g., database migrations, Models, Services, Routers, API Schemas, etc.), then create all functionally equivalent files in the `$ARGUMENTS` module.

**The focus is on complete alignment in structure and responsibilities**. If the `user` module has a certain file, the `$ARGUMENTS` module must also have a corresponding file that assumes the same responsibilities.

### 3. Handle Inter-Module Relationships

If the new module `$ARGUMENTS` has logical relationships with any existing modules (such as `user`) - for example, one-to-many or many-to-many relationships - you need to proactively identify and implement these relationships.

When implementing, please reference the existing relationship implementation patterns in the project, ensuring that the data models, database foreign keys, and business logic relationship code are consistent with existing code styles and patterns.

### 4. Module Integration & Configuration

Creating module files alone is not enough. You also need to analyze how the `user` module is integrated into the entire application (e.g., referenced in main routing files, registered in database or dependency injection configurations, etc.).

Please completely replicate this integration pattern for the `$ARGUMENTS` module, ensuring that the new module can be immediately recognized and used by the application after creation, without any additional manual configuration.

### 5. Quality & Validation

-   The code you write must be **complete and error-free**.
-   After completing the coding, you must internally run the `npm run build` command for self-checking and fix all possible type errors, syntax errors, or dependency issues.
-   The final code delivered to me must be able to pass the `npm run build` check directly without requiring any modifications from me.

---

**Please begin.**
```
