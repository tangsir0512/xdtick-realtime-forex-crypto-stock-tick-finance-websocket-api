# Websocket 行情 API 地址说明

[English ](https://en.apis.alltick.co/integration-process/market-address-description/websocket-quotes-api-address-description)/ 中文

## 股票市场数据 WebSocket 订阅

**接口地址**

* **基本路径**: `/quote-stock-b-ws-api`
* **完整URL**: `wss://quote.alltick.co/quote-stock-b-ws-api`

**认证信息**

每次建立连接时，必须在 URL 中附加您的认证 token，如下所示：

```arduino
wss://quote.alltick.co/quote-stock-b-ws-api?token=您的token
```

**订阅说明**

连接成功后，您可以根据需要订阅特定的股票市场数据。详细的调用方法请参考我们的 WebSocket 接口列表。

***

## 外汇、加密货币与商品市场数据 WebSocket 订阅

**接口地址**

* **基本路径**: `/quote-b-ws-api`
* **完整URL**: `wss://quote.alltick.co/quote-b-ws-api`

**认证信息**

建立连接时，同样需要在 URL 中附加您的认证 token，以确保数据传输的安全性。正确的格式应如下：

```arduino
wss://quote.alltick.co/quote-b-ws-api?token=您的token
```

**订阅说明**

一旦连接建立，您即可根据需求订阅外汇、加密货币（数字货币）、以及商品（贵金属）的市场数据。具体的接口调用方式，请查看我们的 WebSocket 接口列表。

***

**注意事项**：为了您的账户安全，请确保妥善保管您的 token 信息。若需进一步帮助或有任何疑问，欢迎随时联系我们的技术支持团队。

***

#### AllTick 网站

{% hint style="info" %}
官方网站：[https://alltick.co/](https://alltick.co/)
{% endhint %}
