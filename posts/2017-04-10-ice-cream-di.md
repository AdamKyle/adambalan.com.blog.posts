Ice Cream DI is the next evolution of my Ice Cream project. A project where I spent the vast majority of my time understanding and learning how frameworks worked in components.

Based off of [Pimple](http://pimple.sensiolabs.org/) and [Symfony](http://symfony.com/doc/current/components/dependency_injection.html) I created something simple and easy to use.

The simplest way to understand Ice Cream DI is to see a simple demonstration:

```php
use IceCreamDI\Container;

$container = new Container();

$container['service'] = function($c) {
  return new Service();
}

$container['services']
```

You can see here that we register a container object called service, which we can then fetch at a later time
by doing `$container['service']`.

I allow you to extend a service by doing:

```php

$container->extend('service', function($service){
  $service-> ....

  ....

  return $service;
});
```

Here you can see we carry on from the registered service instance and we extend it, that is we do additional logic with it, so that when we call `$container['service']` to get the existing instance of it. In this case the  class is already set up. This is useful if you have some stuff you have to do before accessing the container object.

You can read more in depth in the [README](https://github.com/AdamKyle/ice-cream-di).

## Why Did You Build This?

I built it to learn more about how dependency injection works in frameworks. I wanted to understand how something got registered and then was called in various other places. With a lot of frameworks these days, it seems that there is this allure to magical-ness that happens behind the curtains. By building my own
implementation, I took away some of the mystery and really got to focus on the "How".

## Is The Component Maintained?

All Ice Cream Components are maintained, although not on a regular or consistent basis, how ever they are maintained and updated every so often. Most of the times its just updating dependencies, running tests and seeing if anything broke.
