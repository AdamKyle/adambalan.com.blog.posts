Ice Cream Events is the simplest event management library that I have ever built.

It was a learning experience from the get go, because I wanted to understand what exactly an event was.

Events consist of an the event itself, a listener, a registration and finally a dispatch.

You can [read more from the README](https://github.com/AdamKyle/ice-cream-events), how ever essentially we have to define an Event Listener class:

```php
use IceCreamEvents\Listener;

class PageViewEventListener extends Listener{

  // Read on to see the event definition.
  public function onAction(PageViewEvent $pageViewedEvent) {
     // ... Do something.
  }
}
```

And a Event:

```php
use IceCreamEvents\Event;

class PageViewEvent extends Event {

  protected $pageViewed;

  public function __construct(PageViewed $pageViewed) {
    $this->pageViewed = $pageViewed;
  }

  public function getPageViewed() {
    return $this->pageViewed;
  }
}
```

Then we need to register and dispatch:

```php
$eventHandler->register('page.viewed', PageViewEvent::class, PageViewEventListener::class, 'onAction');
$eventHandler->dispatch('page.viewed');
```

This is rather simple, we register an event, where all the logic happens. Weather thats updating a database column, fetching a record, alerting the user that something changed or what ever else.

Then we register this to a Listener and state what action on the listener should be fired when the event is dispatched.

When the event is dispatched in this case, the `PageViewEvent` class is passed to  the `onAction` method of the `PageViewEventListener`.

From there you can do additional logic, such as calling the `getPageViewed` function.

## Why Did You Build This?

I was fascinated by how Laravel built it's notification system and how other frameworks were handling the concept of "events" what ever their definition of an event was or is.

I built it strictly to learn, but have found that it can come in handy, should I want to create my own events for another Ice Cream Component.

## Is The Component Maintained?

All Ice Cream Components are maintained, although not on a regular or consistent basis, how ever they are maintained and updated every so often. Most of the times its just updating dependencies, running tests and seeing if anything broke.
