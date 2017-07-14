+++
title= "Container"
description = "Container supporting PSR-11"
date = "2017-04-10T16:43:08+01:00"
weight = 3
bref = "Container supporting PSR-11"
toc = true
+++

<h3 class="section-head" id="introduction"><a href="#introduction">Introduction</a></h3>
Container is a standalone component incredibly easy.
It's a container (yes, really) that implements only the PSR-11 interface without other method.

<h3 class="section-head" id="installation"><a href="#installation">Installation</a></h3>

It's recommended that you use [Composer](https://getcomposer.org/) to install Moon Container.

```bash
$ php composer.phar require moon-php/container
```

This will install Container, it requires PHP 7.1 or newer.

<h3 class="section-head" id="usage"><a href="#usage">Usage</a></h3>

The container accept as  constructor argument, an associative array.
The key (a.k.a alias) always has an entry.

##### Init Container

    $entries = [
        'alias' => function () {
            return new App\Acme\Class();
        }
    ];
    $container = new Container($entries);
        
The entry can be anything: an integer, a string, a closure or an instance.

##### Check if entry exists by alias

    $entries = [...];
    $container = new Moon\Container($entries);
    $container->has('alias'); // Return true or false

##### Getting an entry

    $entries = [...];
    $c = new Moon\Container($entries);
    $container->get('alias'); // Return the instance or throw a Moon\Container\Exception\NotFoundException
    

##### Entry with container resolution

An entry may require an instance of the container for other entries.
In this case, just use an argument in the function where the container instance will be bound.
 
         $entries = [];
         $entries['ten'] = 10;
         $entries['two'] = 2;
         $entries['multiply'] = function ($c) {
             return $c->get('ten') * $c->get('two');
         };
         $c = new Moon\Container($entries);
         $c->get('multiply'); // Return 20
