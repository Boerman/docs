---
title: Design Philosophy
category: Boerman.Networking
order: 2
---


While designing the TCP server we thought it would be important to deliver powerful tooling in an easy to use package. As there is a wide variety of use cases for TCP servers we aimed to design one which is as generic as it gets. No funky stuff. No timeout settings, no client capping, no authentication, nothing, just the bare TCP logic ready to use in your application.

There are several methods available for starting the server, stopping the server and sending data.

In case you want to be notified when a client has connected, disconnected or has sent you something you can subscribe to a set events.

Methods which do not have an immediate return