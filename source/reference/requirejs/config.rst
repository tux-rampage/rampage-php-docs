.. requirejs.config:

Configuration
#############

Since rampage-php allows a very modular architecture with assets from different modules,
you may have to define your require.js modules in order to make them accessible.


.. requirejs.config.module:

Definition via module config
============================

From your module config, you can define require.js modules, packages and bundles. Just add the definition to your
config array. You may specify them via asset path or absolute URL.

.. code-block:: php

    return [
        'requirejs' => [
            'modules' => [
                'jquery' => '//code.jquery.com/jquery-2.1.3.min.js', // absolute url
                'jquery' => '@my.app/js/jquery.js', // Asset path
                'foo/bar' => '@my.app/js/foo/bar.js', // Another asset path
            ],

            'packages' => [
                'foopack' => '@my.app/js/foopack',
            ],

            'bundles' => [
                'myapp' => [ 'jquery', 'foo/bar' ],
            ],
        ]
    ];


.. requirejs.config.template:

Definition in view scripts
==========================

You can also dynamically define modules, packages and bundles in your view scripts.
To do so call teh appropriate helper method. All of these methods provide a fluent interface
by returning ``$this``.

.. code-block:: html+php

    <?php // viewscript

        $this->requirejs()->addModule('foo/bar', '@my.app/js/foo/bar.js');
        $this->requirejs()->addBundle('my.bundle', ['jquery', 'foo/bar']);
        $this->requirejs()->addPackage('foopack', '@my.app/js/foopack');

    ?>
    <!-- HTML goes here -->
