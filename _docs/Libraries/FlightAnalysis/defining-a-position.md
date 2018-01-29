---
title: Defining A Position
category: Boerman.FlightAnalysis
order: 2
---


The core of this library is to process position information from aircraft in order to determine basic information about the flight. The `PositionUpdate` object contains the position information we're talking about here.

A `PositionUpdate` contains the following information:

* Latitude
* Longitude
* Altitude
* Speed
* Heading
* Timestamp

This information is the basis on which both the `FlightContext` and `FlightContextFactory` work to process flight information.

A `PositionUpdate` instance is immutable and can be initialized by using the constructor.

`public PositionUpdate(string aircraft, DateTime timeStamp, double latitude, double longitude, double altitude, double speed, double heading)`

&nbsp;