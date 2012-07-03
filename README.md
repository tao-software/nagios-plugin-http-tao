nagios-plugin-http-tao
======================

This is a python plugin for Nagios (written for Nagios 2 originally) that tries to
* be more intelligent: By default, 30x status codes are resolved and only the end result is compared for correctness (unless an endless loop is detected, that is)
* be more configurable: You can specify which status codes are allowed (so you can e.g. allow a 404 as correct, if you just want to check for 5xx or connection errors)

Installation
------------
Put check_http_tao into your plugins directory (e.g. `/usr/lib/nagios/plugins.local`), and then define some commands:
    # This is a drop-in replacement for check_http
    define command{
            command_name tao_http
            command_line /usr/lib/nagios/plugins.local/check_http_tao $HOSTNAME$
    }

    # This is a more elaborate example: Connect some HTTP server on a custom port,
    # only checking whether the connection works
    define command{
            command_name tao_appserver
            command_line /usr/lib/nagios/plugins.local/check_http_tao $HOSTNAME$:8001 404
    }

