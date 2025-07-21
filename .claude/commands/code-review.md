# 代码审查

## 中文版

```markdown
# 代码审查并修改

## 角色

你是一位极其严谨和注重细节的代码审查工程师 (Code Reviewer)。你的任务是找出代码实现中的任何不一致之处并修改它。

## 背景

我之前让你根据 `user` 模块作为模板，创建了一个新的 `$ARGUMENTS` 模块。现在，我需要你对你生成的代码进行一次严格的审查，以确保新模块在每一个细节上都完全遵循了模板的规范。

## 核心任务

请你逐一对比 `$ARGUMENTS` 模块和 `user` 模块中每一个功能对等的文件，然后生成一份详细的审查报告。

## 审查流程与报告格式

你的审查报告需要严格按照下面的结构来组织：

### 代码审查报告：`$ARGUMENTS` vs `user`

#### 1. Service 层文件对比

**对比文件:**

-   `src/services/user/*.ts` (模板)
-   `src/services/$ARGUMENTS/*.ts` (待审查)

**检查要点:**

-   **文件结构**: 确保包含所有必需文件 (`create.ts`, `delete-by-id.ts`, `find-list.ts`, `find-list-and-count.ts`, `find-one.ts`, `find-one-by-id.ts`, `update.ts`, `index.ts`)
-   **导入语句**: 检查导入路径格式、模块引用是否一致
-   **函数定义**: 使用 `export const functionName = async () => {}` 格式
-   **类型定义**: `CreateData` 类型使用 `Pick<Model, 'field1' | 'field2'>` 格式
-   **ID 生成**: 使用正确的前缀格式 (User: 'U' + 10 位数字)
-   **数据库操作**: 使用 `table('tableName')` 语法，错误处理方式
-   **上下文获取**: 使用 `getContext()` 或 `getUserId()` 获取用户信息
-   **返回值**: create 方法调用 `findOneById(id)` 返回完整对象
-   **index.ts 导出**: 按字母顺序排列方法，服务名称格式为 `${ModuleName}Service`

#### 2. Router 层文件对比

**对比文件:**

-   `src/routers/user/*.ts` (模板)
-   `src/routers/$ARGUMENTS/*.ts` (待审查)

**检查要点:**

-   **文件结构**: 包含 (`create.ts`, `delete.ts`, `read-detail.ts`, `read-list.ts`, `update.ts`, `index.ts`)
-   **路由组织**:
    -   ID 路由中间件模式: 检查 ID 格式验证 (长度 11 位，正确前缀)
    -   嵌套路由结构: `idr` 处理带 ID 的路由，`r` 处理所有路由
    -   路由挂载顺序: `detail`, `update`, `del` 在 `idr`; `list`, `create` 在 `r`
-   **中间件**: ID 验证逻辑、target 设置、错误处理
-   **导入导出**: 统一的导入别名 (`{ r as create }`)、变量类型定义
-   **错误处理**: 使用 `ApiError` 和正确的错误码
-   **响应格式**: 正确的泛型类型和状态码

#### 3. Schema 层文件对比

**对比文件:**

-   `src/schemas/user/*.ts` (模板)
-   `src/schemas/$ARGUMENTS/*.ts` (待审查)

**检查要点:**

-   **文件结构**: 包含 (`create.ts`, `update.ts`, `query.ts`, `index.ts`)
-   **导入声明**: `import { z } from 'zod/v4'` 格式
-   **Schema 定义**:
    -   create.ts: 必填字段验证规则
    -   update.ts: 可选字段 (所有字段添加 `.optional()`)
    -   query.ts: 查询参数定义
-   **验证规则一致性**: 相同字段使用相同的验证规则
-   **导出格式**: `export const CreateSchema = z.object({...})`
-   **index.ts 聚合**: `${ModuleName}Schema` 对象，包含 `Create`, `Update`, `Query`

#### 4. Model 文件对比

**对比文件:**

-   `src/models/user.ts` (模板)
-   `src/models/$ARGUMENTS.ts` (待审查)

**检查要点:**

-   **接口定义**: `export interface ${ModuleName}Model {}`
-   **字段规范**:
    -   id: string (正确格式)
    -   业务字段定义
    -   系统字段: `creator_id`, `updater_id`, `created_at`, `updated_at`
-   **可选字段标记**: 敏感字段如 `password?` 的可选标记
-   **字段类型**: Date 类型使用，null 联合类型
-   **models/index.ts 导出**: 检查是否正确导出新模型

#### 5. 具体路由实现对比

**create.ts 路由对比:**

-   **类型定义**: `type CreateData = z.infer<typeof ${ModuleName}Schema.Create>`
-   **验证中间件**: `customZodValidator(${ModuleName}Schema.Create, 'json')`
-   **业务逻辑**: 重复检查逻辑、密码哈希处理
-   **错误处理**: 统一的错误码使用
-   **响应格式**: `ApiCreateResponse<${ModuleName}Model>` 格式

**read-list.ts 路由对比:**

-   **分页处理**: 使用分页查询 Schema
-   **服务调用**: `findListAndCount` 方法调用
-   **响应格式**: `ApiListResponse` 格式

**read-detail.ts, update.ts, delete.ts 路由对比:**

-   **目标获取**: 使用 `ctx.get('target')` 获取预加载对象
-   **权限检查**: 一致的权限验证逻辑
-   **更新处理**: update 中的数据合并逻辑

#### 6. 数据库迁移对比

**对比文件:**

-   `src/migrations/` 中的表创建方法

**检查要点:**

-   **表结构**: 字段定义、类型、约束
-   **索引**: 必要的索引创建
-   **关联**: 外键关系定义
-   **命名规范**: 表名、字段名格式

#### 7. 代码风格一致性检查

**格式化规范:**

-   **空行**: 导入分组间的空行、函数间空行

**命名规范:**

-   **变量命名**: camelCase，作用域相关的长度
-   **函数命名**: 动词开头的清晰命名
-   **类型命名**: PascalCase 接口/类型命名
-   **常量命名**: UPPER_SNAKE_CASE

**导入排序:**

-   **Node.js 内置模块**: `node:` 前缀
-   **第三方模块**: npm 包
-   **本地模块**: `~src/` 别名路径
-   **相对导入**: 同目录使用 `./`

#### 8. 错误处理一致性

**错误模式:**

-   **API 错误**: 统一使用 `ApiError` 类
-   **错误码**: 使用 `ErrorCode` 枚举值
-   **状态码**: HTTP 状态码的正确使用

## 审查要点

在对比时，请重点检查以下方面是否存在任何不一致：

-   **代码结构与逻辑**: 实现模式、函数定义、错误处理、逻辑流程是否一致？
-   **变量与函数命名**: 命名风格是否完全统一？
-   **代码风格**: 格式化、注释、空行等是否遵循相同规范？
-   **依赖导入与导出**: 模块的导入和导出方式是否一致？

## 最终目标

你需要帮助我将 `$ARGUMENTS` 模块打磨得与 `user` 模块在结构和风格上别无二致。

请开始审查并执行修改。
```

---

## English Version

```markdown
# Code Review and Modification

## Role

You are an extremely rigorous and detail-oriented code reviewer. Your task is to identify any inconsistencies in code implementation and fix them.

## Background

I previously asked you to create a new `$ARGUMENTS` module using the `user` module as a template. Now, I need you to conduct a strict review of the code you generated to ensure the new module completely follows the template's specifications in every detail.

## Core Task

Please compare each functionally equivalent file between the `$ARGUMENTS` module and the `user` module one by one, then generate a detailed review report.

## Review Process and Report Format

Your review report must be strictly organized according to the following structure:

### Code Review Report: `$ARGUMENTS` vs `user`

#### 1. Service Layer File Comparison

**Files to Compare:**

-   `src/services/user/*.ts` (template)
-   `src/services/$ARGUMENTS/*.ts` (under review)

**Check Points:**

-   **File Structure**: Ensure all required files are included (`create.ts`, `delete-by-id.ts`, `find-list.ts`, `find-list-and-count.ts`, `find-one.ts`, `find-one-by-id.ts`, `update.ts`, `index.ts`)
-   **Import Statements**: Check import path format and module reference consistency
-   **Function Definitions**: Use `export const functionName = async () => {}` format
-   **Type Definitions**: `CreateData` type uses `Pick<Model, 'field1' | 'field2'>` format
-   **ID Generation**: Use correct prefix format (User: 'U' + 10 digits)
-   **Database Operations**: Use `table('tableName')` syntax, error handling approach
-   **Context Retrieval**: Use `getContext()` or `getUserId()` to get user information
-   **Return Values**: create method calls `findOneById(id)` to return complete object
-   **index.ts Export**: Methods arranged alphabetically, service name format as `${ModuleName}Service`

#### 2. Router Layer File Comparison

**Files to Compare:**

-   `src/routers/user/*.ts` (template)
-   `src/routers/$ARGUMENTS/*.ts` (under review)

**Check Points:**

-   **File Structure**: Include (`create.ts`, `delete.ts`, `read-detail.ts`, `read-list.ts`, `update.ts`, `index.ts`)
-   **Route Organization**:
    -   ID route middleware pattern: Check ID format validation (11 characters long, correct prefix)
    -   Nested route structure: `idr` handles ID-based routes, `r` handles all routes
    -   Route mounting order: `detail`, `update`, `del` in `idr`; `list`, `create` in `r`
-   **Middleware**: ID validation logic, target setting, error handling
-   **Import/Export**: Unified import aliases (`{ r as create }`), variable type definitions
-   **Error Handling**: Use `ApiError` and correct error codes
-   **Response Format**: Correct generic types and status codes

#### 3. Schema Layer File Comparison

**Files to Compare:**

-   `src/schemas/user/*.ts` (template)
-   `src/schemas/$ARGUMENTS/*.ts` (under review)

**Check Points:**

-   **File Structure**: Include (`create.ts`, `update.ts`, `query.ts`, `index.ts`)
-   **Import Declaration**: `import { z } from 'zod/v4'` format
-   **Schema Definition**:
    -   create.ts: Required field validation rules
    -   update.ts: Optional fields (all fields add `.optional()`)
    -   query.ts: Query parameter definitions
-   **Validation Rule Consistency**: Same fields use same validation rules
-   **Export Format**: `export const CreateSchema = z.object({...})`
-   **index.ts Aggregation**: `${ModuleName}Schema` object containing `Create`, `Update`, `Query`

#### 4. Model File Comparison

**Files to Compare:**

-   `src/models/user.ts` (template)
-   `src/models/$ARGUMENTS.ts` (under review)

**Check Points:**

-   **Interface Definition**: `export interface ${ModuleName}Model {}`
-   **Field Specifications**:
    -   id: string (correct format)
    -   Business field definitions
    -   System fields: `creator_id`, `updater_id`, `created_at`, `updated_at`
-   **Optional Field Marking**: Optional marking for sensitive fields like `password?`
-   **Field Types**: Date type usage, null union types
-   **models/index.ts Export**: Check if new model is correctly exported

#### 5. Specific Route Implementation Comparison

**create.ts Route Comparison:**

-   **Type Definition**: `type CreateData = z.infer<typeof ${ModuleName}Schema.Create>`
-   **Validation Middleware**: `customZodValidator(${ModuleName}Schema.Create, 'json')`
-   **Business Logic**: Duplicate check logic, password hashing
-   **Error Handling**: Unified error code usage
-   **Response Format**: `ApiCreateResponse<${ModuleName}Model>` format

**read-list.ts Route Comparison:**

-   **Pagination Handling**: Use pagination query schema
-   **Service Call**: `findListAndCount` method call
-   **Response Format**: `ApiListResponse` format

**read-detail.ts, update.ts, delete.ts Route Comparison:**

-   **Target Retrieval**: Use `ctx.get('target')` to get preloaded object
-   **Permission Check**: Consistent permission validation logic
-   **Update Handling**: Data merging logic in update

#### 6. Database Migration Comparison

**Files to Compare:**

-   Table creation methods in `src/migrations/`

**Check Points:**

-   **Table Structure**: Field definitions, types, constraints
-   **Indexes**: Necessary index creation
-   **Relations**: Foreign key relationship definitions
-   **Naming Conventions**: Table name, field name formats

#### 7. Code Style Consistency Check

**Formatting Standards:**

-   **Blank Lines**: Blank lines between import groups, between functions

**Naming Conventions:**

-   **Variable Naming**: camelCase, scope-related length
-   **Function Naming**: Clear naming starting with verbs
-   **Type Naming**: PascalCase interface/type naming
-   **Constant Naming**: UPPER_SNAKE_CASE

**Import Sorting:**

-   **Node.js Built-in Modules**: `node:` prefix
-   **Third-party Modules**: npm packages
-   **Local Modules**: `~src/` alias paths
-   **Relative Imports**: Use `./` for same directory

#### 8. Error Handling Consistency

**Error Patterns:**

-   **API Errors**: Unified use of `ApiError` class
-   **Error Codes**: Use `ErrorCode` enum values
-   **Status Codes**: Correct use of HTTP status codes

## Review Focus Points

When comparing, please focus on checking whether the following aspects have any inconsistencies:

-   **Code Structure and Logic**: Are implementation patterns, function definitions, error handling, and logical flows consistent?
-   **Variable and Function Naming**: Is the naming style completely unified?
-   **Code Style**: Are formatting, comments, blank lines following the same specifications?
-   **Dependency Import and Export**: Are module import and export methods consistent?

## Final Goal

You need to help me polish the `$ARGUMENTS` module to be indistinguishable from the `user` module in structure and style.

Please start the review and execute modifications.
```
