+++
title= "Http-Middleware"
description = "Http-Middleware supporting PSR-15"
date = "2017-04-10T16:43:08+01:00"
weight = 5
bref = "Http-Middleware supporting PSR-15"
toc = true
+++

<h3 class="section-head" id="introduction"><a href="#introduction">Introduction</a></h3>
Http-Middleware is a standalone component supporting.

**Accpeted as [awesome psr-15 middleware](https://github.com/middlewares/awesome-psr15-middlewares#packages) package**

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

So i decided to make the **Delegate** a **Middleware Dispatcher** itself.

The object is really simple, it has a constructor that requires an **array of MiddlewareInterface** implementor, a callable to use as **default** response and optionally a PSR-7 Container for lazy loading middleware.

The MiddlewareInterface will be directly implemented by the userland and inserted into the array.

    $request = new ServerRequestImplementor();
    $delegate = new Delegate([new MiddlewareOne(), new MiddlewareTwo(), new MiddlewareThree()], new DefaultResponse());
    $delegate->process($request);

It's also possible to pass a PSR-7 Container, as third argument, and will instantiate/load the object at runtime.
This approach is preferable because will not load all the **MiddlewareInterface** before the execution.

    $conatiner= new Container(); // This container will retireve the middleware at runtime. $container->get('middlewareOne');
    $request = new ServerRequestImplementor();
    $delegate = new Delegate(['middlewareOne', 'middlewareTwo', 'middlewareThree'], new DefaultResponse(), $container);
    $delegate->process($request);

#### InvalidArgumentException

If an object passed into the array is not a MiddlewareInterface implementor an **InvalidArgumentException** will be thrown while the Delgate is processing.
