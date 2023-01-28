---
title: Websockets
date: 2023-01-27 +0000
categories: [python, js, documentation, websockets]
tags: [python, js, documentation, automation, backend]
---

A websocket is a computer communications protocol, providing full-duplex communication channels over a single TCP connection. WebSockets provide a persistent connection between a client and a server that both parties can use to start sending data at any time. This is in contrast to HTTP, where the client opens a connection, sends a request, and then waits for the server to send a response before closing the connection.

## Python

```bash
pip3 install websockets
```

### Server

```python
import asyncio
import websockets

IP = 'localhost'
PORT = 8765

async def echo(websocket, path):
    async for message in websocket:
        await websocket.send(message)
        print(f'received: {message}')

start_server = websockets.serve(echo, IP, PORT)

asyncio.get_event_loop().run_until_complete(start_server)
asyncio.get_event_loop().run_forever()
```

### Client

```python
import asyncio
import websockets

IP = 'localhost'
PORT = 8765

async def hello():
    async with websockets.connect(f'ws://{IP}:{PORT}') as websocket:
        name = input("What's your name? ")

        await websocket.send(name)
        print(f"> {name}")

        greeting = await websocket.recv()
        print(f"< {greeting}")

asyncio.get_event_loop().run_until_complete(hello())
```

The server runs permanently, waiting for a client to connect. The client connects to the server, sends a message, and then waits for a response. The server receives the message, sends it back to the client, and then waits for another message. The client receives the message, prints it, and then exits. The server continues to wait for another client to connect.

## NodeJS

```bash
npm install ws
```

### Server

```javascript
const WebSocket = require('ws');

const wss = new WebSocket.Server({ port: 8765 });

wss.on('connection', (ws) => {
    ws.on('message', (message) => {
        console.log(`Received message => ${message}`);
        ws.send(`Hello, ${message}`);
    });

    ws.send('Welcome to the WebSocket server!');
});

```

### Client

```javascript
const socket = new WebSocket('ws://example.com:8765');

// Connection opened
socket.addEventListener('open', (event) => {
    socket.send('Hello Server!');
});

// Listen for messages
socket.addEventListener('message', (event) => {
    console.log('Message from server ', event.data);
});
```

> If you want to connect over a domain using ssl: `wss://example.com:443` <br>
Without ssl: `ws://example.com:80` <br>
If you use a proxy manager like [nginx](https://nginx.org/en/) use the port `443` for ssl and `80` for non ssl. The direction to the websocket server will be handled from the proxy manager.
{: .prompt-tip }
