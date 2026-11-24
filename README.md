# 展票选择与分时换购资料

以下台账为合成数据，不涉及真实访客、供应商或展馆。CSV 采用 UTF-8，首行为字段名，空字段代表源资料未给出。标识仅在字段明示的实体范围内使用。`data/agreements.json` 是当期业务方提供的运营资料，`data/formats.json` 记录文件列顺序和确定的外键引用。

- `data/sku.csv` 记录票型及资源配比。列为 `sku`、`title`、`cents`、`required_people`、`main`、`experience`、`exchange`。
- `data/dates.csv` 记录各放票日期的共享资源与观测划分。列为 `run`、`day`、`kind`、`main_limit`、`experience_limit`、`partition`。
- `data/stock.csv` 记录各选择时点最新的可买数量，不是共享资源总量。列为 `run`、`minute`、`sku`、`shown_available`、`status`。
- `data/display.csv` 记录页面展示及是否有事先轮换支持。列为 `run`、`minute`、`sku`、`cents`、`ordinal`、`randomized_price`、`randomized_position`、`party_min`。
- `data/shops.csv` 记录购物机会、同组人数、渠道和选择启动记录。alias 只在同一放票日可对照渠道重报。列为 `shop`、`run`、`at`、`channel`、`people`、`audience`、`alias`、`engagement`。
- `data/tickets.csv` 记录曾请求支付的票及结果。空票型为没有选择。列为 `ticket`、`shop`、`run`、`sku`、`sold`、`state`、`rec_min`。
- `data/exchange.csv` 记录换购提议及实际确认。列为 `ticket`、`run`、`at`、`state`、`new_sku`、`acknowledgement`。
- `data/forward.csv` 记录后续档的已有售票及未确认预留，chosen_slot 是同一 run 内不同开放资源档。列为 `ticket`、`run`、`channel`、`sku`、`people`、`booked`、`state`、`chosen_slot`、`exchange_until`。
- `data/current_transactions.csv` 记录后续档观察，原单状态与事件分别记录。列为 `event`、`ticket`、`run`、`minute`、`channel`、`change`、`desired`、`state`。
- `data/plans.csv` 记录可比较的共享时隙配额，priority 为优先客群保留到约定分钟的名额。列为 `plan`、`run`、`slot`、`main`、`experience`、`priority`、`allow_transfer`。

使用 Python 3.11，无第三方依赖。用 `python3 -m unittest discover -s tests -v` 核对文件的可读性、列结构和确定引用，源文件保持只读。
