# EveryData 来源绑定清洗交接

> 生产继续提供现有EveryData采集工具，并已提供2个来源绑定清洗工具。每次执行仍须实时发现；
> 工具存在不证明特定账户已达标、激活或完成端到端实测。

## 正确入口

清洗只处理客户有权读取、仍保留在EveryInfra的EveryData结果。它不是免费的通用Gemini接口，
不接受脱离来源的任意文本、自定义prompt、模型选择、工具、外部URL或客户自定输出schema。

必须先调用MCP `tools/list`并读取清洗工具的实时`inputSchema`。当前共15个操作：

- 读取：`get_entitlement`、`get_source`、`get_source_fields`、`list_recipes`、`preview`、
  `list_jobs`、`find_job`、`get_job`、`list_units`、`get_result`、`export`。
- 动作：`activate`、`submit`、`cancel`、`delete_result`。

首期附赠权益有条件且有上限：可核净结算充值本金达到人民币500元的直客账户，可显式领取一个
30天周期；每UTC日最多1,000个成功单元、总计30,000个、每分钟5次execute提交、并发5个单元。
实际资格、激活、剩余额度及客户费用是否为零，只以实时权益响应为准。

## 发现与恢复

1. 只读查询权益，不自动领取。
2. 解析EveryData `source_ref`，读取服务端`source_version`，发现不含样例值的有界字段路径/类型。
3. 发现固定配方并预览选中字段；字段推断不等于可执行证明。
4. 领取与提交是两个独立显式动作；持久保存提交幂等键。
5. 刷新或回执未知时，用`list_jobs`或原幂等键`find_job`找回原任务。404不能证明原提交未受理，
   不得自动重提。
6. 导出前读取原任务、单元及结果；partial导出、取消和删除均是独立选择。

线上未发现清洗时，正常返回EveryData采集结果并明确清洗不可用；不得静默改送
`everyinfra_chat`。
