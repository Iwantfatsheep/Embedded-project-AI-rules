# Agent 实现规则

## 1. 实现前必须回答的问题

在写任何代码前，agent 必须先判断：

1. 这个功能属于 `app/`、`services/`、`protocols/`、`middleware/`、`drivers/`、`bsp/`、`platform/`、`vendor/`、`common/` 还是 `config/`？
2. 是否已有模块可以复用？
3. 是否需要新增 public API？
4. 是否会产生反向依赖？
5. 是否涉及 ISR、DMA、RTOS task 或共享资源？
6. 是否需要错误码、日志、诊断、测试或 mock？
7. 是否需要新增模块级 spec？

## 2. 实现过程规则

- MUST: 新增代码前必须先确定所属层级。
- MUST: 新增文件必须放入正确目录。
- MUST: 新增函数必须属于正确模块。
- MUST: 必须先复用已有 public API。
- MUST: 修改代码时不得破坏现有模块边界。
- MUST NOT: 不得绕过 public API 直接访问其他模块内部状态。
- MUST: 具体分层禁止事项（driver/protocol/app 边界、ISR 限制等）以 `architecture/architecture-layers.md` 和 `runtime/interrupt-and-dma-rules.md` 为准，本文件不重复列出。

## 3. 输出要求

每次完成实现后，agent 必须输出：

1. 修改文件列表；
2. 每个文件所属层级；
3. 新增或修改的 public API；
4. 是否存在跨层依赖；
5. 错误处理策略；
6. 并发或 ISR 影响；
7. 测试或验证方式；
8. 未完成或需要人工确认的问题。

## 4. 不确定时的处理

- MUST: 如果无法判断模块应该放在哪一层，必须停止并标记 `NEED_CONFIRMATION`。
- MUST: 如果原有项目结构与本 spec 冲突，必须说明冲突并请求人工确认。
- MUST NOT: 不允许在架构不明确时擅自创建不合理目录。

