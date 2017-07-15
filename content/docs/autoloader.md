+++
title= "Autoloader"
description = "Autoloader supporting PSR-0 & PSR-4"
date = "2017-04-10T16:43:08+01:00"
weight = 8
bref = "Autoloader supporting PSR-0 & PSR-4"
toc = true
+++

<h3 class="section-head" id="introduction"><a href="#introduction">Introduction</a></h3>
Autoloader is a standalone component incredibly easy.
It's a small autoloader supporting for PSR4 and PSR0.
It also support a map autoloading.

<h3 class="section-head" id="installaton"><a href="#installaton">Installation</a></h3>

It's recommended that you use [Composer](https://getcomposer.org/) to install Moon Autoloader.

```bash
$ php composer.phar require moon-php/autoloader
```

This will install Autoloader, it requires PHP 7.1 or newer.

<h3 class="section-head" id="usage"><a href="#usage">Usage</a></h3>

The Autoloader has 2 different classes.
- One for PSR-4 & PSR-0
- One for manual mapping.

Both the classes have register and unregister methods, for create or destroy an autoloader instance.
 
##### PSRAutoloader

    <?php
    $autoloader = new PsrAutoloader();
    $autoloader->addNamespace('JohnSmith\\Container\\', 'vendor/JohnSmith/Container/src');
    $autoloader->addNamespace('JohnSmith\\Logger\\', 'vendor/JohnSmith/Logger/src');
    $autoloader->addNamespace('MarkBuzz\\Router\\', 'vendor/MarkBuzz/Router/src//MarkBuzz/Router/', PsrAutoloader::PSR0);
    $autoloader->register(); // For enable this autoloader 
    
    // Now you can create object without require all the files
    $container = new JohnSmith\Container\Container();
    $logger = new JohnSmith\Logger\StaticLogger();
    
    $autoloader->unregister(); // For disable this autoloader

##### MapAutoloader

    <?php
    $autoloader = new MapAutoloader();
    $autoloader->addNamespace('JohnSmith\\Package\\Class', 'vendor/JohnSmith/Package/main/common/mainClass.php');
    $autoloader->register(); // For enable this autoloader
    
    // Now you can create object without require all the files
    $container = new JohnSmith\Package\Class();
    
    $autoloader->unregister(); // For disable this autoloader
