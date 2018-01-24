---
title: Getting Started
category: Boerman.AprsClient
order: 1
---


Thank you for checking out the docs for the [`Boerman.AprsClient`](https://github.com/Boerman/Boerman.AprsClient) library! This library enables you to rig up a fully working [APRS (Automatic Position Reporting System)](http://www.aprs.org/doc/APRS101.PDF) in a matter of seconds. This library exists of both an APRS message parser and a TCP client.
{: .present-before-paste}

This project has been kickstarted by code found on [aprs.codeplex.com](aprs.codeplex.com). The following changes have been made to this library:
{: .present-before-paste}

* The TCP client which was bundled has been replaced by the [`Boerman.Networking`](https://github.com/Boerman/Boerman.Networking) library to facilitate high throughput with low CPU utilization.
* An object oriented wrapper has been crafted for this library to be usable a bit more like a module.
* Event handlers have been added to be able to plug in more easily on incoming messages.
* Support for [OGN flavoured APRS](http://wiki.glidernet.org/wiki:ogn-flavoured-aprs)&nbsp;has been added.

## Platform Support

The compiled libraries available at NuGet target .NET Standard 2.0. Therefore, this library is cross platform compatible under the .NET framework.
{: .present-before-paste}

[It is possible to use the same package in projects targeting .NET Framework 4.6.1 and onwards.](https://github.com/dotnet/standard/issues/514)
{: .present-before-paste}

## Installation

### NuGet

The *Boerman.AprsClient* library is available through NuGet. To install the library using the NuGet command line:
{: .present-before-paste}

```
Install-Package Boerman.AprsClient
```

### .NET CLI

To install the library through the .NET CLI you can use the following command:
{: .present-before-paste}

```
dotnet add package Boerman.AprsClient
```

### Building From Scratch

You will be able to build the library from scratch by cloning [the git repository](https://github.com/Boerman/Boerman.AprsClient) and restoring the NuGet packages.
{: .present-before-paste}