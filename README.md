Belfry.js
========
##### A simple publish subscribe library returning curried functions to work with cumin

## Installation

1. dependencies + cumin
2. bower install
3. tag inclusion

## Usage

Belfry provides a singlton instance from the method `getTower`.

```js
var tower = Belfry.getTower();
```

Instance methods are `publish`, `subscribe` and `unsubscribe`.

```js
// create a function to subscribe to topics
var logger = function( data, topic ){
    console.log( topic, data );
};

// subscribe to topic 'channel1'
// Keep returned id to unsubscribe
var subscriberId = tower.subscribe('channel1')(logger);

// publish to 'channel1'
// returns true if any listerns otherwise returns false
tower.publish('channel1')({message: 'Hello, World!'});

// Unsubscribe from topic
// requires both channel and subscriberId
tower.unsubscribe('channel1')(subscriberId);
```

## Tips
Use curried function to create custom listeners

```js
var ListenToResizeEvents = tower.subscribe('resize-events');

// Later
ListenToResizeEvents(logger);
```

Unsubscribe all listeners from a topic by not passing a subscriberId
```js
ListenToResizeEvents(logger);
ListenToResizeEvents(otherFunc);

var clearResizeListeners = tower.unsubscribe('resize-events');
clearResizeListeners();
```

## Debug Code

