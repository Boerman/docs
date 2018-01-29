---
title: Using the Flight Context
category: Boerman.FlightAnalysis
order: 3
---


The `FlightContext` object can be seen as a bag containing position information from a single aircraft. The `FlightContext` is being used as a tool which transforms position updates into usable flight metadata.

All input information is processed as soon as possible. It is possible to process information which is gathered after the flight is finished or it can be used to process real-time data as well.

## Basic Usage

To get started using the `FlightContext`:

```
FlightContext flightContext = new FlightContext();
```

## Available Events

Due to the asynchronous nature of the information we're handling in most situations it is required to subscribe to events in order to retrieve relevant information. The following events are available to subscribe to:

* `OnTakeoff` when the aircraft being tracked has taken off.
* `OnLanding` when the aircraft being tracked has landed.
* `OnRadarContact` will fire when a previously unseen aircraft has been detected.
* `CompletedWithErrors` will fire when an aircraft was flying but a landing could not be detected within a reasonable timeframe.

Flight information is passed on with the event args for all these events.

## Real-time Information Processing

In order to be able to process information real time you have to make sure that each bit of information (each individual position update) is being sent to the `FlightContext` instance as soon as possible.

```
FlightContext flightContext = new FlightContext();

// Asume this position update is retrieved from a realtime source:
PositionUpdate positionUpdate = new PositionUpdate(....);

flightContext.Enqueue(positionUpdate);
```

If something interested just happened you will be notified through an event as soon as possible!

## Batch Processing Information

Batch processing information is as easy as making a collection of position updates and passing these to the `FlightContext` instance. Batch processing and real-time processing use the same logic underwater. There are no performance trade offs when choosing one method over another. A combination of these two would also be possible when, for example loading previous data from a database and complementing this information with the latest received position updates.

Processing a list of position updates is as easy as processing a single point:

```
FlightContext flightContext = new FlightContext();

List<PositionUpdate> positionUpdates = new List<PositionUpdate>();
// Assuming you fill the list with interesting information here...
flightContext.Enqueue(positionUpdates);
```

Like the realtime variant, you will be notified of interesting things happening as soon as the position updates have been processed.

## More Advanced Use-Cases

For more advanced use-cases where it is required to handle position updates from multiple different aircraft it is possible to use the `FlightContextFactory`.