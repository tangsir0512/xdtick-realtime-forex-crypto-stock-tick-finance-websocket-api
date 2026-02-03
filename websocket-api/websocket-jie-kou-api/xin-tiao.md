# 心跳

English / 中文

## 接口说明

要求请求者每10秒发送一次，在30秒内如果没有收到心跳请求，就会认为超时，断开请求者的 websocket 连接。

## 请求 — 协议号：22000

### 数据结构 (json)

{% code title="请求示例" %}
```json
{
    "cmd_id":22000
}
```
{% endcode %}

## 应答 — 协议号：22001

### 数据结构 (json)

{% code title="应答示例" %}
```json
{
    "code":200,
    "msg":"successful"
}
```
{% endcode %}

{% hint style="info" %}
官方网站：[https://www.xdtick.cc/](https://www.xdtick.cc/)
{% endhint %}
