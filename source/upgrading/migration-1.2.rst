.. _migration_1.2:

Migrating to 1.2
################

This version introduces some BC breaks to the previous versions.

Backward incompatible changes
=============================

* :ref:`migration_1.2.bcb.url`
* :ref:`migration_1.2.bcb.urlhelpers`
* :ref:`migration_1.2.bcb.ui`


.. _migration_1.2.bcb.url:

rampage\\core\\url has been removed
-----------------------------------

This component was removed in favour of a more generic implementation ``rampage\\core\\BaseUrl``.
Also all url locators relying on this component have been refactored.

The base url configuration can now be defined in the ``urls`` section of your config:

.. code-block:: php

    // module configs; config/conf.d/*.conf.php
    return [
        'urls' => [
            'base_url' => 'http://foo.bar.org/',
            'resources' => [
                'base_url' => 'http://foobar.somecdn.com/',
            ]
        ]
    ];


.. _migration_1.2.bcb.urlhelpers:

Refactored URL Locators / Helpers
---------------------------------

All url helpers and url locators have been refactored to accept a base url via constructor or/and a ``setBaseUrl()``.
This base url may be a string, a ``Zend\\Uri\\Http`` instance or a ``rampage\\core\\BaseUrl`` instance.

All dependencies to ``rampage\\core\\url`` components have been removed.

This simplifies the configuration of these components and removes uneccessary dependencies.


.. _migration_1.2.bcb.ui:

Removed rampage\\ui from main package
-------------------------------------

This component is removed from the main package.
It will be merged into a base ui implementation ``rampage-php/ui``.


