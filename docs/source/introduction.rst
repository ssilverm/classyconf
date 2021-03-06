What's classyconf
-----------------

Classyconf is a framework agnostic python library created to make easy the
separation of configuration and code.

It adds a declarative way to define settings for your projects contained in a
class that can be extended, config objects can be passed around modules and
settings are lazily loaded, plus some other goodies (aka `dunder`_ methods).

It's classy, it's pretty, it's good.


Motivation
++++++++++

Configuration is just another API of you app, aimed for users who will install
and run it, that allows them to *preset* the state of a program, without having
to interact with it, only through static files or environment variables.

It is an important aspect of the architecture of any system, yet it is
sometimes overlooked.

It is important to provide a clear separation of configuration and code. This
is because config varies substantially across deploys and executions, code
should not. The same code can be run inside a container or in a regular
machine, it can be executed in production or in testing environments.


Settings discoverability
++++++++++++++++++++++++

Well designed applications allow different ways to be configured. For example
command line args are great to explore an app from the shell, but when you
already know what you want it would be great to set some defaults in a
configuration file somewhere.

But what happens if a setting is passed as command line arg but also exist in
the config file?

A proper settings-discoverability chain goes as follows:

1. First command line args are checked.
2. Then Environment variables.
3. Config files in different directories, that also imply some hierarchy. For
   example: config files in ``/etc/myapp/settings.ini`` are applied
   system-wide, while ``~/.config/myapp/settings.ini`` take precedence and are
   user-specific.
4. Hardcoded constants as defaults.

Each one of this sources of configuration need to be properly collected and
overwritten with an explicit level of hierarchy.

This raises the need to consolidate configuration in a single source of truth
to avoid having config management scattered all over the codebase.


Parsing and casting
+++++++++++++++++++

Not only each different source of configuration needs to be parsed differently
but also each setting might need to be converted from a generic type like strings to
proper types like integers or db connection structs.

Also each source of configuration follows some naming conventions, CLI args
look like this ``--fag=true`` while environment variables can be ``FLAG=on``.


A settings architecture
+++++++++++++++++++++++

Classyconf was born as a wrapper around `prettyconf`_, inspired by
`goodconf`_, originally trying to follow the recomendations of `12 Factor`_'s
topic about configs, but expanded to address all the cases stated above.

The good practices that this library suggest have an agnostic approach to
configure applications, no matter if they are web, CLI or GUI apps, hosted on
the cloud or running in your desktop.

Classyconf aims to be the settings management solution for perfectionists
with deadlines.


.. _`12 Factor`: http://12factor.net/
.. _`prettyconf`: https://github.com/osantana/prettyconf
.. _`goodconf`: https://github.com/lincolnloop/goodconf
.. _`dunder`: https://nedbatchelder.com/blog/200605/dunder.html
