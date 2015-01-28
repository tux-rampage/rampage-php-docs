.. requirejs.usage:

How to add requirejs
####################

To enable require.js, you should render the ``requireJs()`` helper on the very bottom of your HTML, before the closing
``</body>`` tag **and before** the ``inlinescript()`` rendering.

Mostly you would do this in your layout view script.

.. code-block:: html+php

    <!DOCTYPE html>
    <html>
        <body>
            ...

            <?php echo $this->requireJs(); ?>
            <?php echo $this->inlinescript(); ?>
        </body>
    </html>

After that you can simply add requirejs enabled inline scripts anywhere in your view scripts:

.. code-block:: html+php

    <!-- view script -->
    <?php $this->inlinescript()->appendFile($this->resourceUrl('@my.module/js/foobar.js')); ?>

    <!-- even captured scripts are supported -->
    <?php $this->inlinescript()->captureStart(); ?>
        (function(factory) {
            require(['jQuery'], factory);
        }(function($) {
            $(document).ready(function() { // do something... });
        }));
    <?php $this->inlinescript()->captureEnd(); ?>
