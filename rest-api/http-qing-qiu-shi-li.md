# HTTP 请求示例

[English ](https://en.apis.alltick.co/rest-api/http-request-example)/ 中文

{% tabs %}
{% tab title="Go" %}
```go
package main

import (
	"fmt"
	"io/ioutil"
	"log"
	"net/http"
)

func http_example() {

	/*
		将如下JSON进行url的encode，复制到http的查询字符串的query字段里
		{"trace" : "go_http_test1","data" : {"code" : "700.HK","kline_type" : 1,"kline_timestamp_end" : 0,"query_kline_num" : 2,"adjust_type": 0}}

		特别注意：
		github: https://github.com/alltick/realtime-forex-crypto-stock-tick-finance-websocket-api
		token申请：https://alltick.co
		把下面url中的testtoken替换为您自己的token
		外汇，加密货币（数字币），贵金属的api址：
		https://quote.alltick.co/quote-b-api
		股票api地址:
		https://quote.alltick.co/quote-stock-b-api
	*/
	url := "https://quote.alltick.co/quote-stock-b-api/kline"
	log.Println("请求内容：", url)

	req, err := http.NewRequest("GET", url, nil)
	if err != nil {
		fmt.Println("Error creating request:", err)
		return
	}

	q := req.URL.Query()
	token := "testtoken"
	q.Add("token", token)
	queryStr := `{"trace":"1111111111111111111111111","data":{"code":"AAPL.US","kline_type":1,"kline_timestamp_end":0,"query_kline_num":10,"adjust_type":0}}`
	q.Add("query", queryStr)
	req.URL.RawQuery = q.Encode()
	// 发送请求
	resp, err := http.DefaultClient.Do(req)
	if err != nil {
		fmt.Println("Error sending request:", err)
		return
	}
	defer resp.Body.Close()

	body2, err := ioutil.ReadAll(resp.Body)

	if err != nil {

		log.Println("读取响应失败：", err)

		return

	}

	log.Println("响应内容：", string(body2))

}
```
{% endtab %}

{% tab title="Java" %}
```java
import java.io.BufferedReader;
import java.io.InputStreamReader;
import java.net.HttpURLConnection;
import java.net.URL;

public class HttpJavaExample {

    public static void main(String[] args) {

        try {

            /*
            Encode the following JSON into URL format and copy it to the query field of the HTTP request
            {"trace" : "java_http_test1","data" : {"code" : "700.HK","kline_type" : 1,"kline_timestamp_end" : 0,"query_kline_num" : 2,"adjust_type": 0}}
            Special Note:
            GitHub: https://github.com/alltick/realtime-forex-crypto-stock-tick-finance-websocket-api
            Token Application: https://alltick.co
            Replace "testtoken" in the URL below with your own token
            API addresses for forex, cryptocurrencies, and precious metals:
            https://quote.alltick.co/quote-b-api
            Stock API address:
            https://quote.alltick.co/quote-stock-b-api
            */
            String url = "http://quote.alltick.co/quote-stock-b-api/kline?token=testtoken&query=%7B%22trace%22%20%3A%20%22java_http_test1%22%2C%22data%22%20%3A%20%7B%22code%22%20%3A%20%22700.HK%22%2C%22kline_type%22%20%3A%201%2C%22kline_timestamp_end%22%20%3A%200%2C%22query_kline_num%22%20%3A%202%2C%22adjust_type%22%3A%200%7D%7D";

            URL obj = new URL(url);

            HttpURLConnection con = (HttpURLConnection) obj.openConnection();

            con.setRequestMethod("GET");

            int responseCode = con.getResponseCode();

            System.out.println("Response Code: " + responseCode);

            BufferedReader in = new BufferedReader(new InputStreamReader(con.getInputStream()));

            String inputLine;

            StringBuffer response = new StringBuffer();

            while ((inputLine = in.readLine()) != null) {
                response.append(inputLine);
            }

            in.close();

            System.out.println(response.toString());

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

// Special Note:
// GitHub: https://github.com/alltick/realtime-forex-crypto-stock-tick-finance-websocket-api
// Token Application: https://alltick.co
// Replace "testtoken" in the URL below with your own token
// API addresses for forex, cryptocurrencies, and precious metals:
// https://quote.alltick.co/quote-b-ws-api
// Stock API address:
// https://quote.alltick.co/quote-stock-b-ws-api

$params = '{"trace":"1111111111111111111111111","data":{"code":"AAPL.US","kline_type":1,"kline_timestamp_end":0,"query_kline_num":10,"adjust_type":0}}';

$url = 'https://quote.alltick.co/quote-stock-b-api/kline?token=testtoken';
$method = 'GET';

$opts = array(CURLOPT_TIMEOUT => 10, CURLOPT_RETURNTRANSFER => 1, CURLOPT_SSL_VERIFYPEER => false, CURLOPT_SSL_VERIFYHOST => false);

/* Set specific parameters based on request type */
switch (strtoupper($method)) {
    case 'GET':
        $opts[CURLOPT_URL] = $url.'&query='.rawurlencode($params);
        $opts[CURLOPT_CUSTOMREQUEST] = 'GET';
        break;
    default:
}

/* Initialize and execute curl request */
$ch = curl_init();
curl_setopt_array($ch, $opts);
$data = curl_exec($ch);
$error = curl_error($ch);
curl_close($ch);

if ($error) {
    $data = null;
}

echo $data;
?>
```
{% endtab %}

{% tab title="Pyton" %}
```python
import time
import requests
import json

# Extra headers
test_headers = {
    'Content-Type': 'application/json'
}

'''

# Special Note:

# GitHub: https://github.com/alltick/realtime-forex-crypto-stock-tick-finance-websocket-api

# Token Application: https://alltick.co

# Replace "testtoken" in the URL below with your own token

# API addresses for forex, cryptocurrencies, and precious metals:

# https://quote.alltick.co/quote-b-ws-api

# Stock API address:

# https://quote.alltick.co/quote-stock-b-ws-api
Encode the following JSON and copy it to the "query" field of the HTTP query string
{"trace": "python_http_test1", "data": {"code": "700.HK", "kline_type": 1, "kline_timestamp_end": 0, "query_kline_num": 2, "adjust_type": 0}}
{"trace": "python_http_test2", "data": {"symbol_list": [{"code": "700.HK"}, {"code": "UNH.US"}]}}
{"trace": "python_http_test3", "data": {"symbol_list": [{"code": "700.HK"}, {"code": "UNH.US"}]}}
'''
test_url1 = 'https://quote.alltick.co/quote-stock-b-api/kline?token=testtoken&query=%7B%22trace%22%20%3A%20%22python_http_test1%22%2C%22data%22%20%3A%20%7B%22code%22%20%3A%20%22700.HK%22%2C%22kline_type%22%20%3A%201%2C%22kline_timestamp_end%22%20%3A%200%2C%22query_kline_num%22%20%3A%202%2C%22adjust_type%22%3A%200%7D%7D'
test_url2 = 'https://quote.alltick.co/quote-stock-b-api/depth-tick?token=testtoken&query=%7B%22trace%22%20%3A%20%22python_http_test2%22%2C%22data%22%20%3A%20%7B%22symbol_list%22%3A%20%5B%7B%22code%22%3A%20%22700.HK%22%7D%2C%7B%22code%22%3A%20%22UNH.US%22%7D%5D%7D%7D'
test_url3 = 'https://quote.alltick.co/quote-stock-b-api/trade-tick?token=testtoken&query=%7B%22trace%22%20%3A%20%22python_http_test3%22%2C%22data%22%20%3A%20%7B%22symbol_list%22%3A%20%5B%7B%22code%22%3A%20%22700.HK%22%7D%2C%7B%22code%22%3A%20%22UNH.US%22%7D%5D%7D%7D'

resp1 = requests.get(url=test_url1, headers=test_headers)
time.sleep(1)
resp2 = requests.get(url=test_url2, headers=test_headers)
time.sleep(1)
resp3 = requests.get(url=test_url3, headers=test_headers)

# Decoded text returned by the request
text1 = resp1.text
print(text1)

text2 = resp2.text
print(text2)

text3 = resp3.text
print(text3)
```
{% endtab %}
{% endtabs %}

***

#### AllTick网站

{% hint style="info" %}
官方网站：[https://alltick.co/](https://alltick.co/)
{% endhint %}
