---
title: TCP Server
category: Boerman.Networking
order: 3
---


The `TCPServer` class features a full blown TCP server implementation. The implementation has been kept as simple as possible it is possible to extend the TCP server class to facilitate in your own use cases (for example implementing a HTTP server).

## Simple Server

The easiest way to run a TCP server is as follows:

```
var server = new Boerman.Networking.TcpServer(
    new IPEndPoint(IPAddress.Parse("127.0.0.1"), 2626));
server.Start();
```

This doesn't do anything useful yet other than running a TCP server.

### Instantiating The Server

To instantiate a TCP server you should at least provide the endpoint you want to bind the server to, which is an IP address and port number. Please be careful to check that the endpoint isn't in use yet as you would be unable to bind and start the TCP server otherwise.

Optionally you can provide the encoding you wish to use with the TCP server. If no encoding is provided while instantiating the TCP server the default encoding (UTF-8) is being used. The encoding is only used to display the string representation of the bytes received. If you only access the byte representation of the data during sending and receiving you do not have to worry about the encoding. The two constructor signatures you can use for instantiating a new TCP server are as follows.

```
public TcpServer(IPEndPoint endpoint);
public TcpServer(IPEndPoint endpoint, Encoding encoding);
```

### Startin the Server

The `Start()` method starts the server and starts waiting for incoming connections. This method is not async and will immediately return with a boolean value indicating whether the server could be started on the specified endpoint.

### Subscribing To Events

Events are being used to notify you about interesting things happening. You can subscribe to any of the following events:

* **Connected**&nbsp;– A client just connected with the server.
* **DataReceived**&nbsp;– You just received some data from a connected client.
* **Disconnected**&nbsp;– A previously connected client just disconnected.

An example on subscribing to the `Connected` event is given below.

```
server.Connected += (sender, e) => {
    Console.WriteLine($"{e.TimeStamp}: {e.Endpoint} connected");
};
```

The `sender` object in all events is the instance of the TCP server which fired the event, in case you are about to get creative. The `e` object contains the `EventArgs` object for the specific event. This object will at least contain the endpoint of the client from which the event originated.

> The `EndPoint` property in the event args can / should be used to uniquely identify a client.

### Reading Received Data

As it should be pretty obvious to everyone the `DataReceived` event can be used to retrieve data sent to the server from client. The `DataReceivedEventArgs` passed with this event contains both the EndPoint of the sending client and the data. You can retrieve both the byte representation and the string representation with respectively the `Bytes` and `Data` properties. In case you retrieve the string value the EventArgs class will retrieve the string using the encoding used while instantiating the server instance or the default encoding which is UTF-8.

### Sending Data

There are four different methods available to send data. You can either send data to a specific endpoint or you can send data to all connected endpoints. With both options you can send either a byte array or a string value.

The function signatures you can use are as follows:

```
public async Task<bool> Send(EndPoint endpoint, byte[] data)
public async Task<bool> Send(EndPoint endpoint, string message)
public async Task Send(byte[] data)
public async Task Send(string message)
```

The boolean returned when sending data to a single endpoint indicates whether the data was sent successfully. Another detail is that these methods are using the asynchronous programming model as we do not know how long it will take to send a specific set of data.

> These methods are proven to work with large amounts of data. There's are no problems found when sending files of several megabytes.

In case an exception has been thrown because, for example, the TCP server is not listening or there is no client connected on the specified endpoint, the send method will return `false`.

### Stopping the Server

The `Stop()` method is not async either. It will immediately stop accepting new connections and will (most of the times) gracefully close the open connections. Please note that the `Disconnected` event will still fire for all connected clients.

## FAQ

**Q: What's faster, sending / receiving strings or bytes?**

**A:**&nbsp;Under the water everything is being sent or received as bits 'n bytes. So sending as bytes saves a conversion step. But because you'll work with strings most of the times we have also implemented send and receive functions for strings.