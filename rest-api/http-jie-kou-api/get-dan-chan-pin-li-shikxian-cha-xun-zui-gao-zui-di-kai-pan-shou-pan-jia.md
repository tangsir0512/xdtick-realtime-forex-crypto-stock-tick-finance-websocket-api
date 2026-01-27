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

1、请务必阅读：[HTTP接口限制说明](https://apis.alltick.co/integration-process/interface-restriction-description/http-interface-restrictions)

2、请务必阅读：[错误码说明](https://apis.alltick.co/integration-process/interface-restriction-description/error-code-description)

## 接口地址

**1、美股、港股、A股、大盘数据接口地址：**

* 基本路径: /quote-stock-b-api/kline
* 完整URL: [https://quote.alltick.co/quote-stock-b-api/kline](https://quote.alltick.co/quote-stock-b-api/kline)

**2、外汇、贵金属、加密货币、原油、CFD指数、商品接口地址：**

* 基本路径: /quote-b-api/kline
* 完整URL: [https://quote.alltick.co/quote-b-api/kline](https://quote.alltick.co/quote-b-api/kline)

## 请求示例

**1、美股、港股、A股、大盘数据请求示例：**

在发送查询请求时，必须包含方法名和token信息。一个请求的示例如下：\
https://quote.alltick.co/quote-stock-b-api/kline?token=您的token\&query=queryData

**2、外汇、贵金属、加密货币、原油、CFD指数、商品请求示例：**

在发送查询请求时，必须包含方法名和token信息。一个请求的示例如下：\
https://quote.alltick.co/quote-b-api/kline?token=您的token\&query=queryData

## 请求参数

| 名称    | 位置    | 类型     | 必选 | 说明            |
| ----- | ----- | ------ | -- | ------------- |
| token | query | string | 否  |               |
| query | query | string | 否  | 查看query请求参数说明 |

## query 请求参数 示例

```
{
  "trace": "3baaa938-f92c-4a74-a228-fd49d5e2f8bc-1678419657806",
  "data": {
    "code": "857.HK",
    "kline_type": 1,
    "kline_timestamp_end": 0,
    "query_kline_num": 2,
    "adjust_type": 0
  }
}
```

参数说明：

<table data-full-width="false"><thead><tr><th width="211.7999267578125">名称</th><th width="112">类型</th><th width="83.199951171875">必选</th><th>说明</th></tr></thead><tbody><tr><td>trace</td><td>string</td><td>是</td><td>追踪码，用来查询日志使用，请保证每次请求时唯一</td></tr><tr><td>data</td><td>object</td><td>是</td><td></td></tr><tr><td>» code</td><td>string</td><td>是</td><td>请查看code列表，选择你要查询的code：<a href="https://docs.google.com/spreadsheets/d/1avkeR1heZSj6gXIkDeBt8X3nv4EzJetw4yFuKjSDYtA/edit?gid=495387863#gid=495387863">[点击code列表]</a></td></tr><tr><td>» kline_type</td><td>integer</td><td>是</td><td>k线类型 1、1是1分钟K，2是5分钟K，3是15分钟K，4是30分钟K，5是小时K，6是2小时K(股票不支持2小时)，7是4小时K(股票不支持4小时)，8是日K，9是周K，10是月K （注：股票不支持2小时K、4小时K） 2、最短的k线只支持1分钟 3、查询<mark style="color:red;">昨日收盘价</mark>，kline_type 传8</td></tr><tr><td>» kline_timestamp_end</td><td>integer</td><td>是</td><td>从指定时间往前查询K线 1、传0表示从当前最新的交易日往前查k线 2、指定时间请传时间戳，传时间戳表示从该时间戳往前查k线 3、只有外汇贵金属加密货币支持传时间戳，股票类的code不支持</td></tr><tr><td>» query_kline_num</td><td>integer</td><td>是</td><td>1、表示查询多少根K线，每次最大请求500根，可根据时间戳循环往前请求 2、通过该字段可查询<mark style="color:red;">昨日收盘价</mark>，kline_type 传8，query_kline_num传2，返回2根k线数据中，时间戳较小的数据是昨日收盘价</td></tr><tr><td>» adjust_type</td><td>integer</td><td>是</td><td>复权类型,对于股票类的code才有效，例如：0:除权,1:前复权，目前仅支持0</td></tr></tbody></table>

## 返回示例

```
{
  "ret": 200,
  "msg": "ok",
  "trace": "3baaa938-f92c-4a74-a228-fd49d5e2f8bc-1678419657806",
  "data": {
    "code": "857.HK",
    "kline_type": 1,
    "kline_list": [
      {
        "timestamp": "1677829200",
        "open_price": "136.421",
        "close_price": "136.412",
        "high_price": "136.422",
        "low_price": "136.407",
        "volume": "0",
        "turnover": "0"
      },
      {
        "timestamp": "1677829260",
        "open_price": "136.412",
        "close_price": "136.401",
        "high_price": "136.415",
        "low_price": "136.397",
        "volume": "0",
        "turnover": "0"
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

<table data-full-width="false"><thead><tr><th width="137">名称</th><th width="186">类型</th><th width="105.5999755859375">必选</th><th>说明</th></tr></thead><tbody><tr><td>» ret</td><td>integer</td><td>true</td><td></td></tr><tr><td>» msg</td><td>string</td><td>true</td><td></td></tr><tr><td>» trace</td><td>string</td><td>true</td><td></td></tr><tr><td>» data</td><td>object</td><td>true</td><td></td></tr><tr><td>»» code</td><td>string</td><td>true</td><td>代码</td></tr><tr><td>»» kline_type</td><td>integer</td><td>true</td><td>k线类型 1、1是1分钟K，2是5分钟K，3是15分钟K，4是30分钟K，5是小时K，6是2小时K(股票不支持2小时)，7是4小时K(股票不支持4小时)，8是日K，9是周K，10是月K （注：股票不支持2小时K、4小时K） 2、最短的k线只支持1分钟</td></tr><tr><td>»» kline_list</td><td>[object]</td><td>true</td><td></td></tr><tr><td>»»» timestamp</td><td>string</td><td>true</td><td>该K线时间戳</td></tr><tr><td>»»» open_price</td><td>string</td><td>true</td><td>该K线开盘价</td></tr><tr><td>»»» close_price</td><td>string</td><td>true</td><td>该K线收盘价： 1、交易时段内，最新一根K线，该价格也是最新成交价 2、休市期间，最新一根K线，该价格是收盘价</td></tr><tr><td>»»» high_price</td><td>string</td><td>true</td><td>该K线最高价</td></tr><tr><td>»»» low_price</td><td>string</td><td>true</td><td>该K线最低价</td></tr><tr><td>»»» volume</td><td>string</td><td>true</td><td>该K线成交数量</td></tr><tr><td>»»» turnover</td><td>string</td><td>true</td><td>该K线成交金额</td></tr></tbody></table>

#### AllTick网站

{% hint style="info" %}
官方网站：[https://alltick.co/](https://alltick.co/)
{% endhint %}
