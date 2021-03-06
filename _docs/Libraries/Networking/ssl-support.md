---
title: SSL Support
category: Boerman.Networking
order: 5
---

The `Boerman.Networking` library supports SSL/TLS on both client and server instances. SSL and TLS are protocol which enables end to end encryption of the contents sent between the client and the server over a socket connection. The amazing thing about this technology is that it does not alter the protocol itself, but rather is a wrapper which authenticates the client/server and encrypts and decrypts contents sent over the connection.

A connection encrypted with SSL or TLS will further be referred to as a secure connection.

## Setting up a TCP server with SSL support

If you want a TCP server which only accepts clients with a secure connection you can set up the TCP server just as usual, with the difference you provide a (X509) certificate. Please note that this certificates FQDN (Fully Qualified Domain Name) should match the endpoint on which your clients connect. For localhost this will be `217.0.0.1`, while for this website it might be `docs.boerman.co`. Clients will verify the certificate with the endpoint they're connecting to.

```
var tcpServer = new TcpServer(
    new IPEndPoint(IPAddress.Parse("127.0.0.1"), 2626),
    new X509Certificate2("cert.pfx", "1234"));
```

Besides the instantiation of the TCP server nothing is different from a plain connection.

[For a sample on how to set up a TCP server with SSL encryption, see this folder in the GitHub repo.](https://github.com/Boerman/Boerman.Networking/tree/master/TcpServerWithSSL)

## Setting up a TCP client with SSL support

In order to create a TCP client with SSL support enabled there are two additional properties available to set upon opening the connection. These properties are:

* useSsl
* allowCertificateChainErrors

Opening a connection can be as follows:

```
await tcpClient.Open(new IPEndPoint(IPAddress.Parse("127.0.0.1"), 2626),
    useSsl: true,
    allowCertificateChainErrors: true);
```

**Please note:*** it is **NOT RECOMMENDED** to allow certificate chain errors in production. It's great during development for using self signed certificates but it essentially means no trusted party could verify the validity of the certificate and therefore the integrity of the connection could not be verified.*

[A full working sample for a TCP client connecting with SSL enabled, see this folder in the GitHub repo.](https://github.com/Boerman/Boerman.Networking/tree/master/TcpClientWithSSL)

[For a sample demonstrating how to make a HTTPS request to google, see this file.](https://github.com/Boerman/Boerman.Networking/blob/master/HttpRequestExample/Program.cs)

*Client authentication using certificates in order to verify the client is currently not supported.*