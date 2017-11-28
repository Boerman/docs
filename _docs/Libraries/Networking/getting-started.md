---
title: Getting Started
category: Boerman.Networking
order: 1
---


Thank you for checking out these docs! The [`Boerman.Networking`](https://github.com/Boerman/Boerman.TcpLib) library provides simple to use networking capabilities on the .NET framework. This library is for you if you do not want to know too much about the underlying protocols yet you want to have a powerful toolchain for quickly building networking enabled applications.

## Features

This library can help you with the following components:

* [TCP server](/Libraries/Networking/tcp-server/)
* [TCP client](/Libraries/Networking/tcp-client/)
* APRS client

These libraries are developed to be as **performant**, **stable** and **reliable** as possible. In practice this means that this library will not require and utilize a single core only to receive data from a connected party.

## Platform Support

At this moment the compiled libraries available at NuGet only target .NET Standard 2.0.

> It should be fairly easy to target .NET 4.7.1 when compiling the source code yourself, but please note mileage may vary and you're on your own.

Due to cross platform considerations we chose only support .NET Standard 2.0 at the moment.

## Installation

### NuGet

The&nbsp;*Boerman.Networking*&nbsp;library is available through NuGet. To install the library using the NuGet command line:

```
Install-Package Boerman.Networking
```

### .NET CLI

To install the library through the .NET CLI you can use the following command:

```
dotnet add package Boerman.Networking
```

### Building From Scratch

As the library doesn't have any fancy dependencies outside the .NET Framework you could clone [the repo](https://github.com/Boerman/Boerman.TcpLib) and you would be good to go.