---
title:Websockets
date: 2023-01-27 +0000
categories: [python, documentation, websockets]
tags: [python, documentation, automation, backend]
---

A websocket is a computer communications protocol, providing full-duplex communication channels over a single TCP connection. WebSockets provide a persistent connection between a client and a server that both parties can use to start sending data at any time. This is in contrast to HTTP, where the client opens a connection, sends a request, and then waits for the server to send a response before closing the connection.

## Python Websockets

'''bash
pip3 install websockets
'''

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

The server runs permanently, waiting for a client to connect. The client connects to the server, sends a message, and then waits for a response. The server receives the message, sends it back to the client, and then waits for another message. The client receives the message, prints it, and then exits.
