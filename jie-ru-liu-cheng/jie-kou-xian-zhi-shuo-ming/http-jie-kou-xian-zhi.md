# HTTP 接口限制

English / 中文

## HTTP接口限制

### 1. 频率类限制

<table data-full-width="false"><thead><tr><th width="81">计划</th><th width="342.0001220703125">单独请求</th><th width="332">同时请求多个http接口</th></tr></thead><tbody><tr><td>免费</td><td><strong>/kline接口：</strong>每10秒，只能1次请求<br><strong>/batch-kline接口：</strong><mark style="color:red;">每10秒，可1次请求</mark><br><strong>/trade-tick接口：</strong>每10秒，只能请求1次</td><td><p>1、10秒只能请求1个接口</p><p>2、需注意/batch-kline接口需间隔10秒 3、所有接口相加，1分钟最大请求10次(6秒1次) 4、每天总共最大可请求14400次，超过则第二天凌晨恢复使用</p></td></tr><tr><td>基础</td><td><strong>/kline接口：</strong>每1秒，只能1次请求<br><strong>/batch-kline接口：</strong><mark style="color:red;">每3秒，只能1次请求</mark><br><strong>/trade-tick接口：</strong>每1秒，只能1次请求</td><td><p>1、同1秒只能请求1个接口</p><p>2、需注意/batch-kline接口需间隔3秒 3、所有接口相加，1分钟最大请求60次(1秒1次) 4、每天总共最大可请求86400次，超过则第二天凌晨恢复使用</p></td></tr><tr><td>高级</td><td><strong>/kline接口：</strong>每1秒，最大可10次请求<br><strong>/batch-kline接口：</strong><mark style="color:red;">每2秒，只能1次请求</mark><br><strong>/trade-tick接口：</strong>每1秒，最大10次请求</td><td><p>1、所有接口相加，每1秒可请求10次</p><p>2、需注意/batch-kline接口需间隔2秒 3、所有接口相加，1分钟最大请求600次(1秒10次) 4、每天总共最大可请求864000次，超过则第二天凌晨恢复使用</p></td></tr><tr><td>专业</td><td><strong>/kline接口：</strong>每1秒，最大可20次请求<br><strong>/batch-kline接口：</strong><mark style="color:red;">每1秒，只能1次请求</mark><br><strong>/trade-tick接口：</strong>每1秒，最大20次请求</td><td><p>1、所有接口相加，每1秒可请求20次</p><p>2、需注意/batch-kline接口需间隔1秒 3、所有接口相加，1分钟最大请求1200次(1秒20次) 4、每天总共最大可请求1728000次，超过则第二天凌晨恢复使用</p></td></tr></tbody></table>

***

### 2. IP类限制

* HTTP接口只会根据Token限制请求频率，对IP没有限制
* 示例：基础计划规定1秒只能请求1次，如果Token在14:03:01请求了/kline接口1次，并在相同的一分钟内调用了/trade-tick接口1次，后台服务都将正常提供服务。如果Token在14:03:01内对/kline接口发出2次请求，第一次请求将正常得到服务，而第二次请求则会收到错误响应。

***

### 3. K线查询限制

* \*\*/kline接口：\*\*每次查询请求只能针对一个产品代码（code）查询K线数据，每次查询最多返回500根K线数据。如果请求查询超过500根的K线，系统将按500根数据进行查询并返回结果。
* \*\*/batch-kline接口：\*\*每次查询请求可针对多个产品代码（code）查询K线数据，但购买的计划不同，可批量请求的代码（code）数量也不同，每次查询最多返回2根K线数据。如果请求查询超过2根的K线，系统将按2根数据进行查询并返回结果，详见下面表格。

<table><thead><tr><th width="176">计划</th><th>/batch-kline接口，最大可请求代码（code）数量</th></tr></thead><tbody><tr><td>免费</td><td>每1次请求，最大可请求 5组数据，每1组数据=1只产品数量+1种K线类型，例如同时获取BTCUSDT的1分钟k线和5分钟k线，这就是2组数据</td></tr><tr><td>基础</td><td>每1次请求，最大可请求 100组数据，每1组数据=1只产品数量+1种K线类型，例如同时获取BTCUSDT的1分钟k线和5分钟k线，这就是2组数据</td></tr><tr><td>高级</td><td>每1次请求，最大可请求 200组数据，每1组数据=1只产品数量+1种K线类型，例如同时获取BTCUSDT的1分钟k线和5分钟k线，这就是2组数据</td></tr><tr><td>专业</td><td>每1次请求，最大可请求 500组数据，每1组数据=1只产品数量+1种K线类型，例如同时获取BTCUSDT的1分钟k线和5分钟k线，这就是2组数据</td></tr></tbody></table>

***

### 4. 最新成交价查询限制

* \*\*/trade-tick接口：\*\*每次查询请求可针对多个产品代码（code）查询最新成交价格，但购买的计划不同，可批量请求的代码（code）数量也不同，详见下面表格
* 如果查询请求超过购买的计划所规定的代码（code）数量，系统将仅针在规定数量内的最前面的代码进行查询并返回结果。

<table><thead><tr><th width="227">计划</th><th>最大可请求代码（code）数量</th></tr></thead><tbody><tr><td>免费</td><td>每1次请求，最大可请求 5个code</td></tr><tr><td>基础</td><td>由于GET请求url长度限制，每次最大建议请求50个code<br>推荐使用websocket接口，支持批量订阅更多code：<a href="/broken/pages/99764bb8d346df29327f512408a88689904e1d4e">接口</a></td></tr><tr><td>高级</td><td>由于GET请求url长度限制，每次最大建议请求50个code<br>推荐使用websocket接口，支持批量订阅更多code：<a href="/broken/pages/99764bb8d346df29327f512408a88689904e1d4e">接口</a></td></tr><tr><td>专业</td><td>由于GET请求url长度限制，每次最大建议请求50个code<br>推荐使用websocket接口，支持批量订阅更多code：<a href="/broken/pages/99764bb8d346df29327f512408a88689904e1d4e">接口</a></td></tr></tbody></table>

***



#### 注意事项

* 请根据上述限制合理规划您的请求策略，以避免不必要的服务中断。
* 上述限制是为了保证所有用户能够公平地享受服务，同时保护后台系统免受过度负载的影响。
* 如有疑问或需要进一步的帮助，请联系客服支持。

***

XdTick网站

{% hint style="info" %}
官方网站：[https://www.xdtick.cc/](https://www.xdtick.cc/)
{% endhint %}
