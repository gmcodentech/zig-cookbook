## http.Server - std

A basic implementation of `http.Server` has been introduced since Zig 0.12.0.

For each connection we spawn a new thread to handle it, in `accept` it will:
1. First it use `defer` to ensure the connection is closed when returned.
2. Then init a HTTP server to begin parse request
3. For each request, we first check if it could upgrade to WebSocket.
   - If it succeeds, call `serveWebSocket` else call `serverHTTP`

```zig
{{#include ../src/05-03.zig }}
```

## Test

For HTTP, we could use `curl`:
```bash
curl -v localhost:8080
```
It will output:
```bash
< HTTP/1.1 200 OK
< content-length: 32
< custom header: custom value
<
Hello World from Zig HTTP server
```

For WebSocket, we could use console in your browser's `Developer Tools`:

```js
var webSocket = new WebSocket('ws://localhost:8080');
webSocket.onmessage = function(data) { console.log(data); }
```
Then we could send message like this:
```js
webSocket.send('abc')
```

![](./images/websocket-client.webp)

See [Writing WebSocket client applications - Web APIs | MDN](https://developer.mozilla.org/en-US/docs/Web/API/WebSockets_API/Writing_WebSocket_client_applications) for details.

## Note
The std implementation exhibits extremely poor performance. If you're planning beyond basic experimentation, consider utilizing alternative libraries such as:
- <https://github.com/karlseguin/http.zig>
- <https://github.com/zigzap/zap>
- <https://github.com/mookums/zzz>
