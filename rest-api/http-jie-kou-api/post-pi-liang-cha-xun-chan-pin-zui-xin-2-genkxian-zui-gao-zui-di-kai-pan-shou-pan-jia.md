# POST 批量查询产品最新2根K线（最高、最低、开盘、收盘价）

English / 中文

## POST /batch-kline

## 接口说明

该接口可以一次性批量查询多个产品，且可批量一次性查询多个k线类型（k线类型指的是1分钟，15分钟，30分钟等），<mark style="color:red;">**但只能批量查询最新的2根k线。**</mark>

使用HTTP接口获取K线的客户，建议将 /kline 和 /batch-kline 这2个接口结合使用，步骤如下：

{% stepper %}
{% step %}
### 步骤一

通过 /kline 接口轮询请求历史数据并存储到本地数据库，后续历史数据可直接从客户的数据库获取，无需再通过接口请求。
{% endstep %}

{% step %}
### 步骤二

后续持续使用 /batch-kline 接口批量请求多个产品的最新2根K线，并将数据更新到数据库。

这种方式能够快速更新最新的K线，同时避免频繁请求历史K线造成频率受到限制。
{% endstep %}
{% endstepper %}

## 请求频率

<table data-full-width="false"><thead><tr><th width="89">计划</th><th width="298.2000732421875">单独请求</th><th width="375">同时请求多个http接口</th></tr></thead><tbody><tr><td>免费</td><td>1、每10秒，可1次请求<br>2、每次可批量查询10组数据，每1组数据=1只产品数量+1种K线类型，例如同时获取BTCUSDT的1分钟k线和5分钟k线，这就是2组数据</td><td>1、10秒只能请求1个接口<br>2、所有接口相加，1分钟最大请求10次(6秒1次)<br><mark style="color:red;">3、需注意/batch-kline接口需间隔10秒</mark><br>4、每天总共最大可请求14400次，超过则第二天凌晨恢复使用</td></tr><tr><td>基础</td><td>1、每3秒，只能1次请求<br>2、每次可批量查询100组数据，每1组数据=1只产品数量+1种K线类型，例如同时获取BTCUSDT的1分钟k线和5分钟k线，这就是2组数据</td><td>1、同1秒只能请求1个接口<br>2、所有接口相加，1分钟最大请求60次(1秒1次)<br><mark style="color:red;">3、需注意/batch-kline接口需间隔3秒</mark><br>4、每天总共最大可请求86400次，超过则第二天凌晨恢复使用</td></tr><tr><td>高级</td><td>1、每2秒，只能1次请求<br>2、每次可批量查询200组数据，每1组数据=1只产品数量+1种K线类型，例如同时获取BTCUSDT的1分钟k线和5分钟k线，这就是2组数据</td><td>1、所有接口相加，1分钟最大请求600次(1秒10次)<br><mark style="color:red;">2、需注意/batch-kline接口需间隔2秒</mark><br>3、每天总共最大可请求864000次，超过则第二天凌晨恢复使用</td></tr><tr><td>专业</td><td>1、每1秒，只能1次请求<br>2、每次可批量查询500组数据，每1组数据=1只产品数量+1种K线类型，例如同时获取BTCUSDT的1分钟k线和5分钟k线，这就是2组数据</td><td>1、所有接口相加，1分钟最大请求1200次(1秒20次)<br><mark style="color:red;">2、需注意/batch-kline接口需间隔1秒</mark><br>3、每天总共最大可请求1728000次，超过则第二天凌晨恢复使用</td></tr></tbody></table>

## 接口限制

1、请务必阅读：[HTTP接口限制说明](../../jie-ru-liu-cheng/jie-kou-xian-zhi-shuo-ming/http-jie-kou-xian-zhi.md)

2、请务必阅读：[错误码说明](../../jie-ru-liu-cheng/jie-kou-xian-zhi-shuo-ming/cuo-wu-ma-shuo-ming.md)

## 接口地址

**1、外汇、贵金属、加密货币、原油、CFD指数、商品接口地址：**

* 基本路径: /tick-api/batch-kline
* 完整URL: https://api.xdtick.com/tick-api/batch-kline

## 请求示例

**1、外汇、贵金属、加密货币、原油、CFD指数、商品请求示例：**

批量查询产品最新K线功能，由于批量查询参数比较多，放入 body 中，url 参数中只保留 token 字段参数。\
在发送查询请求时，必须包含方法名和 token 信息。一个请求的示例如下：\
https://api.xdtick.com/tick-api/batch-kline

## 注意

<mark style="color:red;">批量查询产品最新K线功能，由于批量查询参数比较多，放入body中，url参数中只保留token字段参数。</mark>

## Body 请求参数示例

```json
[
        {
            "code": "BTCUSD",
            "klineType": "1min,
            "size": 2
        },
        {
            "code": "ETHUSD",
            "klineType": "1min",
            "size": 2
        }
    ]
```

