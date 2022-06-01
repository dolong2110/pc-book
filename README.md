# pc-book


# I. Theory

- RPC stands for **R**emote **P**rocedure **C**alls
It is a protocol allows a program to
  - execute a procedure of another program located in other computer.
  - without developer explicitly coding details for remote interaction


### 2. Stubs 
- gRPC needs stubs to communicate between services
- Generate stubs:
  - first need API contract: contains services and payload messages in protocol buffered file
  - Why gRPC uses protocol buffer:
    - human-readable interface definition language (IDL)
    - automatically code generators for many languages
    - represent data in binary format:
      - smaller size
      - faster to transport
      - more efficient to serialize and deserialize than some text-based format like JSON or XML
    - strong typed-API contract between client and server which is super safe
    - conventions for API evolution
      - ensure backward and forward compatibility

### 3. HTTP/2
- gRPC uses HTTP/2 as its transfer protocol
- Great features gRPC inherits from HTTP/2:
  - binary framing:
    - more performance and robust
    - lighter to transport, safer to decode compare to other text-based protocol
    - great combination with protocol buffer
  - Header compression using HPACK:
    - reduce overhead and improve performance
  - multiplexing:
    - client and server can send multi requests and responses in parallel over a single TCP connection.
    - reduce latency and improve network utilization
  - allow server push:
    - one request from client, server can send back multi response -> valuable to reduce the round trip latency between client and server when server knows exactly what resources the client will be needed and send them before they are even requested

### 4. How HTTP/2 vs HTTP/1.1

| | HTTP/2 | HTTP/1 |
|---| --- | ---|
| Transfer Protocol | Binary | Text |
| Headers | Compressed | Plain text |
| Multiplexing | Yes | No |
| Requests per connections | multiple | 1 |
| Server push | Yes | No |

### 5. 4 types of gRPC

1. Unary
- client send 1 single request and server replies 1 single response. Similar to normal HTTP API.

2. Client Streaming
- client send stream of multi messages and expect server send back 1 single response.

3. Server Streaming
- client send 1 request message, server replies with a stream of multi messages

4. Bidirectional Streaming
- server and client keep send and receive multi messages in parallel with arbitrary order -> very complex, but flexible and no blocking -> no sides need to wait for the response before sending the next message.

### 6. gRPC vs REST

| Feature | gRPC | REST |
| ------- | ---- | ---- |
| Protocol | HTTP/2 (Fast) | HTTP/1.1 (slow) |
| Payload | Protobuf (binary, small) | JSON (text, large) |
| API contract | Strict, required to be clearly defined in .proto file | Loose, optional (OpenAPI) |
| Code Generation | Built-in in gRPC with helps of protocol buffer compiler | Third-party tools like open API and swagger |
| Security | TLS/SSL | TLS/SSL |
| Streaming | Bidirectional streaming | Client -> server request only |
| Browser support | Limited (require gRPC web with proxy layer to convert btw HTTP/1 and HTTP/2 | fully supported by all browsers |

### 7. Where gRPC is well suited to?

- Micro-services is where gRPC shines
  - Low latency and high throughput communication.
  - Strong API contract.
- Polyglot environments
  - gRPC provides code generation out of the box for many languages.
- Point-to-Point communication
  - Excellent support for bidirectional streaming.
- Network constrained environments- such as mobile app
  - Lightweight message format