# 错误码说明

[English ](https://en.apis.alltick.co/integration-process/interface-restriction-description/error-code-description)/ 中文

***

## 200

* 错误内容：ok
* 含义：成功

***

## 400 — request header param invalid

* 错误内容：request header param invalid
* 含义：请求JSON第一层参数错误

排查建议：

{% stepper %}
{% step %}
### 检查 JSON 结构

检查 JSON 结构是否完整。
{% endstep %}

{% step %}
### 必需字段

确认所有必需字段已正确包含。
{% endstep %}

{% step %}
### data 字段类型

验证 data 字段是否为有效的对象类型。
{% endstep %}

{% step %}
### 关键字段

核实 trace 等关键字段是否存在。
{% endstep %}
{% endstepper %}

***

## 400 — request data param invalid

* 错误内容：request data param invalid
* 含义：请求JSON中data字段参数错误

排查建议：

{% stepper %}
{% step %}
### data 是否为对象

检查 data 字段是否为有效对象。
{% endstep %}

{% step %}
### data 中必需字段

确认 data 中所有必需字段已正确填写。
{% endstep %}

{% step %}
### 对照接口文档核实

对照具体接口文档，核实 data 字段内容。
{% endstep %}

{% step %}
### POST 请求体

特别注意 POST 请求中，确保 body 体中 JSON 参数完整且正确。
{% endstep %}
{% endstepper %}

***

## 401

* 错误内容：token invalid
* 含义：token 无效

可能由以下情况导致：

{% stepper %}
{% step %}
### Token 格式

Token 格式不正确。
{% endstep %}

{% step %}
### Token 过期

Token 账号过期。
{% endstep %}
{% endstepper %}

***

## 402

* 错误内容：query invalid
* 含义：请求的 query 参数错误

排查建议：

{% stepper %}
{% step %}
### 检查 GET 请求的 query

检查 GET 请求的 query 参数。
{% endstep %}

{% step %}
### URL 编码

对 query 参数进行 URL 编码。
{% endstep %}

{% step %}
### 参数格式

确保参数格式符合接口要求。
{% endstep %}

{% step %}
### 特殊字符转义

验证特殊字符是否正确转义。
{% endstep %}
{% endstepper %}

***

## 429

* 错误内容：Too Many Requests
* 含义：超过套餐规定的请求频率

建议：

{% stepper %}
{% step %}
### 优化请求频率

优化请求频率和逻辑。
{% endstep %}

{% step %}
### 升级套餐

考虑升级套餐，获取更高的请求频率。
{% endstep %}
{% endstepper %}

点击查看接口限制说明：

* [HTTP接口限制](http-jie-kou-xian-zhi.md)
* [Websocket接口限制](websocket-jie-kou-xian-zhi.md)

***

## 600

* 错误内容：code invalid
* 含义：请求 code 产品无效

排查建议：

{% stepper %}
{% step %}
### 检查请求 URL

仔细核对接口文档，股票类和外汇类贵金属类数据的请求 URL 是不同。
{% endstep %}

{% step %}
### 检查产品 code

对照产品列表，确保代码有效且准确：[产品列表](../chan-pin-code-lie-biao/)
{% endstep %}
{% endstepper %}

***

## 601

* 错误内容：body empty
* 含义：请求消息体数据为空

排查建议：

{% stepper %}
{% step %}
### 检查 POST 消息体

检查 POST 请求的消息体。
{% endstep %}

{% step %}
### 完整 JSON 参数

确保 body 中包含完整的 JSON 参数。
{% endstep %}

{% step %}
### 批量接口注意

特别注意批量获取 /batch-kline 等接口。
{% endstep %}

{% step %}
### 必需字段

验证所有必需字段均已正确填写。
{% endstep %}
{% endstepper %}

***

## 603

* 错误内容：token level not enough
* 含义：请求产品个数或者 K 线根数超过接口文档规定的限制

排查建议：

{% stepper %}
{% step %}
### 检查产品数量（K 线接口）

K 线接口，确认同时请求的【产品数】加上【K 线类型】的总和，是否超过套餐限制。注意批量产品 K 线接口每次仅允许 2 根。
{% endstep %}

{% step %}
### 非 K 线接口

非 K 线接口，确认请求的产品数，是否超过套餐限制。
{% endstep %}

{% step %}
### 验证 K 线根数

核实 K 线根数是否符合接口规定。
{% endstep %}
{% endstepper %}

点击查看接口限制说明：[HTTP接口限制](http-jie-kou-xian-zhi.md)

***

## 604

* 错误内容：code unauthorized
* 含义：您的 token 没有请求该 code 的权限

***

## 605

* 错误内容：too many requests
* 含义：请求频率限制

建议：

{% stepper %}
{% step %}
### 优化请求频率

优化请求频率和逻辑。
{% endstep %}

{% step %}
### 升级套餐

考虑升级套餐，获取更高的请求频率。
{% endstep %}
{% endstepper %}

点击查看接口限制说明：

* [HTTP接口限制](http-jie-kou-xian-zhi.md)
* [Websocket接口限制](websocket-jie-kou-xian-zhi.md)

***

## 606

* 错误内容：too many requests and connection will be closed
* 含义：一般是 Websocket 接口请求频率限制

排查建议：

{% stepper %}
{% step %}
### 检查 Websocket 连接数

确认是否超过套餐规定的最大连接数。
{% endstep %}

{% step %}
### 控制请求频率

确保多个 Websocket 请求时间隔至少 3 秒。
{% endstep %}
{% endstepper %}

点击查看接口限制说明：[Websocket接口限制](websocket-jie-kou-xian-zhi.md)

***

#### XdTick 网站

{% hint style="info" %}
官方网站：[https://xdtick.com/](https://xdtick.com/)
{% endhint %}
