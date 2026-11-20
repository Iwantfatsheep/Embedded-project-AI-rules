# 嵌入式项目通用规范

这是一份企业级嵌入式项目通用工程规范，用于约束 MCU/RTOS/裸机嵌入式 C 项目的目录结构、分层架构、模块边界、编码规范、运行时规范、质量策略和 agent 实现行为。

## 定位

- MUST: 项目级规范负责约束所有模块都必须遵守的工程秩序。
- MUST: 模块级规范只负责补充某个具体模块的实现细节。
- MUST: 当模块级规范与项目级规范冲突时，必须优先遵守项目级规范。
- MUST: 本模板安装后会成为目标项目的 `.trellis/spec/` 起点。
- MUST NOT: 不允许把本 spec 当作某个具体业务功能的实现说明。

## 推荐阅读顺序

1. 先读 `index.md`
2. 再读 `architecture/index.md`
3. 编码任务读 `coding/index.md`
4. 涉及 RTOS、ISR、DMA、状态机时读 `runtime/index.md`
5. 涉及错误处理、测试和 review 时读 `quality/index.md`
6. agent 实现代码前必须读 `agent/index.md`
7. 具体模块设计参考 `modules/index.md`

## 安装路径约束

- MUST: 本模板目录内容必须直接对应最终 `.trellis/spec/` 内容。
- MUST NOT: `marketplace/specs/embedded-project/` 内部不得再额外包含一层 `spec/`。
- MUST NOT: `marketplace/specs/embedded-project/` 内部不得再额外包含一层 `embedded-project/`。

## 在嵌入式工程中的放置位置

将本规范放在目标嵌入式工程根目录下的 `.trellis/spec/`，目录应如下：

```text
your_embedded_project/
└── .trellis/
	 └── spec/
		  ├── README.md
		  ├── index.md
		  ├── architecture/
		  ├── coding/
		  ├── runtime/
		  ├── quality/
		  ├── agent/
		  ├── modules/
		  └── examples/
```

注意：不要在 `.trellis/spec/` 下再嵌套一层 `embedded-project/`。

## 如何使用这份规范

1. 初始化规范目录
	- 将 `marketplace/specs/embedded-project/` 下全部文件复制到目标工程 `.trellis/spec/`。

2. 实现前先定位任务
	- 先阅读 `index.md`，根据任务类型加载对应领域 `index.md`。
	- 涉及多个领域时，必须同时阅读多个领域规范。

3. 开始实现前做三件事
	- 先判断代码所属层级（`app/`、`services/`、`protocols/`、`drivers/` 等）。
	- 确认依赖方向不反转，且通过 public API 访问下层能力。
	- 明确错误处理、并发/ISR 影响和最小验证方式。

4. 修改完成后执行自检
	- 按 `quality/review-checklist.md` 逐项自检。
	- 在交付说明中记录验证命令与结果（参考 `quality/testing-and-check-strategy.md`）。

5. 需要新增模块规范时
	- 使用 `modules/module-spec-template.md` 创建模块级 spec。
	- 模块级 spec 只能补充项目级规则，不能覆盖项目级规则。

