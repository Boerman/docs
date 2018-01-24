---
title: Getting Started
category: Boerman.AprsClient
order: 1
---

Thank you for checking out the docs for the `Boerman.AprsClient` library! This library enables you to rig up a fully working APRS (Automatic Position Reporting System) in a matter of seconds. This library exsists of both an APRS message parser and a TCP client.

This project has been kickstarted by code found on [aprs.codeplex.com](aprs.codeplex.com). The following changes have been made to this library:

- The TCP client which was bundled has been replaced by the `Boerman.Networking` library to facilitate high throughput with low CPU utilization.
- An object oriented wrapper has been crafted for this library to be usable a bit more like a module.
- Event handlers have been added to be able to plug in more easily on incoming messages.
- Support for [OGN flavoured APRS] has been added.

## Platform Support
The compiled libraries available at NuGet target .NET Standard 2.0. Therefore, this library is cross platform compatible under the .NET framework.

## Installation

### NuGet
The *Boerman.AprsClient* library is available through NuGet. To install the library using the NuGet command line:

    Install-Package Boerman.AprsClient

### .NET CLI
To install the library through the .NET CLI you can use the following command:

    dotnet add package Boerman.AprsClient

### Building From Scratch

You will be able to build the library from scratch by cloning the git repository and restoring the NuGet packages.