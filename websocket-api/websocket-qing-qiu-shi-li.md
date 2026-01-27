# Websocket 请求示例

[English ](https://en.apis.alltick.co/websocket-api/websocket-request-example)/ 中文

{% content-ref url="/broken/pages/bf76d89cbc39544ecf10171e95af5854b465ea95" %}
[Broken link](/broken/pages/bf76d89cbc39544ecf10171e95af5854b465ea95)
{% endcontent-ref %}

{% tabs %}
{% tab title="Go" %}
{% code title="websocket_example.go" %}
```go
package main

import (
	"encoding/json"
	"github.com/google/uuid"
	"github.com/gorilla/websocket"
	"log"
	"time"
)

type Symbol struct {
	Code       string `json:"code"`
	DepthLevel int    `json:"depth_level"`
}

type Data struct {
	SymbolList []Symbol `json:"symbol_list"`
}

type Request struct {
	CmdID  int    `json:"cmd_id"`
	SeqID  int    `json:"seq_id"`
	Trace  string `json:"trace"`
	Data   Data   `json:"data"`
}

/*
	Special Note:
	GitHub: https://github.com/alltick/realtime-forex-crypto-stock-tick-finance-websocket-api
	Token Application: https://alltick.co
	Replace "testtoken" in the URL below with your own token
	API addresses for forex, cryptocurrencies, and precious metals:
	wss://quote.alltick.co/quote-b-ws-api
	Stock API address:
	wss://quote.alltick.co/quote-stock-b-ws-api
*/
const (
	url = "wss://quote.alltick.co/quote-b-ws-api?token=testtoken"
)

func websocket_example() {

	log.Println("Connecting to server at", url)

	c, _, err := websocket.DefaultDialer.Dial(url, nil)
	if err != nil {
		log.Fatal("dial:", err)
	}
	defer c.Close()

	// Send heartbeat every 10 seconds
	go func() {
		for range time.NewTicker(10 * time.Second).C {
			req := Request{
				CmdID: 22000,
				SeqID: 123,
				Trace: "3380a7a-3e1f-c3a5-5ee3-9e5be0ec8c241692805462",
				Data:  Data{},
			}
			messageBytes, err := json.Marshal(req)
			if err != nil {
				log.Println("json.Marshal error:", err)
				return
			}
			log.Println("req data:", string(messageBytes))

			err = c.WriteMessage(websocket.TextMessage, messageBytes)
			if err != nil {
				log.Println("write:", err)
			}
		}
	}()

	req := Request{
		CmdID: 22002,
		SeqID: 123,
		Trace: uuid.New().String(),
		Data: Data{SymbolList: []Symbol{
			{"GOLD", 5},
			{"AAPL.US", 5},
			{"700.HK", 5},
			{"USDJPY", 5},
		}},
	}
	messageBytes, err := json.Marshal(req)
	if err != nil {
		log.Println("json.Marshal error:", err)
		return
	}
	log.Println("req data:", string(messageBytes))

	err = c.WriteMessage(websocket.TextMessage, messageBytes)
	if err != nil {
		log.Println("write:", err)
	}

	req.CmdID = 22004
	messageBytes, err = json.Marshal(req)
	if err != nil {
		log.Println("json.Marshal error:", err)
		return
	}
	log.Println("req data:", string(messageBytes))

	err = c.WriteMessage(websocket.TextMessage, messageBytes)
	if err != nil {
		log.Println("write:", err)
	}

	rece_count := 0
	for {
		_, message, err := c.ReadMessage()

		if err != nil {
			log.Println("read:", err)
			break
		} else {
			log.Println("Received message:", string(message))
		}

		rece_count++
		if rece_count%10000 == 0 {
			log.Println("count:", rece_count, " Received message:", string(message))
		}
	}

}
```
{% endcode %}
{% endtab %}

{% tab title="Java" %}
{% code title="WebSocketJavaExample.java" %}
```java
import java.io.IOException;
import java.net.URI;
import java.net.URISyntaxException;
import javax.websocket.*;

// Special Note:
// GitHub: https://github.com/alltick/realtime-forex-crypto-stock-tick-finance-websocket-api
// Token Application: https://alltick.co
// Replace "testtoken" in the URL below with your own token
// API addresses for forex, cryptocurrencies, and precious metals:
// wss://quote.alltick.co/quote-b-ws-api
// Stock API address:
// wss://quote.alltick.co/quote-stock-b-ws-api

@ClientEndpoint
public class WebSocketJavaExample {

    private Session session;

    @OnOpen
    public void onOpen(Session session) {
        System.out.println("Connected to server");
        this.session = session;
    }

    @OnMessage
    public void onMessage(String message) {
        System.out.println("Received message: " + message);
    }

    @OnClose
    public void onClose(Session session, CloseReason closeReason) {
        System.out.println("Disconnected from server");
    }

    @OnError
    public void onError(Throwable throwable) {
        System.err.println("Error: " + throwable.getMessage());
    }

    public void sendMessage(String message) throws Exception {
        this.session.getBasicRemote().sendText(message);
    }

    public static void main(String[] args) throws Exception, URISyntaxException, DeploymentException, IOException, IllegalArgumentException, SecurityException, NoSuchMethodException, IllegalAccessException, InvocationTargetException, InstantiationException {
        // Special Note:
        // GitHub: https://github.com/alltick/realtime-forex-crypto-stock-tick-finance-websocket-api
        // Token Application: https://alltick.co
        // Replace "testtoken" in the URL below with your own token
        // API addresses for forex, cryptocurrencies, and precious metals:
        // wss://quote.alltick.co/quote-b-ws-api
        // Stock API address:
        // wss://quote.alltick.co/quote-stock-b-ws-api

        WebSocketContainer container = ContainerProvider.getWebSocketContainer();
        URI uri = new URI("wss://quote.alltick.co/quote-stock-b-ws-api?token=testtoken"); // Replace with your websocket endpoint URL

        WebSocketJavaExample client = new WebSocketJavaExample();

        container.connectToServer(client, uri);

        // Send messages to the server using the sendMessage() method
        // If you want to run for a long time, in addition to sending subscriptions, you also need to modify the code to send heartbeats regularly to prevent disconnection. Refer to the interface documentation for details
        client.sendMessage("{\"cmd_id\": 22002, \"seq_id\": 123,\"trace\":\"3baaa938-f92c-4a74-a228-fd49d5e2f8bc-1678419657806\",\"data\":{\"symbol_list\":[{\"code\": \"700.HK\",\"depth_level\": 5},{\"code\": \"UNH.US\",\"depth_level\": 5}]}}");

        // Wait for the client to be disconnected from the server (or until the user presses Enter)
        System.in.read(); // Wait for user input before closing the program
    }
}
```
{% endcode %}
{% endtab %}

{% tab title="PHP" %}
{% code title="ws_client.php" %}
```php
<?php
require_once __DIR__ . '/vendor/autoload.php';

use Workerman\Protocols\Ws;
use Workerman\Worker;
use Workerman\Connection\AsyncTcpConnection;

// Special Note:
// GitHub: https://github.com/alltick/realtime-forex-crypto-stock-tick-finance-websocket-api
// Token Application: https://alltick.co
// Replace "testtoken" in the URL below with your own token
// API addresses for forex, cryptocurrencies, and precious metals:
// wss://quote.alltick.co/quote-b-ws-api
// Stock API address:
// wss://quote.alltick.co/quote-stock-b-ws-api

$worker = new Worker();
// When the process starts
$worker->onWorkerStart = function()
{
    // Connect to remote websocket server using the websocket protocol
    $ws_connection = new AsyncTcpConnection("ws://quote.alltick.co/quote-stock-b-ws-api?token=testtoken", [
        'ssl' => [
            'verify_peer' => false,
            'verify_peer_name' => false,
        ]
    ]);
    $ws_connection->transport = 'ssl';
    // Send a websocket heartbeat opcode (0x9) to the server every 55 seconds
    $ws_connection->websocketPingInterval = 10;
    $ws_connection->websocketType = Ws::BINARY_TYPE_BLOB; // BINARY_TYPE_BLOB for text, BINARY_TYPE_ARRAYBUFFER for binary
    // After the TCP handshake is completed
    $ws_connection->onConnect = function($connection){
        echo "TCP connected\n";
        // Send subscription request
        $connection->send('{"cmd_id":22002,"seq_id":123,"trace":"3baaa938-f92c-4a74-a228-fd49d5e2f8bc-1678419657806","data":{"symbol_list":[{"code":"700.HK","depth_level":5},{"code":"AAPL.US","depth_level":5}]}}');
    };
    // After the websocket handshake is completed
    $ws_connection->onWebSocketConnect = function(AsyncTcpConnection $con, $response) {
        echo $response;
    };
    // When a message is received from the remote websocket server
    $ws_connection->onMessage = function($connection, $data){
        echo "Received: $data\n";
    };
    // When an error occurs, usually due to failure to connect to the remote websocket server
    $ws_connection->onError = function($connection, $code, $msg){
        echo "Error: $msg\n";
    };
    // When the connection to the remote websocket server is closed
    $ws_connection->onClose = function($connection){
        echo "Connection closed and trying to reconnect\n";
        // If the connection is closed, reconnect after 1 second
        $connection->reConnect(1);
    };
    // After setting up all the callbacks above, initiate the connection
    $ws_connection->connect();
};
Worker::runAll();
?>
```
{% endcode %}
{% endtab %}

{% tab title="Pyton" %}
{% code title="feed.py" %}
```python
import json
import websocket    # pip install websocket-client

'''

# Special Note:

# GitHub: https://github.com/alltick/realtime-forex-crypto-stock-tick-finance-websocket-api

# Token Application: https://alltick.co

# Replace "testtoken" in the URL below with your own token

# API addresses for forex, cryptocurrencies, and precious metals:

# wss://quote.alltick.co/quote-b-ws-api

# Stock API address:

# wss://quote.alltick.co/quote-stock-b-ws-api
'''

class Feed(object):

    def __init__(self):
        self.url = 'wss://quote.alltick.co/quote-stock-b-ws-api?token=testtoken'  # Enter your websocket URL here
        self.ws = None

    def on_open(self, ws):
        """
        Callback object which is called at opening websocket.
        1 argument:
        @ ws: the WebSocketApp object
        """
        print('A new WebSocketApp is opened!')

        # Start subscribing (an example)
        sub_param = {
            "cmd_id": 22002,
            "seq_id": 123,
            "trace":"3baaa938-f92c-4a74-a228-fd49d5e2f8bc-1678419657806",
            "data":{
                "symbol_list":[
                    {
                        "code": "700.HK",
                        "depth_level": 5,
                    },
                    {
                        "code": "UNH.US",
                        "depth_level": 5,
                    }
                ]
            }
        }

        # If you want to run for a long time, you need to modify the code to send heartbeats periodically to avoid disconnection, please refer to the API documentation for details
        sub_str = json.dumps(sub_param)
        ws.send(sub_str)
        print("depth quote are subscribed!")

    def on_data(self, ws, string, type, continue_flag):
        """
        4 arguments.
        The 1st argument is this class object.
        The 2nd argument is utf-8 string which we get from the server.
        The 3rd argument is data type. ABNF.OPCODE_TEXT or ABNF.OPCODE_BINARY will be came.
        The 4th argument is continue flag. If 0, the data continue
        """

    def on_message(self, ws, message):
        """
        Callback object which is called when received data.
        2 arguments:
        @ ws: the WebSocketApp object
        @ message: utf-8 data received from the server
        """
        # Parse the received message
        result = eval(message)
        print(result)

    def on_error(self, ws, error):
        """
        Callback object which is called when got an error.
        2 arguments:
        @ ws: the WebSocketApp object
        @ error: exception object
        """
        print(error)

    def on_close(self, ws, close_status_code, close_msg):
        """
        Callback object which is called when the connection is closed.
        2 arguments:
        @ ws: the WebSocketApp object
        @ close_status_code
        @ close_msg
        """
        print('The connection is closed!')

    def start(self):
        self.ws = websocket.WebSocketApp(
            self.url,
            on_open=self.on_open,
            on_message=self.on_message,
            on_data=self.on_data,
            on_error=self.on_error,
            on_close=self.on_close,
        )
        self.ws.run_forever()


if __name__ == "__main__":
    feed = Feed()
    feed.start()
```
{% endcode %}
{% endtab %}
{% endtabs %}

***

#### AllTick网站

{% hint style="info" %}
官方网站：[https://alltick.co/](https://alltick.co/)
{% endhint %}
