# 心跳

[English ](https://en.apis.alltick.co/websocket-api/stock-websocket-interface-api/ping-pang)/ 中文

## 接口说明

要求请求者每10秒发送一次，在30秒内如果没有收到心跳请求，就会认为超时，断开请求者的 websocket 连接。

## 请求 — 协议号：22000

### 数据结构 (json)

{% code title="请求示例" %}
```json
{
    "cmd_id":22000,
    "seq_id":123,
    "trace":"3baaa938-f92c-4a74-a228-fd49d5e2f8bc-1678419657806",
    "data":{
    }
}
```
{% endcode %}

## 应答 — 协议号：22001

### 数据结构 (json)

{% code title="应答示例" %}
```json
{
    "ret":200,
    "msg":"ok",
    "cmd_id":22001,
    "seq_id":123,
    "trace":"3baaa938-f92c-4a74-a228-fd49d5e2f8bc-1678419657806",
    "data":{
    }
}
```
{% endcode %}

{% hint style="info" %}
官方网站：[https://alltick.co/](https://alltick.co/)
{% endhint %}
