---
title: WebSockets Cheatsheet
date: 2023-01-27 +0000
categories: [Python, JavaScript, Documentation, WebSockets]
tags: [Python, JavaScript, Documentation, Automation, Backend, Full-Duplex, TCP, WebSockets]

---

WebSockets protocol allows for full-duplex communication between a client and a server over a single, long-lasting TCP connection. It is particularly useful in scenarios where real-time, bidirectional communication is needed, such as chat applications, live feeds, and interactive games. Unlike HTTP, WebSockets keep the connection open, enabling both parties to send data independently at any time.

## Python Implementation

### Installation

```bash
pip install websockets
```

### WebSocket Server

```python
import asyncio
import websockets

IP = 'localhost'
PORT = 8765

async def handle_connection(websocket, path):
    async for message in websocket:
        await websocket.send(message)
        print(f'Received: {message}')

start_server = websockets.serve(handle_connection, IP, PORT)

asyncio.get_event_loop().run_until_complete(start_server)
asyncio.get_event_loop().run_forever()
```

### WebSocket Client

```python
import asyncio
import websockets

IP = 'localhost'
PORT = 8765

async def communicate():
    async with websockets.connect(f'ws://{IP}:{PORT}') as websocket:
        name = input("Enter your name: ")
        await websocket.send(name)
        response = await websocket.recv()
        print(f"Server says: {response}")

asyncio.get_event_loop().run_until_complete(communicate())
```

## Node.js Implementation

### Installation

```bash
npm install ws
```

### WebSocket Server

```javascript
const WebSocket = require('ws');

const server = new WebSocket.Server({ port: 8765 });

server.on('connection', (socket) => {
    socket.on('message', (message) => {
        console.log(`Received message: ${message}`);
        socket.send(`Hello, ${message}`);
    });

    socket.send('Welcome to the WebSocket server!');
});
```

### WebSocket Client

```javascript
const WebSocket = require('ws');

const socket = new WebSocket('ws://localhost:8765');

socket.addEventListener('open', () => {
    socket.send('Hello Server!');
});

socket.addEventListener('message', (event) => {
    console.log('Message from server:', event.data);
});
```

## Tips and Best Practices

- **SSL/TLS Usage**: For secure communication, use `wss://` (WebSocket Secure) instead of `ws://`. This is crucial for production environments.
- **Handling Connections**: Ensure robust error handling and reconnection logic in both client and server code.
- **Scaling**: Consider using WebSocket libraries that support clustering and load balancing for handling multiple connections efficiently.
- **Proxy Configuration**: When deploying behind a proxy like nginx, configure the proxy to correctly forward WebSocket traffic to your server.
- **Heartbeats**: Implement heartbeats (regular pings) to keep the connection alive, especially if you're dealing with network components that may close idle connections.

## Additional Resources

- [MDN WebSockets API](https://developer.mozilla.org/en-US/docs/Web/API/WebSockets_API)
- [WebSocket-Node](https://github.com/theturtle32/WebSocket-Node) for Node.js
- [websockets](https://websockets.readthedocs.io/en/stable/) library for Python
