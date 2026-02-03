# HTTP 请求示例

English / 中文

{% tabs %}
{% tab title="Go" %}
```go
package main

import (
	"fmt"
	"io"
	"log"
	"net/http"
	"net/url"
	"time"
)

func main() {
	httpKlineExample()
}

func httpKlineExample() {
	// 接口地址
	baseURL := "https://api.xdtick.com/tick-api/kline"

	// 构造 query 参数
	params := url.Values{}
	params.Add("code", "BTCUSD")
	params.Add("klineType", "1min")
	params.Add("size", "2")

	// 拼接完整 URL
	requestURL := baseURL + "?" + params.Encode()
	log.Println("请求地址：", requestURL)

	// 创建 HTTP 请求
	req, err := http.NewRequest("GET", requestURL, nil)
	if err != nil {
		log.Println("创建请求失败：", err)
		return
	}

	// 设置请求 Header
	req.Header.Set("X-API-KEY", "YOUR_API_KEY") // 替换为你的商户 key
	req.Header.Set("Content-Type", "application/json")

	// HTTP Client（可设置超时）
	client := &http.Client{
		Timeout: 10 * time.Second,
	}

	// 发送请求
	resp, err := client.Do(req)
	if err != nil {
		log.Println("请求失败：", err)
		return
	}
	defer resp.Body.Close()

	// 读取响应
	body, err := io.ReadAll(resp.Body)
	if err != nil {
		log.Println("读取响应失败：", err)
		return
	}

	// 输出结果
	fmt.Println("HTTP Status:", resp.Status)
	fmt.Println("Response Body:")
	fmt.Println(string(body))
}

```
{% endtab %}

{% tab title="Java" %}
```java
import java.net.URI;
import java.net.URLEncoder;
import java.net.http.HttpClient;
import java.net.http.HttpRequest;
import java.net.http.HttpResponse;
import java.nio.charset.StandardCharsets;
import java.time.Duration;

public class KlineHttpExample {

    public static void main(String[] args) {
        httpKlineExample();
    }

    public static void httpKlineExample() {
        try {
            // 构造 query 参数
            String query = String.format(
                "code=%s&klineType=%s&size=%s",
                URLEncoder.encode("BTCUSD", StandardCharsets.UTF_8),
                URLEncoder.encode("1min", StandardCharsets.UTF_8),
                URLEncoder.encode("2", StandardCharsets.UTF_8)
            );

            // 完整请求地址
            String url = "https://api.xdtick.com/tick-api/kline?" + query;
            System.out.println("请求地址：" + url);

            // 创建 HttpClient
            HttpClient client = HttpClient.newBuilder()
                    .connectTimeout(Duration.ofSeconds(10))
                    .build();

            // 创建 HttpRequest
            HttpRequest request = HttpRequest.newBuilder()
                    .uri(URI.create(url))
                    .timeout(Duration.ofSeconds(10))
                    .header("X-API-KEY", "YOUR_API_KEY") // 替换为你的商户 key
                    .header("Content-Type", "application/json")
                    .GET()
                    .build();

            // 发送请求
            HttpResponse<String> response =
                    client.send(request, HttpResponse.BodyHandlers.ofString());

            // 输出结果
            System.out.println("HTTP Status: " + response.statusCode());
            System.out.println("Response Body:");
            System.out.println(response.body());

        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}

```
{% endtab %}

{% tab title="PHP" %}
```php
<?php

function httpKlineExample() {
    // 接口地址
    $baseUrl = "https://api.xdtick.com/tick-api/kline";

    // Query 参数
    $params = [
        "code"      => "BTCUSD",
        "klineType" => "1min",
        "size"      => 2
    ];

    // 拼接完整 URL
    $url = $baseUrl . "?" . http_build_query($params);
    echo "请求地址：{$url}\n";

    // 初始化 cURL
    $ch = curl_init();

    curl_setopt_array($ch, [
        CURLOPT_URL            => $url,
        CURLOPT_RETURNTRANSFER => true,
        CURLOPT_TIMEOUT        => 10,
        CURLOPT_HTTPHEADER     => [
            "X-API-KEY: YOUR_API_KEY",   // 替换为你的商户 key
            "Content-Type: application/json"
        ]
    ]);

    // 执行请求
    $response = curl_exec($ch);

    if ($response === false) {
        echo "请求失败：" . curl_error($ch) . PHP_EOL;
        curl_close($ch);
        return;
    }

    // HTTP 状态码
    $httpCode = curl_getinfo($ch, CURLINFO_HTTP_CODE);
    curl_close($ch);

    // 输出结果
    echo "HTTP Status: {$httpCode}\n";
    echo "Response Body:\n";
    echo $response . PHP_EOL;
}

// 执行示例
httpKlineExample();

```
{% endtab %}

{% tab title="Python" %}
```python
import requests

def http_kline_example():
    # 接口地址
    url = "https://api.xdtick.com/tick-api/kline"

    # Query 参数
    params = {
        "code": "BTCUSD",
        "klineType": "1min",
        "size": 2
    }

    # Header
    headers = {
        "X-API-KEY": "YOUR_API_KEY",  # 替换为你的商户 key
        "Content-Type": "application/json"
    }

    # 发送 GET 请求
    response = requests.get(
        url,
        params=params,
        headers=headers,
        timeout=10
    )

    # 输出结果
    print("HTTP Status:", response.status_code)
    print("Response Body:")
    print(response.text)


if __name__ == "__main__":
    http_kline_example()

```
{% endtab %}
{% endtabs %}

***

#### XdTick网站

{% hint style="info" %}
官方网站：[https://www.xdtick.cc/](https://www.xdtick.cc/)
{% endhint %}
