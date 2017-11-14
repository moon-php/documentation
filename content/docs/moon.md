+++
title= "Moon"
description = "Moon micro-framework core"
date = "2017-04-10T16:43:08+01:00"
weight = 2
bref = "Moon micro-framework core"
+++

<h3 class="section-head" id="introduction"><a href="#introduction">Introduction</a></h3>

Moon is a micro-framework built using the latest version of PHP and using only PSR interfaces for 	
ensure the best flexibility and interchangeability. 

The concept of this framework is to keep the focus on the Domain logic of your application, instead of using a framework with thousands of files.

If you will need a library, you'll use composer, that's it.

<h3 class="section-head" id="installation"><a href="#installation">Installation</a></h3>

It's recommended that you use [Composer](https://getcomposer.org/) to install Moon.

```bash
$ php composer.phar require moon-php/moon
```

This will install Moon, it requires PHP 7.1 or newer.

<h3 class="section-head" id="usage"><a href="#usage">Usage</a></h3>

The micro-framework is really simple to build, just use a container and pass it to the AppFactory. 
 
The container will need at least the ResponseInterface and the ServerRequestInterface, all the other one are optional.

##### Build the App
    <?php
    $entries = [
        Psr\Http\Message\ResponseInterface::class => function() {
            // return a Psr\Http\Message\ResponseInterface instance
        },
        Psr\Http\Message\ServerRequestInterface::class => function() {
            // return a Psr\Http\Message\ServerRequestInterface instance
        }
    ];
    $container = new Container($entries);
    $app = AppFactory::buildFromContainer($entries); 


If you need other custom logic for the micro-framework built in component, you can do it.
And you can do it easily.

Before create the App, you need to specify in the container the custom classes you want to use.
 
###### Moon\Moon\Processor\ProcessorInterface:
Use it for override the default Moon\Moon\Processor\WebProcessor

It handle the logic for process the middleware/callback/pipeline stack

###### Moon\Moon\Matchable\MatchableRequestInterface:
Use it for override the default Moon\Moon\Matchable\MatchableRequest

It handle the logic for match a request to a route

###### Moon\Moon\Handler\ErrorHandlerInterface:
Use it for override the default Moon\Moon\Handler\ErrorHandler

It handle the logic for show the Error response

###### Moon\Moon\Handler\InvalidRequestHandlerInterface:
Use it for override the default Moon\Moon\Handler\InvalidRequestHandler

It handle the logic for show the InvalidRequest page

###### Moon\AppFactory::STREAM_READ_LENGTH
Ise it for override the default chunk length for the response
