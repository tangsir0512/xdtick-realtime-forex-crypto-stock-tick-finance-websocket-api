# 最新成交价(实时逐笔Tick数据、当前价、最新价)批量订阅

[English ](https://en.apis.alltick.co/websocket-api/stock-websocket-interface-api/transaction-quote-subscription)/ 中文

## 接口说明

该接口支持批量订阅产品的最新成交价(实时逐笔Tick数据，也是当前价、最新价)，不支持历史成交价格(历史逐笔tick数据)。

该接口特性为对于每一个websocket连接，每发送一次该请求，后台会默认覆盖上一次订阅请求（例如，如果您最初订阅了A、B、C这三只产品，想要追加订阅E、F、G，则需要重新发送一次A、B、C、E、F、G），订阅成功后会进行推送数据。

{% stepper %}
{% step %}
### 注意（1）

订阅一次成功后，不需要再频繁的发起订阅请求，要求每10秒发送一次心跳，接口就会实时推送数据，在30秒内如果没有收到心跳请求，就会认为超时，断开请求者的websocket连接。
{% endstep %}

{% step %}
### 注意（2）

接入时，客户可增加断开自动重连的逻辑，确保因网络等原因断开可自动重连。
{% endstep %}
{% endstepper %}

## 接口限制

{% stepper %}
{% step %}
请务必阅读：[Websocket限制说明](https://apis.alltick.co/integration-process/interface-restriction-description/websocket-interface-limitations)
{% endstep %}

{% step %}
请务必阅读：[错误码说明](https://apis.alltick.co/integration-process/interface-restriction-description/error-code-description)
{% endstep %}
{% endstepper %}

## 接口地址

**1、外汇、贵金属、加密货币、原油、CFD指数、商品接口地址：**

* 基本路径: /tick-ws-api
* 完整URL: wss://api.xdtick.com/tick-ws-api

## 请求示例

连接成功后，您可以根据需要订阅特定的股票市场数据。详细的调用方法请参考下面的文档说明。

**1、外汇、贵金属、加密货币、原油、CFD指数、商品请求示例：**

每次建立连接时，必须在URL中附加您的认证token，如下所示：

wss://api.xdtick.com/tick-ws-api?token=您的token

连接成功后，您可以根据需要订阅特定的外汇、加密货币、贵金属、商品数据。详细的调用方法请参考下面的文档说明.

## 请求-协议号：22004

#### json定义

| 字段      | 名称   | 类型      | 必填项 | 说明                |
| ------- | ---- | ------- | --- | ----------------- |
| cmd\_id | 协议号  | integer | 是   | 逐笔订阅请求协议号固定：22004 |
| codes   | 产品列表 | array   | 是   | 具体格式见下面symbol定义   |

#### symbol定义

| 字段   | 名称 | 类型     | 必填项 | 说明                                                                         |
| ---- | -- | ------ | --- | -------------------------------------------------------------------------- |
| code | 代码 | string | 是   | 具体内容，请查阅code列表：[ 点击code列表](../../jie-ru-liu-cheng/chan-pin-code-lie-biao/) |

### 数据结构(json)

{% code title="请求示例.json" %}
```json
{
    "cmd_id":22004,
    "codes": "BTCUSD,ETHUSD"
}
```
{% endcode %}

## 应答-协议号：22005

### 数据结构(json)

{% code title="应答示例.json" %}
```json
{
    "msg": "successful",
    "code": 200,
    "data": {
        "tick_list": [
            {
                "volume": 0.99173000,
                "code": "BTCUSD",
                "price": 89262.11000000,
                "turnover": 88523.9123503000000000,
                "timestamp": 1769616358
            },
            {
                "volume": 12.13900000,
                "code": "ETHUSD",
                "price": 2966.71000000,
                "turnover": 36012.8926900000000000,
                "timestamp": 1769616358
            }
        ]
    }
}
```
{% endcode %}

## 推送-协议号：22998

#### data定义

| 字段          | 名称    | 类型     | 说明                                                                                                                                               |
| ----------- | ----- | ------ | ------------------------------------------------------------------------------------------------------------------------------------------------ |
| code        | 代码    | string | 具体内容，请查阅code列表： [点击code列表](https://docs.google.com/spreadsheets/d/1avkeR1heZSj6gXIkDeBt8X3nv4EzJetw4yFuKjSDYtA/edit?gid=495387863#gid=495387863) |
| timestamp   | 报价时间戳 | string | 单位毫秒                                                                                                                                             |
| price       | 成交价   | string | 最新成交价                                                                                                                                            |
| volume      | 成交量   | string | 最新一口成交价对应的成交量                                                                                                                                    |
| quoteVolume | 成交额   | string | 成交额：\n1、外汇、贵金属、能源不返回成交额，可自行根据每次推送的数据计算，计算公式：turnover = price \* volume\n2、股票、加密货币正常返回成交额。                                                        |

### 数据结构（json）

{% code title="推送示例.json" %}
```json
{
    "cmd_id":22998,
    "data":{
        "code": "BTCUSD",
        "timestamp": "1605509068",
        "price": "651.12",
        "volume": "300",
        "quoteVolume": "12345.6"
    }
}
```
{% endcode %}

{% hint style="info" %}
官方网站：[https://xdtick.com/](https://xdtick.com/)
{% endhint %}
