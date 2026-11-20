# 内存和资源管理规范

## Buffer

- MUST: 所有 buffer 都必须有明确所有者。
- MUST: 所有 buffer 读写必须检查长度。
- MUST: ring buffer、DMA buffer、协议帧 buffer 必须说明生产者、消费者和生命周期。
- MUST NOT: 不允许无边界 `memcpy()`、`strcpy()`、`sprintf()`。
- SHOULD: 优先使用 `snprintf()`、带长度参数的 copy 函数或项目封装。

## 动态内存

- MUST: 是否允许 `malloc()` / `free()` 必须由项目配置明确。
- MUST: 如果允许动态内存，必须说明失败路径和释放责任。
- MUST NOT: 不允许在 ISR 中调用 `malloc()` 或 `free()`。
- MUST NOT: 不允许在实时性关键路径中反复申请和释放内存。
- SHOULD: MCU 项目优先使用静态分配、内存池或编译期固定容量。

## 资源所有权

- MUST: 外设实例、mutex、queue、timer、DMA channel 必须有唯一管理者。
- MUST: 共享资源必须有锁、临界区、消息队列或单写者规则。
- MUST: 资源初始化失败必须能够回滚或进入明确故障状态。
- MUST NOT: 不允许多个模块无边界地直接操作同一个硬件资源。

## 栈

- MUST: 关键 task 的栈大小必须有估算依据（如最坏调用深度、局部变量占用或历史实测余量），不得凭经验随意设置。
- SHOULD: 项目应启用栈溢出检测机制（如 RTOS 栈水位检查、编译器栈保护或链接期栈溢出告警）。
- MUST NOT: 不允许在栈上分配大小不确定或随输入增长的缓冲区。

## 持久化数据

- MUST: 持久化数据必须具备版本、长度和校验策略。
- MUST: 参数默认值、升级迁移和损坏恢复必须有明确路径。
- MUST: 如项目支持固件升级，升级包必须有完整性校验（如 CRC/哈希）和合法性校验（如签名验证），不得直接写入未经校验的固件数据。
- MUST NOT: `app/` 不得直接写 Flash 寄存器保存配置。

