# 代码规范 (CODING_RULES)

---

## 命名约定

### 函数 / 方法

- **Python**：`snake_case`
- **TypeScript/JavaScript**：`camelCase`
- 名称应为动词开头，表明意图（如 `fetch_user`、`parseResponse`）

### 变量

- 与函数命名风格一致
- 布尔值以 `is_`、`has_`、`can_` 前缀（如 `is_ready`、`hasPermission`）
- 避免单字母变量（循环计数器 `i`/`j` 除外）

### 文件 / 模块

- **Python**：`snake_case.py`
- **TypeScript**：`kebab-case.ts` 或 `PascalCase.tsx`（React 组件）

### 常量

- 全大写 + 下划线：`MAX_RETRY_COUNT`、`API_BASE_URL`

---

## 模块结构

### Python 后端（src/copaw/）

```
src/copaw/
├── agents/       # Agent 定义与技能
├── cli/          # CLI 入口
├── services/     # 业务逻辑
├── utils/        # 通用工具函数
└── __init__.py
```

### TypeScript 前端（console/）

```
console/src/
├── api/          # API 请求模块
├── components/   # 通用组件
├── layouts/      # 布局组件
├── pages/        # 页面组件
├── locales/      # 国际化
└── main.tsx      # 入口文件
```

---

## 注释要求

- **公共 API** 必须有文档注释（Python: docstring，TS: JSDoc）
- **复杂逻辑**：用行内注释解释"为什么"，而不是"做什么"
- **TODO**：格式为 `# TODO(zj): 描述`，必须关联 issue 编号

---

## 禁止事项

### 通用

- 禁止提交包含硬编码密钥、密码、Token 的代码
- 禁止 `console.log` / `print` 调试语句遗留在生产代码中
- 禁止空的 catch 块（必须至少记录错误日志）

### Python 专项

- 禁止裸 `except:`（必须指定异常类型）
- 禁止可变默认参数（如 `def f(x=[]):` ）
- 必须使用类型注解（Python 3.10+）

### TypeScript 专项

- 禁止 `any` 类型（使用 `unknown` + 类型守卫）
- 禁止 `@ts-ignore`（优先修复类型错误）
- 禁止非空断言 `!`（使用可选链 `?.`）

---

## 测试要求

- 每个公共函数必须有对应单元测试
- 测试文件与源文件同目录（或放在 `tests/` 目录）
- 测试名称格式：`test_<功能>_<场景>_<期望结果>`
- 覆盖率目标：核心模块 ≥ 80%
