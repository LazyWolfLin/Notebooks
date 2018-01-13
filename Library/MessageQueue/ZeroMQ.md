# `ZeroMQ`

`ZeroMQ`是一个使用`C`语言编写的异步消息队列库，实际上已经被发展成一个网络库。

## `context`

使用`zmq_ctx_new()`创建，使用`zmq_ctx_term()`进行销毁。
`context`是线程安全，可在线程间共享。
调用`zmq_ctx_term()`，一旦存在未销毁的`socket`，`zmq_ctx_term()`会等待所有连接到此`context`的`socket`全部被`zmq_close()`销毁再销毁`context`。如果`socket`已经全部关闭了，如果还有`Message`未发送，`zmq_ctx_term()`仍会陷入阻塞，解决方法是等待`Message`发送或者把`LINGER`值设置为`0`从而使得`Message`变为超时。不必重复调用`zmq_ctx_term()`去销毁`context`，当`socket`全部关闭后，阻塞的`zmq_ctx_term()`会销毁`context`。在多线程程序中，调用`zmq_ctx_term()`后，处于`receives`、`polls`或者`sends`的`socket`会返回而`error`。

## `zmq_msg_t` `Message`

不要直接操作`zmq_msg_t`对象，应始终使用`zmq_msg`系列函数。

`zmq_msg_init()`、`zmq_msg_init_size()`和`zmq_msg_init_data()`是互斥的`Message`初始化函数，不要重复调用`Message`初始化函数初始化同一个`Message`。

使用`zmq_msg_send()`成功发送`Message`后，不一定需要使用`zmq_msg_close()`销毁`Message`。

`ZMQ`使用一个后台IO线程将消息压入消息收发队列。如果仅使用线程间传输，可以将IO线程数设置为0。

多帧消息即一个`Message`由多个`zmq_msg_t`结构组成。`ZMQ`保证`Message`的原子传输，即要么接到整个`Message`，要么一帧都接不到。

## `socket`

由`zmq_socket()`创建，使用`zmq_close()`进行销毁。
`socket`是线程不安全，仅在创建它的线程中使用，除非在内存上完全的从一个线程传递给另一个线程。

你如果要关闭阻塞的`socket`，正确的方式是设置一个较低的LINGER值，然后关闭它。

### `socket`类型

#### `ZMQ_REQ`

客户端使用`ZMQ_REQ`类型的`socket`发送请求并接收服务器端的回复，服务器端可以使用`ZMQ_REP`或`ZMQ_ROUTER`的`socket`处理请求。

`ZMQ_REQ`类型的`socket`仅允许`zmq_send(request)`和`zmq_recv(reply)`循环发送，一旦违背将产生错误代码`-1`。`ZMQ_REQ`类型的`socket`每次发送请求，会在它的服务器列表中循环选择一个可用的服务发送请求。如果没有可用的服务，将停止发送请求，直到有一个可用的服务，并不会丢弃请求。而它每次收到的回复都会与最后一个请求相匹配。

#### `ZMQ_REP`

服务器端使用`ZMQ_REP`类型的`socket`接收客户端的请求并发送回复，客户端可以使用`ZMQ_REQ`和`ZMQ_DEALER`的`socket`处理请求。

`ZMQ_REP`类型的`socket`仅允许`zmq_recv(request)`和`zmq_send(reply)`循环发送，一旦违背将产生错误代码`-1`。每个收到的请求会先进入`fair-queue`中等待处理，每个发送的回复会发到最后一个被处理请求的客户端。如果发送请求的客户端已经不存在，则会丢弃对应的回复。

#### `ZMQ_DEALER`

`ZMQ_DEALER`的`socket`用于扩展请求应答模式，它的对端可以使用`ZMQ_ROUTER`、`ZMQ_REP`和`ZMQ_DEALER`的`socket`。

`ZMQ_DEALER`的`socket`发送消息时会循环选择一个对端，接收到的消息会进入`fair-queue`中等待处理。如果它的所有连接对象都无法接收消息时，`zmq_send()`将会被阻塞，但消息不会被丢弃。

