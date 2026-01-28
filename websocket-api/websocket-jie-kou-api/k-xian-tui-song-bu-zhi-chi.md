# K线推送(不支持)

English / 中文

{% hint style="danger" %}
Xdtick 的 WebSocket 接口不支持 K 线数据的推送。无论是历史 K 线还是实时 K 线，目前仅支持通过 HTTP 接口直接获取。
{% endhint %}

因为许多客户对此有疑问，特此说明。推荐的实现方式如下（仅供参考）：

{% stepper %}
{% step %}
### 定时拉取 K 线

为了实现 K 线的快速更新，建议购买高请求频率的套餐，以提高拉取频率。
{% endstep %}

{% step %}
### 结合使用 HTTP 接口

建议将 `/kline` 和 `/batch-kline` 两个接口结合使用，具体步骤：

* 通过 `/kline` 接口轮询请求历史数据并存储到本地数据库。后续的历史数据可直接从客户的数据库获取，无需再次通过接口请求。
* 持续使用 `/batch-kline` 接口批量请求多个产品的最新两根 K 线，并将数据更新到数据库。

这种方式能够快速更新最新的 K 线，同时避免频繁请求历史 K 线导致请求频率受到限制。
{% endstep %}
{% endstepper %}

{% hint style="info" %}
官方网站：[https://xdtick.com/](https://xdtick.com/)
{% endhint %}
