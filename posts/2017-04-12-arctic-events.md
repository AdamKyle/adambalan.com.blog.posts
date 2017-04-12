[Arctic Events](https://www.npmjs.com/package/arctic-events) is a simple, very simple, event management and handler for Javascript, written purely in ES6 and compiled via webpack and published to [NPM](https://www.npmjs.com/package/arctic-events).

Ignore the out of date version badge, the actual version is 0.0.5 at the time of this blog.

Arctic Events was written solely as a learning experience and for a slightly larger project that I have in mind for my "Arctic" series of projects.

Much like my various "Ice Cream" projects, Arctic is leading towards something more fun and enjoyable. A small and simple game engine in React JS.

## Getting Started

To get started all you have to do:

```js
  yarn add arctic-events

  // and then in your JS file
  const EventHandler = require('arctic-events');
```

Simple. No fuss no muss.

## Registering Events

When it comes to event registration there are a couple things, which are [outlined in more detail in the README](https://github.com/AdamKyle/arctic-events/blob/master/README.md).

One is that the way events are handled are a bit different then what you are use to, we have the abillity to trigger a before, main and after event. the main is the event you register and the before and after are also registered.

A couple of things to note is that you can specify the before and after for a specific event or use the default first registered. Order does matter when it comes to before and after, in the case where you do not use `{use: {before: 'event.name', after: 'event.name'}}`

But lets back up. How do you even register a simple event?

```js
EventHandler.register('hello.world', () => {
  return 'hello world';
});

EventHandler.trigger('hello.world'); // => hello world
```

Thats it. Thats the simplest way to register an event.

### But Wait theres more

We can define before and after events, it's important to know that no matter what the before event returns its always passed to the main event and that no matter what the main event returns, it is also passed to the after event. This is then returned to you, when you do call trigger.

Lets look at an example:

```js
EventHandler.register('before.hello.world', () => {
  return 'Hello world.';
}, 'before');

EventHandler.register('hello.world', (beforeEventCbReturnValue) => {
  return beforeEventCbReturnValue + ' How are you?';
});

EventHandler.register('after.hello.world', (mainEventCBReturnValue) => {
  return mainEventCBReturnValue.toLowerCase();
}, 'after');

EventHandler.trigger('hello.world'); // => hello world. how are you?
```

First we have a couple of events registered. Notice how we pass a third argument: `before` and `after`?

These stipulate that these specific events are to be triggered before and after the main event.

We see that `before.hello.world` returns a value that is then passed to the main event, which then returns an value which is then passed to the after event which then returns the final result.

> ATTN!
>
> If you do not register a `after` event then what will happen is you will get back: `Hello World. How are
> you?`. You do not need to register a before or an after event.

Notice the parameters for each of the closures. When you define an `after` event you MUST pass a parameter that is the return value of the main event. Even if you do nothing with this parameter you MUST return it.

> ATTN!
>
> The `after` event must always return the passed in parameter. If it doesn't your results might not
> be as expected. Even if it just returns null or undefined.

The way we do things is that `before` returns something, which is then passed to the main event which then returns something, even if its undefined. Which is then passed to `after`. There probably isn't a time when you would use the results of a triggered event. The examples here, while simple, might show when you might want to use the values.

Another more detailed example is if you have an event that does a database request of some kind when triggered and thus returns the database object or some boolean value to tell you that it properly updated or failed to do what you wanted.

#### Defining multiple `before` and `after` events

What if we had multiple before and after events? But we wanted an event to use a specific set of before and after? or none at all? Or we didn't define which ones to choose?

To answer in order, lets define how an event would use a specific set of before and after events:

```js
EventHandler.register('hello.world', (beforeEventCbReturnValue) => {
  return beforeEventCbReturnValue + ' How are you?';
}, null, {use: {before: 'some.event.name', after: 'some.other.event.name'}});
```

What we have done here is passed null to the type and then stated that we are to use these specific event names for `before` and `after`

If we didn't want to use any `before` and `after` events we could do:

```js
EventHandler.register('hello.world', () => {
  return 'hello world';
}, null, false});
```

What ever is returned from this event will be returned from the `trigger` method.

And finally, we asked: What if we didn't define any events to use, but have many before and after?

order will matter, so for example, if you defined 6 `before` and 6 `after` events, the one you define first will be the first one used.

## Why Did You Build This?

I wanted to build some kind of event management/handler in Javascript. [I built one in PHP](https://github.com/AdamKyle/ice-cream-events) for Ice Cream.

I was also looking at a coupe of basic game engines in Javascript and while this event management system will eventually have to change to meet the requirements of what I have planned, for now it was a great and still is a great learning experience.

### Known Bugs

There are some questions and some known bugs with this system as it stands that I found as I was writing this blog post:

- ~~You can have events with duplicate names, this should throw an error.~~
- Why do we put such emphasis on passing returned value of `before` to `main` and then from main to `after` and then back to `trigger` for return a final value? What if the value is just undefined or null?

## Is The Project Maintained?

All Arctic projects are maintained, although not on a regular or consistent basis, how ever they are maintained and updated every so often. Most of the times its just updating dependencies, running tests and seeing if anything broke.
