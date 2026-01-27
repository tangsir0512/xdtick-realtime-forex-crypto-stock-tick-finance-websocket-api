# HTTP 行情 API 地址说明

[English ](https://en.apis.alltick.co/integration-process/market-address-description/http-quotes-api-address-description)/ 中文

## API 地址说明

### 外汇、加密货币（数字币）、商品（贵金属） HTTP 接口 API 地址

接口路径: /tick-api（外汇、加密货币、商品查询 API）

查询 API 使用 HTTPS，完整的 base URL 为：\
https://api.xdtick.com/tick-api

每次查询请求都需要带上方法名和 token 信息。

示例：

* 单产品请求 K 线： [http:///api.xdtick.com/tick-api/kline?code=BTCUSD\&klineType=1min\&size=2](http://api.xdtick.com/tick-api/kline?code=BTCUSD\&klineType=1min\&size=2)
* 批产品请求 K 线（注意：批量请求时，请求参数放在 body 中）：  [http:///api.xdtick.com/tick-api/batch-kline](http://api.xdtick.com/tick-api/batch-kline)
* 请求最新成交价：[http:///api.xdtick.com/tick-api/trade-tick](http://api.xdtick.com/tick-api/trade-tick)

具体调用方式，请查看 http 接口列表。

***

{% hint style="info" %}
官方网站：[https://xdtick.com/](https://xdtick.com/)
{% endhint %}
