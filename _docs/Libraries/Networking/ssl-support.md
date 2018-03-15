---
title: SSL Support
category:
order: 1
---

The `Boerman.Networking` library supports SSL/TLS on both client and server instances. SSL and TLS are protocol which enables end to end encryption of the contents sent between the client and the server over a socket connection. The amazing thing about this technology is that it does not alter the protocol itself, but rather is a wrapper which authenticates the client/server and encrypts and decrypts contents sent over the connection.

A connection encrypted with SSL or TLS will further be referred to as a secure connection.

## Setting up a TCP server with SSL support

If you want a TCP server which only accepts clients with a secure connection you can set up the TCP server just as usual, with the difference you provide a (X509) certificate. Please note that this certificates FQDN (Fully Qualified Domain Name) should match the endpoint on which your clients connect. For localhost this will be `217.0.0.1`, while for this website it might be `docs.boerman.co`.

[For a sample on how to set up a TCP server with SSL encryption, see this folder in the GitHub Repo.](https://github.com/Boerman/Boerman.Networking/tree/master/TcpServerWithSSL)

&nbsp;

&nbsp;

## &nbsp;

## &nbsp;

## Setting up a TCP client with SSL support

## Future plans

Please note that