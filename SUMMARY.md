# Summary

* [欢迎](README.md)

## 接入流程
* [流程说明](docs/flow_instructions.md)
* [行情地址说明](docs/market_address.md)
* [HTTP 行情 API 地址说明](docs/http_market_api.md)
* [Websocket 行情 API 地址说明](docs/ws_market_api.md)
* [Token 申请](docs/token_request.md)

## 接口限制说明
* [HTTP 接口限制](docs/http_interface_limitations.md)
* [Websocket 接口限制](docs/ws_interface_limitations.md)
* [错误码说明](docs/error_codes.md)

## 通用标准头说明
* [HTTP 通用标准头](docs/http_common_headers.md)
* [Websocket 通用标准头](docs/ws_common_headers.md)

## 产品 Code 列表
* [A股](docs/product_code/a_stock.md)
* [港股](docs/product_code/hk_stock.md)
* [美股](docs/product_code/us_stock.md)
* [加密货币(数字币)](docs/product_code/crypto.md)
* [商品(贵金属)](docs/product_code/commodity.md)
* [外汇](docs/product_code/forex.md)

## REST API
* [HTTP 请求示例](docs/rest/http_request_example.md)
* [HTTP接口API](docs/rest/http_api.md)
* [GET 单产品历史K线查询（最高、最低、开盘、收盘价）](docs/rest/get_single_kline.md)
* [POST 批量查询产品最新2根K线（最高、最低、开盘、收盘价）](docs/rest/post_batch_kline.md)
* [GET 最新盘口(最新深度、Order Book)查询](docs/rest/get_orderbook.md)
* [GET 最新成交价(最新tick、当前价、最新价)批量查询](docs/rest/get_latest_tick.md)
* [GET 股票产品基础信息批量查询](docs/rest/get_stock_basic_info.md)
* [GET 停复牌信息查询接口](docs/rest/get_suspend_resume.md)
* [涨跌幅、休市、假期、涨停跌停、新股上市和退市](docs/rest/market_status.md)

## Websocket API
* [Websocket 请求示例](docs/ws/ws_request_example.md)
* [Websocket接口API](docs/ws/ws_api.md)
* [最新成交价(实时逐笔Tick数据、当前价、最新价)批量订阅](docs/ws/sub_latest_tick.md)
* [最新盘口(实时逐笔深度、Order Book)订阅](docs/ws/sub_orderbook.md)
* [取消报价订阅](docs/ws/unsubscribe.md)
* [心跳](docs/ws/heartbeat.md)
* [K线推送(不支持)](docs/ws/kline_push.md)

## FAQs
* [基础使用](docs/faqs/basic_usage.md)
* [AllTick 提供哪些类型的金融数据？](docs/faqs/types_of_data.md)
* [如何获取AllTick的API密钥？](docs/faqs/get_api_key.md)
* [AllTick的数据更新频率是多少？](docs/faqs/data_frequency.md)
* [如何在我的应用程序中集成AllTick的数据？](docs/faqs/integration.md)
* [AllTick支持哪些编程语言进行API调用？](docs/faqs/supported_languages.md)
* [我可以使用AllTick的数据进行商业用途吗？](docs/faqs/commercial_use.md)
* [如何联系AllTick的客户支持？](docs/faqs/contact_support.md)
* [AllTick的API有请求限制吗？](docs/faqs/api_limits.md)
* [如何报告数据问题或API故障？](docs/faqs/report_issues.md)
* [AllTick提供实时数据还是延迟数据？](docs/faqs/realtime_or_delayed.md)

## 订阅与账户管理
* [如何注册AllTick账户？](docs/subscription_account/register.md)
* [AllTick有免费试用期吗？](docs/subscription_account/free_trial.md)
* [如何取消AllTick的订阅服务？](docs/subscription_account/cancel.md)
* [我的订阅包括哪些服务？](docs/subscription_account/services.md)
* [如何升级我的AllTick订阅计划？](docs/subscription_account/upgrade.md)
* [如何更改我的账户信息？](docs/subscription_account/change_info.md)
* [我忘记了我的登录密码，该怎么办？](docs/subscription_account/forgot_password.md)
* [如何保护我的AllTick账户安全？](docs/subscription_account/security.md)
* [是否可以多人共享一个AllTick账户？](docs/subscription_account/multi_user.md)
* [我的订阅可以退款吗？](docs/subscription_account/refund.md)

## 数据使用与技术问题
* [如何使用AllTick的WebSocket服务？](docs/technical/ws_usage.md)
* [AllTick的API支持哪些数据格式？](docs/technical/data_format.md)
* [如何处理AllTick数据的高频更新？](docs/technical/high_frequency.md)
* [我在使用API时遇到了技术问题，该怎么解决？](docs/technical/troubleshooting.md)
* [如何确保从AllTick接收的数据的准确性？](docs/technical/data_accuracy.md)
* [AllTick是否提供历史数据查询？](docs/technical/historical_data.md)
* [如何限制我的数据使用量以避免超出订阅限制？](docs/technical/data_limits.md)
* [AllTick的API是否支持批量请求？](docs/technical/batch_request.md)
* [如何获取特定金融市场的实时通知和警报？](docs/technical/alerts.md)
* [AllTick是否提供数据分析和可视化工具？](docs/technical/data_analysis.md)
