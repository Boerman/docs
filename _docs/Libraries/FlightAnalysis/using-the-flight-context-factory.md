---
title: Using the Flight Context Factory
category: Boerman.FlightAnalysis
order: 4
---


The `FlightContextFactory` object is a factory wrapper around the `FlightContext` object. This specific wrapper will make your life easier when you have to process position information from multiple different aircraft at the same time.

## Basic Example

To get started using the `FlightContextFactory`:

// Insert basic example

## How It Helps You

The `FlightContextFactory` object will instantiate a new `FlightContext` object for you each time information from a new aircraft is being detected.&nbsp;*In order for this to work it is required that you use the `aircraftId` field on the `PositionUpdate` object to identify different aircraft!*&nbsp;The `FlightContextFactory` will also clean up old information from aircraft which have been gone for a while in order to prevent high memory usage. Besides this the object subscribes to all events on each individual `FlightContext` instance and propagates them through the events available on the `FlightContextFactory` object so you will have a single endpoint to retrieve information for all different aircraft you're tracking.

## Available Events

These events are available on the `FlightContextFactory` object:

* `OnTakeoff`; when the aircraft being tracked has taken off.
* `OnLanding`; when the aircraft being tracked has landed.
* `OnRadarContact`; will fire when a previously unseen aircraft has been detected.
* `CompletedWithErrors`; will fire when an aircraft was flying but a landing could not be detected within a reasonable timeframe.
* `OnContextDispose`; please note this is the only event available on the `FlightContextFactory` object which is not available on the `FlightContext`! This event will fire when a `FlightContext` has been disposed due to inactivity.

As the source from these events can be from an arbitrary `FlightContext` instance under the hood all relevant flight (and aircraft) information will be available through the event args objects available on the events.