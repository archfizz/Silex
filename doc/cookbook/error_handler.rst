How to convert errors to exceptions
===================================

Silex will catch exceptions that are thrown from within a request/response
cycle. It will however *not* catch PHP errors and notices. You can catch them
by converting them to exceptions, this recipe will tell you how.

Why does Silex not do this?
---------------------------

Silex could do this automatically in theory, but there is a reason why it does
not. Silex acts as a library, this means that it does not mess with any global
state. Since error handlers are global in PHP, it is your responsibility as a
user to register them.

Registering the ErrorHandler
----------------------------

Fortunately, Silex ships with an ``ErrorHandler`` (it's part of the
``HttpKernel`` package) that solves this issue. It converts all errors to
exceptions, and exceptions can be caught by Silex.

You register it by calling the static ``register`` method::

    use Symfony\Component\HttpKernel\Debug\ErrorHandler;

    ErrorHandler::register();

It is recommended that you do this in your front controller, i.e.
``web/index.php``.

.. note::

    The ``ErrorHandler`` has nothing to do with the ``ExceptionHandler``. The
    ``ExceptionHandler`` is responsible for displaying caught exceptions
    nicely.
