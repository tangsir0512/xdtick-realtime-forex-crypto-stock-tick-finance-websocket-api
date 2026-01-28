# GET 单产品历史K线查询（最高、最低、开盘、收盘价）

[English ](https://en.apis.alltick.co/rest-api/stock-http-interface-api/get-k-line-query)/ 中文

## GET /kline

## 接口说明

该接口可用来查询历史k线，但每次只能查询一个产品，<mark style="color:red;">建议将查询到的历史K线缓存本地数据库。</mark>

使用HTTP接口获取K线的客户，建议将 /kline 和 /batch-kline 这2个接口结合使用，步骤如下：

{% stepper %}
{% step %}
### 从 /kline 获取并存储历史数据

首先，通过 /kline 接口轮询请求历史数据并存储到本地数据库，后续历史数据可直接从客户的数据库获取，无需再通过接口请求。
{% endstep %}

{% step %}
### 使用 /batch-kline 批量更新最新数据

然后，后续持续使用 /batch-kline 接口批量请求多个产品的最新2根K线，并将数据更新到数据库。

这种方式能够快速更新最新的K线，同时避免频繁请求历史K线造成频率受到限制。
{% endstep %}
{% endstepper %}

## 请求频率

<table data-full-width="false"><thead><tr><th width="88.99993896484375">计划</th><th width="196.0001220703125">单独请求</th><th width="472">同时请求多个http接口</th></tr></thead><tbody><tr><td>免费</td><td>每10秒，只能1次请求</td><td><p>1、10秒只能请求1个接口</p><p><mark style="color:red;">2、多个接口请求时，需注意/batch-kline接口需间隔10秒</mark><br>3、所有接口相加，1分钟最大请求10次(6秒1次)<br>4、每天总共最大可请求14400次，超过则第二天凌晨恢复使用</p></td></tr><tr><td>基础</td><td>每1秒，只能1次请求</td><td><p>1、同1秒只能请求1个接口</p><p><mark style="color:red;">2、多个接口请求时，需注意/batch-kline接口需间隔3秒</mark><br>3、所有接口相加，1分钟最大请求60次(1秒1次)<br>4、每天总共最大可请求86400次，超过则第二天凌晨恢复使用</p></td></tr><tr><td>高级</td><td>每1秒，最大可10次请求</td><td><p>1、所以接口相加，每1秒可请求10次</p><p><mark style="color:red;">2、多个接口请求时，需注意/batch-kline接口需间隔2秒</mark><br>3、所有接口相加，1分钟最大请求600次(1秒10次)<br>4、每天总共最大可请求864000次，超过则第二天凌晨恢复使用</p></td></tr><tr><td>专业</td><td>每1秒，最大可20次请求</td><td><p>1、所以接口相加，每1秒可请求20次</p><p><mark style="color:red;">2、多个接口请求时，需注意/batch-kline接口需间隔1秒</mark><br>3、所有接口相加，1分钟最大请求1200次(1秒20次)<br>4、每天总共最大可请求1728000次，超过则第二天凌晨恢复使用</p></td></tr><tr><td>全部港股</td><td>每1秒，最大可20次请求</td><td><p>1、所以接口相加，每1秒可请求20次</p><p><mark style="color:red;">2、多个接口请求时，需注意/batch-kline接口需间隔1秒</mark><br>3、所有接口相加，1分钟最大请求1200次(1秒20次)<br>4、每天总共最大可请求1728000次，超过则第二天凌晨恢复使用</p></td></tr><tr><td>全部A股</td><td>每1秒，最大可20次请求</td><td><p>1、所以接口相加，每1秒可请求20次</p><p><mark style="color:red;">2、多个接口请求时，需注意/batch-kline接口需间隔1秒</mark><br>3、所有接口相加，1分钟最大请求1200次(1秒20次)<br>4、每天总共最大可请求1728000次，超过则第二天凌晨恢复使用</p></td></tr><tr><td>全部美股</td><td>每1秒，最大可20次请求</td><td><p>1、所以接口相加，每1秒可请求20次</p><p><mark style="color:red;">2、多个接口请求时，需注意/batch-kline接口需间隔1秒</mark><br>3、所有接口相加，1分钟最大请求1200次(1秒20次)<br>4、每天总共最大可请求1728000次，超过则第二天凌晨恢复使用</p></td></tr></tbody></table>

## 接口限制

1、请务必阅读：[HTTP接口限制说明](../../jie-ru-liu-cheng/jie-kou-xian-zhi-shuo-ming/http-jie-kou-xian-zhi.md)

2、请务必阅读：[错误码说明](../../jie-ru-liu-cheng/jie-kou-xian-zhi-shuo-ming/cuo-wu-ma-shuo-ming.md)

## 接口地址

**1、外汇、贵金属、加密货币、原油、CFD指数、商品接口地址：**

* 基本路径: /tick-api/kline
* 完整URL: [https://api.xdtick.com/tick-api/kline](https://api.xdtick.com/tick-api/kline)

## 请求示例

**1、外汇、贵金属、加密货币、原油、CFD指数、商品请求示例：**

在发送查询请求时，必须包含方法名和token信息。一个请求的示例如下：\
https://api.xdtick.com/tick-api/kline?code=BTCUSD\&klineType=1min\&size=2

## 请求参数

| 名称        | 位置     | 类型     | 必选 | 说明                                                                                   |
| --------- | ------ | ------ | -- | ------------------------------------------------------------------------------------ |
| X-API-KEY | header | string | 是  | 用户token                                                                              |
| code      | query  | string | 是  | 请查看code列表，选择你要查询的code：[\[点击code列表\]](../../jie-ru-liu-cheng/chan-pin-code-lie-biao/) |
| klineType | query  | string | 是  | 1min=1分钟,5min=5分钟，15min=15分钟，30min=30分钟，60min=1小时，1d=1天，1w=1周，1m=1月                  |
| size      | query  | Int    | 否  | 表示查询多少根K线，每次最大请求1000根，可根据时间戳循环往前请求                                                   |

## query 请求参数 示例

```
{
  "code": "BTCUSD",
  "klineType": "1min",
  "size": 500
}
```

## 返回示例

```
{
    "msg": "successful",
    "code": 200,
    "data": {
        "code": "BTCUSD",
        "klineType": "1min",
        "klineList": [
            {
                "volume": 0.99173000,
                "high": 89287.17000000,
                "low": 89262.10000000,
                "startTime": "2026-01-21T18:46:00",
                "quoteVolume": 88536.41615210,
                "changeAmount": -25.06000000,
                "changeRate": -0.00028067,
                "close": 89262.11000000,
                "open": 89287.17000000,
                "timestamp": 1768992360000
            },
            {
                "volume": 5.05343000,
                "high": 89310.63000000,
                "low": 89287.16000000,
                "startTime": "2026-01-21T18:45:00",
                "quoteVolume": 451249.76464880,
                "changeAmount": -23.46000000,
                "changeRate": -0.00026268,
                "close": 89287.17000000,
                "open": 89310.63000000,
                "timestamp": 1768992300000
            }
        ]
    }
}
```

## 返回结果

| 状态码 | 状态码含义 | 说明 | 数据模型   |
| --- | ----- | -- | ------ |
| 200 | OK    | OK | Inline |

## 返回数据结构

<table data-full-width="false"><thead><tr><th width="137">名称</th><th width="186">类型</th><th width="105.5999755859375">必选</th><th>说明</th></tr></thead><tbody><tr><td>» msg</td><td>string</td><td>true</td><td></td></tr><tr><td>» data</td><td>object</td><td>true</td><td></td></tr><tr><td>»» code</td><td>string</td><td>true</td><td>产品代码</td></tr><tr><td>»» klineType</td><td>string</td><td>true</td><td>1min=1分钟,5min=5分钟，15min=15分钟，30min=30分钟，60min=1小时，1d=1天，1w=1周，1m=1月</td></tr><tr><td>»» klineList</td><td>[object]</td><td>true</td><td></td></tr><tr><td>»»» timestamp</td><td>string</td><td>true</td><td>该K线时间戳</td></tr><tr><td>»»» open</td><td>string</td><td>true</td><td>该K线开盘价</td></tr><tr><td>»»» close</td><td>string</td><td>true</td><td>该K线收盘价： 1、交易时段内，最新一根K线，该价格也是最新成交价 2、休市期间，最新一根K线，该价格是收盘价</td></tr><tr><td>»»» high</td><td>string</td><td>true</td><td>该K线最高价</td></tr><tr><td>»»» low</td><td>string</td><td>true</td><td>该K线最低价</td></tr><tr><td>»»» volume</td><td>string</td><td>true</td><td>该K线成交数量</td></tr><tr><td>»»» changeAmount</td><td>string</td><td>true</td><td>该K线涨跌金额</td></tr><tr><td>»»» changeRate</td><td>string</td><td>true</td><td>该K线涨跌比例</td></tr><tr><td>»»» quoteVolume</td><td>string</td><td>true</td><td>该K线成交额</td></tr></tbody></table>

#### XdTick网站

{% hint style="info" %}
官方网站：[https://xdtick.com/](https://xdtick.com/)
{% endhint %}
