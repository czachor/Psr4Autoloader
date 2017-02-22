# PSR-4 autoloader implementation

Specification: http://www.php-fig.org/psr/psr-4/

Based on: https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-4-autoloader-examples.md

Changes compared to original file:
* remove "Class" suffix
* small code changes and cleanup

An example of a general-purpose implementation that includes the optional
functionality of allowing multiple base directories for a single namespace
prefix.

Given a foo-bar package of classes in the file system at the following
paths ...

    /path/to/packages/foo-bar/
        src/
            Baz.php             # Foo\Bar\Baz
            Qux/
                Quux.php        # Foo\Bar\Qux\Quux
        tests/
            BazTest.php         # Foo\Bar\BazTest
            Qux/
                QuuxTest.php    # Foo\Bar\Qux\QuuxTest

... add the path to the class files for the \Foo\Bar\ namespace prefix
as follows:

     <?php
     // instantiate the loader
     $loader = new \Czachor\Psr4Autoloader;

     // register the autoloader
     $loader->register();

     // register the base directories for the namespace prefix
     $loader->addNamespace('Foo\Bar', '/path/to/packages/foo-bar/src');
     $loader->addNamespace('Foo\Bar', '/path/to/packages/foo-bar/tests');

The following line would cause the autoloader to attempt to load the
\Foo\Bar\Qux\Quux class from /path/to/packages/foo-bar/src/Qux/Quux.php:

     <?php
     new \Foo\Bar\Qux\Quux;

The following line would cause the autoloader to attempt to load the
\Foo\Bar\Qux\QuuxTest class from /path/to/packages/foo-bar/tests/Qux/QuuxTest.php:

     <?php
     new \Foo\Bar\Qux\QuuxTest;

# Installation
    $ composer require czachor/psr4-autoloader

# To do
* Tests.
