Check apt
=========

Overview
--------

This check allows a server administrator to get informed when new updates are available.
It will inform about the severity (security) of a package.

This check only runs on distributions using APT for package management, such as Debian, Ubuntu or Linux Mint.

Fact Sheet
----------

.. csv-table::
    :widths: 30, 70

    "Check Plugin Download",                "https://github.com/Linuxfabrik/monitoring-plugins/tree/main/check-plugins/apt"
    "Check Interval Recommendation",        "Once a day"
    "Can be called without parameters",     "Yes"
    "Compiled for",                         "Linux"

Help
----


Usage Examples
--------------


States
------

* WARN
* WARN
* CRIT
* CRIT


Perfdata / Metrics
------------------




Troubleshooting
---------------


Credits, License
----------------