`ZMQ_DEALER`的`socket`与`ZMQ_REP`的`socket`连接时，每条消息需要使用一个空的`zmq_msg_t`结构作为分隔符。

#### `ZMQ_ROUTER`

`ZMQ_ROUTER`的`socket`用于扩展请求应答模式，它的对端可以使用`ZMQ_DEALER`、`ZMQ_REQ`和`ZMQ_ROUTER`的`socket`。

`ZMQ_DEALER`的`socket`接收消息时会在消息前添加对端的标识然后在送入`fair-queue`中，发送消息时会读取并删去消息的对端标识以确定目的地。如果它的消息的目的地不存在，则消息将默认被丢弃，除非`ZMQ_ROUTER_MANDATORY`被设置成1。

#### `ZMQ_PUB`

`ZMQ_PUB`的`socket`用于发布订阅模式的`publisher`端分发数据，它的对端可以使用`ZMQ_SUB`和`ZMQ_XSUB`。

`ZMQ_PUB`的`socket`分发消息时，如果对端不可用，则发送的消息将被丢弃，直到对端恢复。

#### `ZMQ_SUB`

`ZMQ_SUB`的`socket`用于发布订阅模式的subscriber端接收数据，它的对端可以使用`ZMQ_PUB`和`ZMQ_XPUB`。

`ZMQ_SUB`的`socket`需要使用`zmq_setsockopt()`的`ZMQ_SUBSCRIBE`选项订阅所需消息。

#### `ZMQ_XPUB`

与`ZMQ_PUB`类型相同，只是可以从对端接收来自对端的订阅消息。

#### `ZMQ_XSUB`

与`ZMQ_SUB`类型相同，只是可以向对端发送的订阅消息用以订阅。

#### `ZMQ_PUSH`

`ZMQ_PUSH`的`socket`用于管道模式的上级节点向下级节点分发数据，它的对端可以使用`ZMQ_PULL`。

`ZMQ_PUSH`的`socket`有多个下级节点时，会循环选择一个下级节点分发数据。当下级节点不可用时，它将陷入阻塞，等待至少有一个下级节点可用时继续发送数据，并不会丢弃消息。

#### `ZMQ_PULL`

`ZMQ_PULL`的`socket`用于管道模式的下级节点接收上级节点分发的数据，它的对端可以使用`ZMQ_PUSH`。

`ZMQ_PULL`的`socket`有多个上级节点时，将会使用`fair-queue`接收上级节点分发的消息。

#### `ZMQ_PAIR`

`ZMQ_PAIR`的`socket`在任意时刻都只允许连接到另一个`ZMQ_PAIR`的`socket`。通过`ZMQ_PAIR`的`socket`发送的消息不执行路由策略或许信息过滤机制。

`ZMQ_PAIR`的`socket`的对端如果不可用，它将陷入阻塞，直到对端可用再继续发送，消息不会被丢弃。

`ZMQ_PAIR`被设计用于线程间的通信，并不实现自动重连等功能。而且`ZMQ_PAIR`是一个实验性功能，可能存在漏洞。

#### `ZMQ_STREAM`

`ZMQ_STREAM`的`socket`用于与非ZMQ的对端使用TCP进行通信，它既可作为客户端，也可作为服务器端，可以任意的发送和接收异步TCP数据。

Example
``` C
    //  使用ZMQ_STREAM创建的一个HTTP服务端
    void *ctx = zmq_ctx_new();
    assert(ctx);
    /* Create ZMQ_STREAM socket */
    void *socket = zmq_socket(ctx, ZMQ_STREAM);
    assert(socket);
    int rc = zmq_bind(socket, "tcp://*:8080");
    assert(rc == 0);
    /* Data structure to hold the ZMQ_STREAM ID */
    uint8_t id[256];
    size_t id_size = 256;
    while (1){
        /* Get HTTP request; ID frame and then request */
        id_size = zmq_recv(socket, id, 256, 0);
        assert(id_size > 0);
        /* Prepares the response */
        char http_response[] =
        "HTTP/1.0 200 OK\r\n"
        "Content-Type: text/plain\r\n"
        "\r\n"
        "Hello, World!";
        /* Sends the ID frame followed by the response */
        zmq_send(socket, id, id_size, ZMQ_SNDMORE);
        zmq_send(socket, http_response, strlen (http_response), ZMQ_SNDMORE);
        /* Closes the connection by sending the ID frame followed by a zero response */
        zmq_send(socket, id, id_size, ZMQ_SNDMORE);
        zmq_send(socket, 0, 0, ZMQ_SNDMORE);
        /* NOTE: If we don't use ZMQ_SNDMORE, then we won't be able to send more */
        /* message to any client */
    }
    zmq_close(socket);
    zmq_ctx_term(ctx);
```

