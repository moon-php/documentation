+++
title= "Http-Middleware"
description = "Http-Middleware supporting PSR-15"
date = "2017-04-10T16:43:08+01:00"
weight = 5
bref = "Http-Middleware supporting PSR-15"
toc = true
+++

<h3 class="section-head" id="introduction"><a href="#introduction">Introduction</a></h3>

Http-Middleware is a standalone component supporting PSR-15.

**Accpeted as [awesome PSR-15 middleware](https://github.com/middlewares/awesome-psr15-middlewares#packages) package**

<h3 class="section-head" id="installation"><a href="#installation">Installation</a></h3>

It's recommended that you use [Composer](https://getcomposer.org/) to install Moon Http-Middleware.

```bash
$ php composer.phar require moon-php/http-middleware
```

This will install Http-Middleware, it requires PHP 7.1 or newer.

<h3 class="section-head" id="usage"><a href="#usage">Usage</a></h3>

##### Delegate

According to the PSR-15 proposal : 

_The DelegateInterface defines a single method that accepts a request and returns a response._

_The delegate interface must be implemented by any middleware dispatcher that uses middleware implementing MiddlewareInterface._

In Moon Http-Middleware the **Delegate** is a **Middleware Dispatcher** itself.

The **Delegate** is really simple object, it has a constructor that requires 3 arguments.

- An **array of middleware/string**.
- A callable to use as **default** response
- **Optionally** a **PSR-11 Container** for lazy loading middleware.

The middlewares passed in the array can be immediately PSR-15 MiddlewareInterface instances or strings that will be resolved when needed by a PSR-11 Container.

When resolved by the container a PSR-15 MiddlewareInterface instance is expected to be returned.

    <?php
    $request = new ServerRequestImplementor();
    $delegate = new Delegate([new MiddlewareOne(), new MiddlewareTwo(), new MiddlewareThree()], new DefaultResponse());
    $delegate->process($request);

As said before, it's also possible to pass a PSR-7 Container to the **Delegate** that will instantiate/load the objects at runtime.

This approach is preferable because will not load all the Middlewares before the execution.

    <?php
    $conatiner= new Container(); // This container will retireve the middleware at runtime. $container->get('middlewareOne');
    $request = new ServerRequestImplementor();
    $delegate = new Delegate(['middlewareOne', 'middlewareTwo', 'middlewareThree'], new DefaultResponse(), $container);
    $delegate->process($request);

#### InvalidArgumentException

While the Delegate is processing the middleware stack if an invalid middleware is used, an **InvalidArgumentException** will be thrown.
