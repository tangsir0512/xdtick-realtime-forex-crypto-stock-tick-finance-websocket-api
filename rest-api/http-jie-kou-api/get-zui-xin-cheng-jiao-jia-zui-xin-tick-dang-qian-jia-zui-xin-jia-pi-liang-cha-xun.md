# GET 最新成交价(最新tick、当前价、最新价)批量查询

[English ](https://en.apis.alltick.co/rest-api/stock-http-interface-api/get-latest-transaction-price-query)/ 中文

## GET /trade-tick

## 接口说明

该接口支持批量请求产品的最新成交价(最新逐笔Tick数据、也是当前价、最新价)，不支持请求历史成交价(历史逐笔tick数据)。

## 请求频率

<table data-full-width="false"><thead><tr><th width="89.79998779296875">计划</th><th width="198.4000244140625">单独请求</th><th width="472">同时请求多个http接口</th></tr></thead><tbody><tr><td>免费</td><td>1、每10秒，只能1次请求<br>2、每次最大可批量查询5个产品</td><td><p>1、10秒只能请求1个接口</p><p><mark style="color:red;">2、多个接口请求时，需注意/batch-kline接口需间隔10秒</mark><br>3、所有接口相加，1分钟最大请求10次(6秒1次)<br>4、每天总共最大可请求14400次，超过则第二天凌晨恢复使用</p></td></tr><tr><td>基础</td><td>1、每1秒，只能1次请求<br>2、由于GET请求url长度限制，每次最大建议请求50个code</td><td><p>1、同1秒只能请求1个接口</p><p><mark style="color:red;">2、多个接口请求时，需注意/batch-kline接口需间隔3秒</mark><br>3、所有接口相加，1分钟最大请求60次(1秒1次)<br>4、每天总共最大可请求86400次，超过则第二天凌晨恢复使用</p></td></tr><tr><td>高级</td><td>1、每1秒，最大可10次请求<br>2、由于GET请求url长度限制，每次最大建议请求50个code</td><td><p>1、所以接口相加，每1秒可请求10次</p><p><mark style="color:red;">2、多个接口请求时，需注意/batch-kline接口需间隔2秒</mark><br>3、所有接口相加，1分钟最大请求600次(1秒10次)<br>4、每天总共最大可请求864000次，超过则第二天凌晨恢复使用</p></td></tr><tr><td>专业</td><td>1、每1秒，最大可20次请求<br>2、由于GET请求url长度限制，每次最大建议请求50个code</td><td><p>1、所以接口相加，每1秒可请求20次</p><p><mark style="color:red;">2、多个接口请求时，需注意/batch-kline接口需间隔1秒</mark><br>3、所有接口相加，1分钟最大请求1200次(1秒20次)<br>4、每天总共最大可请求1728000次，超过则第二天凌晨恢复使用</p></td></tr><tr><td>全部港股</td><td>1、每1秒，最大可20次请求<br>2、由于GET请求url长度限制，每次最大建议请求50个code</td><td><p>1、所以接口相加，每1秒可请求20次</p><p><mark style="color:red;">2、多个接口请求时，需注意/batch-kline接口需间隔1秒</mark><br>3、所有接口相加，1分钟最大请求1200次(1秒20次)<br>4、每天总共最大可请求1728000次，超过则第二天凌晨恢复使用</p></td></tr><tr><td>全部A股</td><td>1、每1秒，最大可20次请求<br>2、由于GET请求url长度限制，每次最大建议请求50个code</td><td><p>1、所以接口相加，每1秒可请求20次</p><p><mark style="color:red;">2、多个接口请求时，需注意/batch-kline接口需间隔1秒</mark><br>3、所有接口相加，1分钟最大请求1200次(1秒20次)<br>4、每天总共最大可请求1728000次，超过则第二天凌晨恢复使用</p></td></tr><tr><td>全部美股</td><td>1、每1秒，最大可20次请求<br>2、由于GET请求url长度限制，每次最大建议请求50个code</td><td><p>1、所以接口相加，每1秒可请求20次</p><p><mark style="color:red;">2、多个接口请求时，需注意/batch-kline接口需间隔1秒</mark><br>3、所有接口相加，1分钟最大请求1200次(1秒20次)<br>4、每天总共最大可请求1728000次，超过则第二天凌晨恢复使用</p></td></tr></tbody></table>

## 接口限制

1、请务必阅读：[HTTP接口限制说明](https://apis.alltick.co/integration-process/interface-restriction-description/http-interface-restrictions)

2、请务必阅读：[错误码说明](https://apis.alltick.co/integration-process/interface-restriction-description/error-code-description)

## 接口地址

{% tabs %}
{% tab title="美股、港股、A股、大盘" %}
* 基本路径: /quote-stock-b-api/trade-tick
* 完整URL: [https://quote.alltick.co/quote-stock-b-api/trade-tick](https://quote.alltick.co/quote-stock-b-api/trade-tick)
{% endtab %}

{% tab title="外汇、贵金属、加密货币、原油、CFD指数、商品" %}
* 基本路径: /quote-b-api/trade-tick
* 完整URL: [https://quote.alltick.co/quote-b-api/trade-tick](https://quote.alltick.co/quote-b-api/trade-tick)
{% endtab %}
{% endtabs %}

## 请求示例

{% tabs %}
{% tab title="美股、港股、A股、大盘" %}
在发送查询请求时，必须包含token和query参数。示例：

https://quote.alltick.co/quote-stock-b-api/trade-tick?token=您的token\&query=queryData
{% endtab %}

{% tab title="外汇、贵金属、加密货币、原油、CFD指数、商品" %}
在发送查询请求时，必须包含token和query参数。示例：

https://quote.alltick.co/quote-b-api/trade-tick?token=您的token\&query=queryData
{% endtab %}
{% endtabs %}

## 请求参数

| 名称    | 位置    | 类型     | 必选 | 说明            |
| ----- | ----- | ------ | -- | ------------- |
| token | query | string | 否  |               |
| query | query | string | 否  | 查看query请求参数说明 |

## query请求参数

将如下 JSON 进行 UrlEncode 编码，赋值到 URL 的查询字符串的 query 里：

{% code title="query 示例" %}
```json
{
  "trace": "edd5df80-df7f-4acf-8f67-68fd2f096426",
  "data": {
    "symbol_list": [
      {
        "code": "857.HK"
      },
      {
        "code": "UNH.US"
      }
    ]
  }
}
```
{% endcode %}

参数说明：

| 名称             | 类型        | 必选 | 说明                                                                                                                                                                                                                                              |
| -------------- | --------- | -- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| trace          | string    | 是  |                                                                                                                                                                                                                                                 |
| data           | object    | 是  |                                                                                                                                                                                                                                                 |
| » symbol\_list | \[object] | 是  |                                                                                                                                                                                                                                                 |
| »» code        | string    | 否  | 代码：[https://docs.google.com/spreadsheets/d/1avkeR1heZSj6gXIkDeBt8X3nv4EzJetw4yFuKjSDYtA/edit?gid=495387863#gid=495387863](https://docs.google.com/spreadsheets/d/1avkeR1heZSj6gXIkDeBt8X3nv4EzJetw4yFuKjSDYtA/edit?gid=495387863#gid=495387863) |

## 返回示例

{% code title="返回示例" %}
```json
{
  "ret": 200,
  "msg": "ok",
  "trace": "edd5df80-df7f-4acf-8f67-68fd2f096426",
  "data": {
    "tick_list": [
      {
        "code": "857.HK",
        "seq": "30841439",
        "tick_time": "1677831545217",
        "price": "136.302",
        "volume": "0",
        "turnover": "0",
        "trade_direction": 0
      }
    ]
  }
}
```
{% endcode %}

## 返回结果说明

状态码说明：

| 状态码 | 含义 | 说明 | 数据模型   |
| --- | -- | -- | ------ |
| 200 | OK | OK | Inline |

返回字段说明：

| 名称                  | 类型        | 必选    | 说明                                                                                                                                                                                        |
| ------------------- | --------- | ----- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| ret                 | integer   | true  | 返回code                                                                                                                                                                                    |
| msg                 | string    | true  | 返回code对应消息                                                                                                                                                                                |
| trace               | string    | true  | 请求的trace                                                                                                                                                                                  |
| data                | object    | true  |                                                                                                                                                                                           |
| » tick\_list        | \[object] | true  |                                                                                                                                                                                           |
| »» code             | string    | false | 代码                                                                                                                                                                                        |
| »» seq              | string    | false | 序号                                                                                                                                                                                        |
| »» tick\_time       | string    | false | 时间戳                                                                                                                                                                                       |
| »» price            | string    | false | 成交价                                                                                                                                                                                       |
| »» volume           | string    | false | 成交量                                                                                                                                                                                       |
| »» turnover         | string    | false | <p>成交额：<br>1、外汇、贵金属、能源不返回成交额，可自行根据每次推送的数据计算，计算公式：turnover = price * volume<br>2、股票、加密货币正常返回成交额。</p>                                                                                       |
| »» trade\_direction | integer   | false | <p>交易方向：<br>1、0为默认值，1为Buy，2为SELL<br>2、外汇、贵金属、能源默认只会返回0<br>3、股票、加密货币根据市场情况会返回0、1、2<br>4、详细说明：<br>0:表示中性盘，即以买一价与卖一价之间的价格撮合成交。<br>1:表示主动买入，即以卖一价或者更高价格成交的股票<br>2:表示主动卖出，即以买一价或者更低价格成交的股票</p> |

{% hint style="info" %}
官方网站：[https://alltick.co/](https://alltick.co/)
{% endhint %}