## `ZeroMQ API`

### `zmq_ctx_new()`

``` C
void *zmq_ctx_new();
```

创建一个新的`context`，返回一个`viod*`型指针，成功则指针指向新建的`context`，失败则指针指向NULL。

### `zmq_ctx_set()`

``` C
int zmq_ctx_set(void *context, int option_name, int option_value);
```

设置`context`的参数，返回一个整数，成功则返回0，失败则返回-1。

|option_name|default value|Description|
|---|---|---|
|`ZMQ_IO_THREADS`|1|设置OI线程数|
|`ZMQ_MAX_SOCKETS`|1024|设置`socket`的最大数量|
|`ZMQ_IPV6`|0|是否启用IPv6，0表示不启用，1表示启用|

### `zmq_ctx_get()`

``` C
int zmq_ctx_get(void *context, int option_name);
```

查询`context`的参数，返回一个整数，成功则返回非负的参数值，失败则返回-1。

|option_name|Description|
|---|---|
|`ZMQ_IO_THREADS`|设置OI线程数|
|`ZMQ_MAX_SOCKETS`|设置`socket`的最大数量|
|`ZMQ_IPV6`|是否启用IPv6，0表示不启用，1表示启用|

### `zmq_ctx_term()`

``` C
int zmq_ctx_term(void *context);
```

销毁一个`context`，返回一个整数，成功则返回0，失败则返回-1。

调用`zmq_ctx_term()`销毁`context`时，在`context`上的所有阻塞操作都将返回一个ETERM错误，此时，除了`zmq_close()`外的所有操作都将失败。`zmq_ctx_term()`中断所有阻塞操作后将等待在`context`上的`socket`被`zmq_close()`关闭以及`socket`上所有`Message`都被发送或者超时。

### `zmq_msg_init()`

``` C
int zmq_msg_init(zmq_msg_t *msg);
```

初始化一个空的`zmq_msg_t`，返回值始终为0。

Example:
``` C
zmq_msg_t msg;
rc = zmq_msg_init (&msg);
assert (rc == 0);
rc = zmq_recv (socket, &msg, 0);
assert (rc == 0);
```

### `zmq_msg_init_size()`

``` C
int zmq_msg_init_size(zmq_msg_t *msg, size_t size);
```

初始化一个指定大小的`zmq_msg_t`，返回一个整数，成功则返回0，失败则返回-1。

`zmq_msg_init_size()`的实现会选择将小消息存储在栈空间，将大消息存储在堆空间。但由于性能的原因，`zmq_msg_init_size()`不会清除消息数据。

### `zmq_msg_init_data()`

``` C
typedef void (zmq_free_fn) (void *data, void *hint);
int zmq_msg_init_data(zmq_msg_t *msg, void *data, size_t size, zmq_free_fn *ffn, void *hint);
```

用一块缓存区初始化一个`zmq_msg_t`，返回一个整数，成功则返回0，失败则返回-1。

`zmq_msg_init_data()`不会对`data`进行拷贝，而会通过引用获得该数据块。一旦`ZMQ`不再需要该数据块，就会调用`zmq_free_fn`以释放该数据块。`zmq_free_fn`需要保证线程安全，因为它将在任意线程中被调用。

Example:
``` C
void my_free(void *data, void *hint)
{
    free(data);
}
void *data = malloc(6);
assert(data);
memcpy(data, "ABCDEF", 6);
zmq_msg_t msg;
rc = zmq_msg_init_data(&msg, data, 6, my_free, NULL);
assert(rc == 0);
```

