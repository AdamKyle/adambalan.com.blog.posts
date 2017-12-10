[Arctic Events](https://www.npmjs.com/package/arctic-events) 0.1.0 has been re-written from the ground up, almost.

The api it's self has been simplified and the concept of the library has been made simpler. The goal was to reduce the amount of complexity and fix some rather jarring bugs and issues with the first iteration of the library.

Lets look at how simple it is now to create and trigger events. Checkout the [README](https://github.com/AdamKyle/arctic-events/blob/master/README.md) for more depth.

```js
const EventHandler = require('arctic-events');

EventHandler.register('event.name', (a, b, eventHandler) => {
  console.log(a, b, eventHandler);
});

EventHandler.trigger('event.name', 'hello', 'world');

// console.log:

hello,
world,
EventHandler { events: [ { name: 'event.name', cb: [Function] } ] }
```

As you can see we register an event with two parameters: `a` and `b`. Upon triggering the event we pass in `this` which comes back as `eventHandler` to give you access to the `EventHandler` class object. This can be useful if you have subclassed the `EventHandler` class and have additional methods to call when triggering an event.

As you can see this iteration, as opposed to [0.0.6](http://adambalan.com/post/arctic-events) is cleaner and simpler and less error prone then the previous version.

## Questions To Answer

One of the few questions I have answer is:

- Should I introduce the concept of promises?:

  ```js
  EventHandler.triggerAsync('event.name', 'hello', 'world').then((result) => { ... });
  ```

- Should I allow you to trigger all events?:

  ```js
  EventHandler.triggerAll()
  ```

  - Which leads me to ask how I would handle if some events had params and others did not?
  - This also leads me down the path of: Should I do this async such that they return an array of results?

- Should I introduce the concept of listeners? or is the callback good enough?

These questions I hope to get answers from the community. Right now the API is deadly simple. Slightly inspired by Node Event Management.

I look forward to your feedback.
