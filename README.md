# WEEKLY MODULES

WEEK 8
- [Reflection 8](#Reflection-8)

# WEEK 8
## Reflection 8

1. What are the key differences between unary, server streaming, and bi-directional streaming
RPC (Remote Procedure Call) methods, and in what scenarios would each be most suitable?
    - **Unary**: Client sends one request and receive one response (like a function call), such as making a payment.
    - **Server Streaming**: Allows client to send one request and receive many responses, such as transaction history or log streaming.
    - **Bidirectional Streaming**: Both sides send messages independently, such as chatting systems.

2. What are the potential security considerations involved in implementing a gRPC service in
Rust, particularly regarding authentication, authorization, and data encryption?

    - **Authentication**: Using `TLS` to check who’s connecting, or pass tokens (like login tokens) with the request.
    - **Authorization**: Check user roles or permissions before performing actions.
    - **Encryption**: Using `TLS` so all data sent between client and server is safe and private.
    - **Error handling**: Not showing detailed errors to users — they might reveal private or sensitive info.

3. What are the potential challenges or issues that may arise when handling bidirectional
streaming in Rust gRPC, especially in scenarios like chat applications?

    The challenging part is how to handle reads and writes at the same time. If a connection drops or messages come too fast, it can cause bugs or delays. Background tasks is also needed to be managed properly, to avoid any leaks.

4. What are the advantages and disadvantages of using the
`tokio_stream::wrappers::ReceiverStream` for streaming responses in Rust gRPC services?

    `ReceiverStream` is simple and works nicely with async message sending. On the downside, if too many messages come in quickly, it can get overwhelmed. There's also a case where if the other side stops listening, some messages might be lost. It’s fine for light to moderate use, but not great for sending lots of data fast.

5. In what ways could the Rust gRPC code be structured to facilitate code reuse and modularity,
promoting maintainability and extensibility over time?

    - Separate logic into modules (handlers, services, models, etc).
    - Use traits and generics to write reusable logic.
    - Isolate data access, validation, and response formatting.

6. In the MyPaymentService implementation, what additional steps might be necessary to
handle more complex payment processing logic?

    - Add input validation (e.g., negative amount checks).
    - Integrate a database layer for transaction records
    - Perform external API calls to payment processors
    - Include asynchronous jobs for delayed processing
    - Return better responses with status codes and messages.

7. What impact does the adoption of gRPC as a communication protocol have on the overall
architecture and design of distributed systems, particularly in terms of interoperability with
other technologies and platforms?

    `gRPC` changes how services talk to each other. It simplifies communication with streaming and async support. It also uses strict, fast communication and works across languages. On the downside, it’s more complex than `REST` and needs good planning for versioning and testing.

8. What are the advantages and disadvantages of using HTTP/2, the underlying protocol for
gRPC, compared to HTTP/1.1 or HTTP/1.1 with WebSocket for REST APIs?

    - Advantages:
        - **Faster**: Supports multiplexing (multiple requests over one connection).
        - **Smaller size**: Uses binary format, which is faster and more efficient than text.
        - **Built-in streaming**: Great for real-time data with client/server or bidirectional streaming.
        - **Better performance**: Lower latency.

    - Disadvantages:
        - **Harder to debug**: Binary format is not human-readable like `JSON`, hence harder to debug.
        - **Browser support**: Browsers don’t support `gRPC` directly (only `gRPC-Web`).
        - **More complex setup**: Requires `TLS` (HTTPS) and Protocol Buffers.

9.  How does the request-response model of REST APIs contrast with the bidirectional streaming
capabilities of gRPC in terms of real-time communication and responsiveness?

    `REST` only supports one request and one response. `gRPC` allows streaming, so it’s better for real-time apps. With `gRPC`, the server or client can keep sending updates without new requests.

10. What are the implications of the schema-based approach of gRPC, using Protocol Buffers,
compared to the more flexible, schema-less nature of JSON in REST API payloads?

    - `ProtoBuf` is compact, fast, and strongly typed, making it great for internal systems and performance-sensitive apps.

    - `JSON` is human-readable and flexible but can be less strict, which may lead to inconsistent data or versioning problems.