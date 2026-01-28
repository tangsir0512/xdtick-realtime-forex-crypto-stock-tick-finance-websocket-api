# HTTP 通用标准头

[English ](https://en.apis.alltick.co/integration-process/universal-standard-header-description/http-common-standard-headers)/ 中文

## 请求通用标准头介绍

| 字段        | 名称      | 位置     | 类型     | 必填项 | 说明            |
| --------- | ------- | ------ | ------ | --- | ------------- |
| X-API-KEY | 用户token | Header | string | 是   | 用户token       |
| query     | 数据体     | query  | object | 是   | 具体数据格式见各个接口定义 |

query示例：

{% code title="请求示例.json" %}
```json
{
    "code": "BTCUSD",
    "klineType": "1min",
    "size": 100
}
```
{% endcode %}

## 应答通用标准头介绍

| 字段   | 名称  | 类型     | 说明            |
| ---- | --- | ------ | ------------- |
| msg  | 消息  | string | 对成功或者失败具体的描述  |
| code | 状态  | int    | 接口请求状态        |
| data | 数据体 | object | 具体数据格式见各个接口定义 |

示例：

{% code title="响应示例.json" %}
```json
{
    "code":200,
    "msg":"successful",
    "data":{
    }    
}
```
{% endcode %}

***

{% hint style="info" %}
官方网站：[https://xdtick.com/](https://xdtick.com/)
{% endhint %}
