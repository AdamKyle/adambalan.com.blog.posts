Ice Cream Router is a simple wrapper for [Symfonys Router](http://symfony.com/doc/current/routing.html).

It's core goal is to understand how routing works in terms of a framework and to then expand upon that knowledge and create something that was simple, yet easy to expand and build upon. That was the whole
goal of the routing system.

The core of how it's used is laid out in it's [README](https://github.com/AdamKyle/ice-cream-router), how ever the gist of it is:

```php
use IceCreamRouter\Router;

$router = new Router();

$router->get('/foo/{id}', 'foo', function($id, $request, $response){
  return response->setContent('Id is: ' . $id);
});

$response = $router->processRoutes(Request::create('/foo/1', 'GET'));

var_dump($response->getContent()); // => Id is: 1
```

Here we see that we are instantiating a new instance of the router class, from there we create a basic `GET` request that accepts an `$id`, `$request` and a `$response`.

We then process the route by creating a new `GET` request to the now defined route and from there we can
get the content of the returned response.

## Reason For Building

Much like most things, the whole reason behind building the Ice Cream Router was a learning experience. I wanted to build the individual components of a framework and see what I could learn from doing so. There was a lot of a flack from the PHP community the first time I showed this off, the whole concept was: "Why reinvent the wheel." A fair and honest question, that deserves and even fairer and more honest answer: "I wanted to learn."

Ice Cream Router was the first project in the Ice Cream Components that I started to build and test and explore how different aspects of a framework worked. It was also the hardest one to wrap my head around and understand.

## Is The Component Maintained?

All Ice Cream Components are maintained, although not on a regular or consistent basis, how ever they are maintained and updated every so often. Most of the times its just updating dependencies, running tests and seeing if anything broke.