## 请求参数说明

<table data-full-width="false"><thead><tr><th width="189.934326171875">名称</th><th width="91.199951171875">位置</th><th width="95">类型</th><th width="46.7999267578125">必选</th><th>说明</th></tr></thead><tbody><tr><td>X-API-KEY</td><td>Header</td><td>string</td><td>是</td><td>如果不知道你的token，请联系相关人员索要</td></tr><tr><td>body</td><td>body</td><td>object</td><td>否</td><td></td></tr><tr><td>» code</td><td>body</td><td>string</td><td>是</td><td>请查看code列表，选择你要查询的code：<a href="../../jie-ru-liu-cheng/chan-pin-code-lie-biao/">[点击code列表]</a></td></tr><tr><td>» klineype</td><td>body</td><td>integer</td><td>是</td><td>k线类型<br>1min=1分钟,5min=5分钟，15min=15分钟，30min=30分钟，60min=1小时，1d=1天，1w=1周，1m=1月</td></tr><tr><td>» size</td><td>body</td><td>integer</td><td>是</td><td>1、表示查询多少根K线，<mark style="color:red;">该接口最大只能查询2根k线</mark></td></tr></tbody></table>

## 返回示例

```json
{
    "msg": "successful",
    "code": 200,
    "data": {
        "klineList": [
            {
                "code": "BTCUSD",
                "klineData": [
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
                ],
                "klineType": "1min"
            },
            {
                "code": "ETHUSD",
                "klineData": [
                    {
                        "volume": 12.13900000,
                        "high": 2966.75000000,
                        "low": 2966.71000000,
                        "startTime": "2026-01-21T18:46:00",
                        "quoteVolume": 36013.14733500,
                        "changeAmount": -0.03000000,
                        "changeRate": -0.00001011,
                        "close": 2966.71000000,
                        "open": 2966.74000000,
                        "timestamp": 1768992360000
                    },
                    {
                        "volume": 69.32320000,
                        "high": 2967.97000000,
                        "low": 2966.74000000,
                        "startTime": "2026-01-21T18:45:00",
                        "quoteVolume": 205698.66897900,
                        "changeAmount": -1.23000000,
                        "changeRate": -0.00041442,
                        "close": 2966.74000000,
                        "open": 2967.97000000,
                        "timestamp": 1768992300000
                    }
                ],
                "klineType": "1min"
            }
        ]
    }
}
```

## 返回结果说明

<table data-full-width="false"><thead><tr><th>状态码</th><th>状态码含义</th><th>说明</th><th>数据模型</th></tr></thead><tbody><tr><td>200</td><td>OK</td><td>OK</td><td>Inline</td></tr></tbody></table>

<table data-full-width="false"><thead><tr><th width="179.4000244140625">名称</th><th width="115.7999267578125">类型</th><th width="95.4000244140625">必选</th><th>说明</th></tr></thead><tbody><tr><td>» msg</td><td>string</td><td>true</td><td></td></tr><tr><td>» data</td><td>object</td><td>true</td><td></td></tr><tr><td>»» klineList</td><td>[array]</td><td>true</td><td></td></tr><tr><td>»»» code</td><td>string</td><td>true</td><td>产品代码</td></tr><tr><td>»»» klineType</td><td>integer</td><td>true</td><td>k线类型<br>1min=1分钟,5min=5分钟，15min=15分钟，30min=30分钟，60min=1小时，1d=1天，1w=1周，1m=1月</td></tr><tr><td>»»» klineData</td><td>[array]</td><td>true</td><td></td></tr><tr><td>»»»» timestamp</td><td>string</td><td>true</td><td>该K线时间戳</td></tr><tr><td>»»»» open</td><td>string</td><td>true</td><td>该K线开盘价</td></tr><tr><td>»»»» close</td><td>string</td><td>true</td><td>该K线收盘价：<br>1、交易时段内，最新一根K线，该价格也是最新成交价<br>2、休市期间，最新一根K线，该价格是收盘价</td></tr><tr><td>»»»» high</td><td>string</td><td>true</td><td>该K线最高价</td></tr><tr><td>»»»» low</td><td>string</td><td>true</td><td>该K线最低价</td></tr><tr><td>»»»» volume</td><td>string</td><td>true</td><td>该K线成交数量</td></tr><tr><td>»»»» quoteVolume</td><td>string</td><td>true</td><td>该K线成交金额</td></tr><tr><td>»»»» changeAmount</td><td>string</td><td>true</td><td>该K线涨跌额</td></tr><tr><td>»»»» changeRate</td><td>string</td><td>true</td><td>该K线涨跌比例</td></tr></tbody></table>

#### XdTick网站

{% hint style="info" %}
官方网站：[https://xdtick.com/](https://xdtick.com/)
{% endhint %}