### `zmq_msg_send()`

``` C
int zmq_msg_send(zmq_msg_t * msg，void * socket，int flags);
```

通过`socket`发送消息包，返回一个整数，成功则返回消息的字节数，失败则返回-1。

|flags|description|
|---|---|
|`ZMQ_DONTWAIT`|指定在非阻塞模式下执行发送，`Message`将不经过`queue`直接发送|
|`ZMQ_SNDMORE`|指定当前发送的消息为多帧消息|

发送多帧消息，除了最后一帧，其他所有帧都需要使用`ZMQ_SNDMORE`参数。

Example:
``` C
//  发送一个简单消息
zmq_msg_t msg;
int rc = zmq_msg_init_size(&msg, 6);
assert(rc == 0);
memset(zmq_msg_data(&msg), 'A', 6);
rc = zmq_msg_send(&msg, socket, 0); assert (rc == 6);
```

``` C
//  发送一个多帧消息
rc = zmq_msg_send(&part1, socket, ZMQ_SNDMORE);
rc = zmq_msg_send(&part2, socket, ZMQ_SNDMORE);
rc = zmq_msg_send(&part3, socket, 0);
```

### `zmq_msg_recv()`

``` C
int zmq_msg_recv(zmq_msg_t * msg，void * socket，int flags);
```

通过`socket`接收消息包，返回一个整数，成功则返回消息的字节数，失败则返回-1。

`zmq_msg_recv()`从`socket`中接收一条`Message`，并存储到`msg`参数中，而`msg`参数中存储的任何内容都将被释放。如果`socket`上没有可用的`zmq_msg_t`，`zmq_msg_recv()`将陷入阻塞直到获得`zmq_msg_t`。

Example:
``` C
//  接收一个简单消息
zmq_msg_t msg;
int rc = zmq_msg_init(&msg);
assert(rc == 0);
rc = zmq_msg_recv(&msg, socket, 0);
assert(rc != -1);
zmq_msg_close(&msg);
```

``` C
//  接收一个多帧消息
int64_t more;
size_t more_size = sizeof (more);
do {
    zmq_msg_t part;
    int rc = zmq_msg_init(&part);
    assert(rc == 0);
    rc = zmq_msg_recv(&part, socket, 0);
    assert(rc != -1);
    rc = zmq_getsockopt(socket, ZMQ_RCVMORE, &more, &more_size);
    assert(rc == 0);
    zmq_msg_close (&part);
}while(more);
```

### `zmq_msg_close()`

``` C
int zmq_msg_close(zmq_msg_t *msg);
```

释放`zmq_msg_t`，返回一个整数，成功则返回0，失败则返回-1。

### `zmq_msg_data()`

``` C
void *zmq_msg_data(zmq_msg_t *msg);
```

获取指向`zmq_msg_t`内的数据块的指针，返回指向消息内容的`(viod*)`型指针。

### `zmq_msg_size()`

``` C
size_t zmq_msg_size (zmq_msg_t *msg);
```

获取`zmq_msg_t`内部数据块的字节大小，返回消息内容的字节大小。

### `zmq_msg_more()`

``` C
int zmq_msg_more (zmq_msg_t *message);
```

检查多帧消息是否还有后续帧，如果无后续帧则返回0，如果有后续帧则返回1。

Example:
``` C
//  接收一个多帧消息
zmq_msg_t part;
while (true) {
    int rc = zmq_msg_init (&part);
    assert (rc == 0);
    rc = zmq_msg_recv (socket, &part, 0);
    assert (rc != -1);
    if (zmq_msg_more (&part))
        fprintf (stderr, "more\n");
    else {
        fprintf (stderr, "end\n");
        break;
    }
    zmq_msg_close (&part);
}
```

### `zmq_msg_set()`

``` C
int zmq_msg_set(zmq_msg_t *message, int property, int value);
```

设置`zmq_msg_t`的参数，返回一个整数，成功则返回0，失败则返回-1。但是目前并不支持任何属性。

