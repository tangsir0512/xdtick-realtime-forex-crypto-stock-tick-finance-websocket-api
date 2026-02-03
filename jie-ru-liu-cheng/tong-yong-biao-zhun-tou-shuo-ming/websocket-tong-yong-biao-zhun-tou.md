# Websocket 通用标准头

English / 中文

## 请求通用标准头介绍

| 字段      | 名称  | 类型     | 必填项         | 说明            |
| ------- | --- | ------ | ----------- | ------------- |
| cmd\_id | 协议号 | uint32 | 详见各个接口定义有提供 |               |
| data    | 数据体 | object | 是           | 具体数据格式见各个接口定义 |

示例：

{% code title="请求示例" %}
```json
{
    "cmd_id":22000,
    "data":{
    }
}
```
{% endcode %}

## 应答通用标准头介绍

| 字段      | 名称  | 类型     | 说明                                                            |
| ------- | --- | ------ | ------------------------------------------------------------- |
| code    | 返回值 | int32  | [错误码说明](../jie-kou-xian-zhi-shuo-ming/cuo-wu-ma-shuo-ming.md) |
| msg     | 消息  | string | 对成功或者失败具体的描述                                                  |
| cmd\_id | 协议号 | uint32 | 详见各个接口定义有提供                                                   |
| data    | 数据体 | object | 具体数据格式见各个接口定义                                                 |

示例：

{% code title="应答示例" %}
```json
{
    "code":200,
    "msg":"successful",
    "cmd_id":0,
    "data":{
    }    
}
```
{% endcode %}

***

#### XdTick网站

{% hint style="info" %}
官方网站：[https://www.xdtick.cc/](https://www.xdtick.cc/)
{% endhint %}
