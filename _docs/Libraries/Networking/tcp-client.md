---
title: TCP Client
category: Boerman.Networking
order: 4
---


The `TCPClient` class features a TCP client implementation. This implementation, just like the server implementation, has been kept as simple as possible to facilitate your own use cases.

The design of the TCP client is almost the same as the design of the TCP server. The same [design philosophies](/Libraries/Networking/design-philosophy/) have been applied here.

## Simple Client

The easiest way to run a TCP client is as follows:

```
var client = new Boerman.Networking.TcpClient();
await client.Open(new IPEndPoint(IPAddress.Parse("127.0.0.1"), 2626));
```

It doesn't do anything useful, yet.

### Instantiating the Client

To instantiate a client you can use the parameterless constructor. There is an optional constructor parameter you can use to configure the encoding. If you are good with the default encoding (UTF-8) or you do not use string functions in this library you are good to go with the parameterless constructor.

### Opening A Connection

To open a connection to a server you use the `Open()` method. The open method requires an argument which specifies the endpoint to connect to. Both `IPEndPoint` or `DnsEndPoint` classes may be used to specify the endpoint to connect to.

Please note that the `Open()` method is asynchronous. This way the function will return only after the connection has been opened or not. This function will return a boolean value indicating whether the connection could be made or not. If the client is already connected this method will return `true`.

### Subscribing To Events

The event subscription system for the TCP client is the same as it is being used in the TCP server. You can subscribe to the following events:

* **Connected**&nbsp;– The client just connected with the server.
* **Received**&nbsp;– The client just received data from the server.
* **Disconnected**&nbsp;– The client just (got) disconnected from the server.

An example of an event subscription is given below:

```
client.Connected += (sender, e) => {
    Console.WriteLine($"{e.TimeStamp}: {e.Endpoint} connected");
};
```

The `sender` object used in these events is the instance of the TCP client which dispatched the event. `e` contains the event arguments for the event which will at least contain the endpoint with which the client was connected.

### Reading Received Data

The process to read received data is exactly the same as it is with the TCP server. The `ReceivedEventArgs` passed with the event contains both the endpoint from which this data was sent and the data which was sent. You can retrieve both the byte and string representations by using the `Bytes` and / or `Data` properties on this event args object. When retrieving the string representation please note that the encoding will be used which is configured during client instantiation or the default (UTF-8).

### Sending Data

There are two methods available for sending data:

```
public async Task Send(byte[] data)
public async Task Send(string message)
```

The boolean values returned by this method indicate whether the data has successfully been sent. The send method with the string argument will use the encoding provided during instantiation to retrieve the byte values. If no encoding has been specified the default UTF-8 will be used. In case an exception has been raised which may be because the connection is not open the method will return `false`.

### Closing the Connection

To close the connection you can use the `Close()` method. This function will gracefully close the connection. The `Disconnected` event will still be fired when using this function.