### `zmq_msg_get()`

``` C
int zmq_msg_get(zmq_msg_t *message, int property);
```

查询`zmq_msg_t`的参数，返回一个整数，成功则返回属性值，失败则返回-1。

|property|description|
|---|---|
|`ZMQ_MORE`|是否有后续帧|

### `zmq_msg_copy()`

``` C
int zmq_msg_copy(zmq_msg_t *dest, zmq_msg_t *src);
```

复制消息的内容到另一消息中，返回一个整数，成功则返回0，失败则返回-1。

`zmq_msg_copy()`实际上并没有进行拷贝，因此要避免修改消息内容。如果要拷贝出一个新消息，则使用`zmq_msg_init_size()`及`memcpy()`。

### `zmq_msg_move()`

``` C
int zmq_msg_move(zmq_msg_t *dest, zmq_msg_t *src);
```

把`src`的消息内容到`dest`中，返回一个整数，成功则返回0，失败则返回-1。

`zmq_msg_move()`并不做拷贝，只更新`dest`的内容引用，而`src`的内容将变为空，dest的原内容将被释放。

### `zmq_socket()`

``` C
void *zmq_socket(void *context, int type);
```

创建一个`socket`接口，返回一个`void *`类型的句柄，成功则指针指向新建的`socket`，失败则指针指向`NULL`。

### `zmq_close()`

``` C
int zmq_close(void *socket);
```

关闭一个`socket`，返回一个整数，成功返回0，失败返回-1。

`zmq_close()`关闭`socket`时，物理上已从网络中接收，而未被zmq_recv()函数读取的消息将被丢弃。而被zmq_send()发送但尚未完成物理传输的消息是否丢弃取决于ZMQ_LINGER的值。

### `zmq_setsockopt()`

``` C
int zmq_setsockopt(void *socket, int option_name, const void *option_value, size_t option_len);
```

设置`socket`选项值，返回一个整数值，成功则返回0，失败则返回-1。

