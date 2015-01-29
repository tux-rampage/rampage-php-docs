.. _requirejs.config:

Configuration
#############

Since rampage-php allows a very modular architecture with assets from different modules,
you may have to define your require.js modules in order to make them accessible.

* :ref:`requirejs.config.module`
* :ref:`requirejs.config.template`
* :ref:`requirejs.config.scripturl`
* :ref:`requirejs.config.baseurl`


.. _requirejs.config.module:

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


.. _requirejs.config.template:

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

.. _requirejs.config.scripturl:


Defining the require.js location
================================

Sometimes you want to use a different version than the one bundled with rampage php.
In this case you can specify the require.js location by passing it as parameter to the ``requireJs()`` helper:

.. code-block:: html+php

    <?php echo $this->requireJs($this->resourceUrl('@my.app/js/require.js')); ?>


.. _requirejs.config.baseurl:

Defining the base url
=====================

Mostly this may apply to themes that come with a lot of components. Instead of defining every module, you can set the base url
by calling ``setBaseUrl()`` on the ``requireJs()`` helper in your view scripts.

.. code-block:: php

    // Search all undefined modules in the theme's js/ directory
    $this->requireJs()->setBaseUrl($this->resourceUrl('js'));


.. note::

    The base url is global and only points to a specific theme. You cannot overwrite single require.js modules
    in the same way as view scripts. You'll have to define the overwritten module as described
    in ref:`requirejs.config.template`.
