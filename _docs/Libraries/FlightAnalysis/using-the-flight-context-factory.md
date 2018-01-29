---
title: Using the Flight Context Factory
category: Boerman.FlightAnalysis
order: 4
---


The `FlightContextFactory` object is a factory wrapper around the `FlightContext` object. This specific wrapper will make your life easier when you have to process position information from multiple different aircraft at the same time.

## Basic Example

To create a basic `FlightContextFactory` instance you can immediately use for flight processing:

    FlightContextFactory factory = new FlightContextFactory();


## How It Helps You

Why would you want to use the `FlightContextFactory` over the `FlightContext` object?

The `FlightContextFactory` object will instantiate a new `FlightContext` object for you each time information from a new aircraft is being detected.&nbsp;*In order for this to work it is required that you use the `aircraftId` field on the `PositionUpdate` object to identify different aircraft!*&nbsp;The `FlightContextFactory` will also clean up old information from aircraft which have been gone for a while in order to prevent high memory usage. Besides this the object subscribes to all events on each individual `FlightContext` instance and propagates them through the events available on the `FlightContextFactory` object so you will have a single endpoint to retrieve information for all different aircraft you're tracking.

## Available Events

These events are available on the `FlightContextFactory` object:

* `OnTakeoff`; when the aircraft being tracked has taken off.
* `OnLanding`; when the aircraft being tracked has landed.
* `OnRadarContact`; will fire when a previously unseen aircraft has been detected.
* `CompletedWithErrors`; will fire when an aircraft was flying but a landing could not be detected within a reasonable timeframe.
* `OnContextDispose`; please note this is the only event available on the `FlightContextFactory` object which is not available on the `FlightContext`! This event will fire when a `FlightContext` has been disposed due to inactivity.

As the source from these events can be from an arbitrary `FlightContext` instance under the hood all relevant flight (and aircraft) information will be available through the event args objects available on the events.

## Real-Time Monitoring

In order to keep track of multiple aircraft at the same time you can pass position information to the `FlightContextFactory` as soon as you receive it! Again, the same principles as used with the `FlightContext` are also being used here.

The `FlightContextFactory` will automatically handle position information based on the aircraft id associated with the position update.

    FlightContextFactory factory = new FlightContextFactory();
    
    // It's completely up to you where you get this data from!
    PositionUpdate positionUpdate = new PositionUpdate(.....);
    
    factory.Enqueue(positionUpdate);

As soon as something interesting happens you will be informed by an event!

## Batch Processing Data

In order to process a collection of data you can just pass a collection of position updates to the `FlightContextFactory`. It will take care of ordering the position updates by aircraft for you!

    FlightContextFactory factory = new FlightContextFactory();
    
    List<PositionUpdate> positionUpdates = new List<PositionUpdate>();
    // I don't really care where you got this information from... Just fill the list!
    
    factory.Enqueue(positionUpdates);
    
Again, when something exciting happens an event will keep you informed!