[`socket`选项](http://api.zeromq.org/4-0:zmq-setsockopt)（待补充）

### `zmq_getsockopt()`

``` C
int zmq_getsockopt(void *socket, int option_name, void *option_value, size_t *option_len);
```

获取`socket`选项值，返回一个整数，成功返回0，失败返回-1。

### `zmq_bind()`

``` C
int zmq_bind (void *socket, const char *endpoint);
```

将`socket`绑定到端口，接收该端口的数据，返回一个整数，成功返回0，失败返回-1。

`ZMQ`提供`TCP`、`IPC`、`INPROC`、`pgm`和`epgm`传输。

### `zmq_connect()`

``` C
int zmq_connect(void *socket, const char *endpoint);
```

使用`socket`创建连接用于发送数据，返回一个整数，成功返回0，失败返回-1。

`ZMQ`提供`TCP`、`IPC`、`INPROC`、`pgm`和`epgm`传输。

### `zmq_send()`

``` C
int zmq_send(void *socket, void *buf, size_t len, int flags);
```

通过`socket`发送数据，返回一个整数，成功则返回消息的字节数，失败则返回-1。

|flags|description|
|---|---|
|`ZMQ_DONTWAIT`|指定在非阻塞模式下执行发送，`Message`将不经过`queue`直接发送|
|`ZMQ_SNDMORE`|指定当前发送的消息为多帧消息|

发送多帧消息，除了最后一帧，其他所有帧都需要使用`ZMQ_SNDMORE`参数。

### `zmq_send_const()`

``` C
int zmq_send_const(void *socket, void *buf, size_t len, int flags);
```

通过`socket`发送常量数据，返回一个整数，成功则返回消息的字节数，失败则返回-1。

|flags|description|
|---|---|
|`ZMQ_DONTWAIT`|指定在非阻塞模式下执行发送，`Message`将不经过`queue`直接发送|
|`ZMQ_SNDMORE`|指定当前发送的消息为多帧消息|

发送多帧消息，除了最后一帧，其他所有帧都需要使用`ZMQ_SNDMORE`参数。

### `zmq_recv()`

``` C
int zmq_recv(void *socket, void *buf, size_t len, int flags);
```

通过`socket`接收数据，返回一个整数，成功则返回消息的字节数，失败则返回-1。

`zmq_recv()`从`socket`中接收数据，并存储到`buf`参数中，而超过`len`参数指定长度的数据都将被丢弃。如果`socket`上没有可用的数据，`zmq_recv()`将陷入阻塞直到获得数据。


### `zmq_socket_monitor()`

``` C
int zmq_socket_monitor (void *socket, char * *addr, int events);
```

注册回调函数用于监视`socket`，返回一个整数，成功则返回消息的字节数，失败则返回-1。

可供监视的[事件](http://api.zeromq.org/4-0:zmq-socket-monitor)（待补充）

### `zmq_poll()`

``` C
int zmq_poll(zmq_pollitem_t *items, int nitems, long timeout);
```

轮询


### Deprecated API

``` C
void *zmq_init(int io_threads);//初始化一个zmq context
int zmq_term(void *context);//销毁一个zmq context
int zmq_ctx_destroy(void *context);//销毁一个zmq context
int zmq_sendmsg(void *socket, zmq_msg_t *msg, int flags);//通过socket发送消息包。
int zmq_recvmsg(void *socket, zmq_msg_t *msg, int flags);//通过socket接收消息包。
```


## 消息传递模式

`Message`在两个类型可能相同可能不同的`socket`间传递。

### 请求-应答模式

请求应答模式用于客户端与服务器端之间，客户端发送请求到服务器端，服务器端处理每一个请求。请求应答模式要求服务器端遵循接收-发送循环，客户端遵循发送-接收循环，一旦违背将产生错误代码`-1`。（`ZeroMQ`是靠着这个去保证消息不丢失的么？）[请求应答模式协议](http://rfc.zeromq.org/spec:28)


### 发布-订阅模式

发布订阅模式用于从一个`publisher`到多个`subscriber`的一对多的数据分发模式。

发布订阅模式需要使用`zmq_setsockopt()`设置订阅，如果不设置，则将无法收到任一信息。SUB端可以设置多次订阅，PUB端的信息只要满足SUB端的任意一次订阅，便能在SUB端收到信息。

发布订阅模式存在慢连接现象，即`subscriber`端建立连接需要一定的时间从而导致丢失`publisher`端发送的消息。

如果使用`TCP`协议，`subscriber`端接收消息过慢，则消息会堆积在`publisher`端。

`ZeroMQ v3.x`将消息过滤放在`publisher`端，而旧的`ZeroMQ v2.x`则将消息过滤放在`subscriber`端。

[发布订阅模式协议](http://rfc.zeromq.org/spec:29)

### 管道模式

管道模式用于把数据分配到中间的节点。数据总是沿着管道流动，管道的每一级有一个或多个节点，当有多个节点时，数据从上一级节点循环分发到下一级节点中。

在这一模型中，中间的`worker`可以动态增减数量，`sock`则绑定在两端`ventilator`和`sink`上。

`PUSH_PULL`模式同样存在慢连接问题，先连接的`worker`会先收到`work`从而做更多的工作。（这个问题感觉可以直接忽略？当工作时间很长，刚开始的非分布式工作对于整个工作的效率并不会造成影响？）

[管道模式协议](http://rfc.zeromq.org/spec:30)

### 独占模式

独占模式用于端对端的连接，用于线程间通信。

[独占模式协议](http://rfc.zeromq.org/spec:31)

### 原始模式

原始模式用于与使用`TCP`协议的对端通信，允许任意方向的异步请求和回复。

## 可用传输协议

### `TCP`

### `pgm`

### `ipc`

在`Windows`系统下仍不可使用。

### `inproc`

## 连接模式

### `PUB`-`SUB`

### `REQ`-`REP`

### `REQ`-`ROUTER`

### `DEALER`-`REP`

### `DEALER`-`ROUTER`

### `DEALER`-`DEALER`

### `ROUTER`-`ROUTER`

### `PUSH`-`PULL`

### `PAIR`-`PAIR`