# HTTP 行情 API 地址说明

[English ](https://en.apis.alltick.co/integration-process/market-address-description/http-quotes-api-address-description)/ 中文

## API 地址说明

### 股票 HTTP 接口 API 地址

接口路径: `/quote-stock-b-api`（股票查询 API）

查询 API 使用 HTTPS，完整的 base URL 为：\
https://quote.alltick.co/quote-stock-b-api

每次查询请求都需要带上方法名和 token 信息。

示例：

* 单产品请求 K 线： https://quote.alltick.co/quote-stock-b-api/kline?token=你的token\&query=queryData
* 批产品请求 K 线（注意：批量请求时，请求参数放在 body 中）： https://quote.alltick.co/quote-stock-b-api/batch-kline?token=你的token
* 请求最新成交价： https://quote.alltick.co/quote-stock-b-api/trade-tick?token=你的token\&query=queryData
* 请求最新盘口： https://quote.alltick.co/quote-stock-b-api/depth-tick?token=你的token\&query=queryData

具体调用方式，请查看 http 接口列表。

### 外汇、加密货币（数字币）、商品（贵金属） HTTP 接口 API 地址

接口路径: `/quote-b-api`（外汇、加密货币、商品查询 API）

查询 API 使用 HTTPS，完整的 base URL 为：\
https://quote.alltick.co/quote-b-api

每次查询请求都需要带上方法名和 token 信息。

示例：

* 单产品请求 K 线： https://quote.alltick.co/quote-b-api/kline?token=你的token\&query=queryData
* 批产品请求 K 线（注意：批量请求时，请求参数放在 body 中）： https://quote.alltick.co/quote-b-api/batch-kline?token=你的token
* 请求最新成交价： https://quote.alltick.co/quote-b-api/trade-tick?token=你的token\&query=queryData
* 请求最新盘口： https://quote.alltick.co/quote-b-api/depth-tick?token=你的token\&query=queryData

具体调用方式，请查看 http 接口列表。

***

{% hint style="info" %}
官方网站：https://alltick.co/
{% endhint %}
