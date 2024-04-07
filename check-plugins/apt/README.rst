Check apt
=========

Overview
--------

This check allows a server administrator to get informed when new updates are available.
It will inform about the severity (security) of a package and if there are version changes. (dist-upgrade)

This check only runs on distributions using APT for package management, such as Debian, Ubuntu.

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

.. code-block:: test

    usage: apt [-h] [--always-ok] [-c CRITICAL] [-w WARNING]
               [--criticality {security,dist-upgrade,uncritical} [{security,dist-upgrade,uncritical} ...]]
               [--show-extended] [--update] [-V]

    This check provides basic information about updatable packages, mostly using python-apt

    options:
      -h, --help            show this help message and exit
      --always-ok           Always returns OK
      -c CRITICAL, --critical CRITICAL
                            Threshold number of packages to return "critical". "0" and unset do not emit
                            critical
      -w WARNING, --warning WARNING
                            Threshold number of packages to return "warning". "0" and unset do not emit
                            warning
      --criticality {security,dist-upgrade,uncritical} [{security,dist-upgrade,uncritical} ...]
                            Defines on which type of package updates the check returns critical. "uncritical
                            never returns critical" "dist-upgrade returns CRITICAL on dist-upgrades"
                            "security" returns CRITICAL if the updated version's source is the distributions
                            security repo
      --show-extended       Show human readable package priority, package source repository and current and
                            pending version.
      --update              If set, check runs "apt update" on every run. Needs sudo.
      -V, --version         show program's version number and exit


Usage Examples
--------------

Just a list:

.. code-block:: bash
    sudo python3 apt --update --warning 0 --critical 0 --criticality security dist-upgrade

Output:

.. code-block:: text

    Found pending updates. 9/2494, dist: 0, security: 0

    Normal updates:
      - qemu-system-x86
      - firmware-sof-signed
      - qemu
      - qemu-utils
      - qemu-system-common
      - qemu-block-extra
      - codium
      - qemu-system-data
      - qemu-system-gui|'installed'=2494;;;0; 'upgradable'=9;;;0; 'security'=0;;;0; 'dist-upgrade'=0;;;0

Showing extended information:

.. code-block:: bash

    sudo python3 apt --update --warning 0 --critical 0 --criticality security dist-upgrade --show-extended


.. code-block:: text

    Found pending updates. 9/2494, dist: 0, security: 0

    Standard updates:


    Package             ! Current Version        ! New Version            ! Size     ! Priority ! Archive       ! Component  ! Site
    --------------------+------------------------+------------------------+----------+----------+---------------+------------+-----------------------
    qemu-system-x86     ! 1:6.2+dfsg-2ubuntu6.17 ! 1:6.2+dfsg-2ubuntu6.18 ! 9.6MiB   ! optional ! jammy-updates ! main       ! de.archive.ubuntu.com
    firmware-sof-signed ! 2.0-1ubuntu4.5         ! 2.0-1ubuntu4.7         ! 1.2MiB   ! optional ! jammy-updates ! restricted ! de.archive.ubuntu.com
    qemu                ! 1:6.2+dfsg-2ubuntu6.17 ! 1:6.2+dfsg-2ubuntu6.18 ! 13.8KiB  ! optional ! jammy-updates ! universe   ! de.archive.ubuntu.com
    qemu-utils          ! 1:6.2+dfsg-2ubuntu6.17 ! 1:6.2+dfsg-2ubuntu6.18 ! 1.5MiB   ! optional ! jammy-updates ! main       ! de.archive.ubuntu.com
    qemu-system-common  ! 1:6.2+dfsg-2ubuntu6.17 ! 1:6.2+dfsg-2ubuntu6.18 ! 2.0MiB   ! optional ! jammy-updates ! main       ! de.archive.ubuntu.com
    qemu-block-extra    ! 1:6.2+dfsg-2ubuntu6.17 ! 1:6.2+dfsg-2ubuntu6.18 ! 66.6KiB  ! optional ! jammy-updates ! main       ! de.archive.ubuntu.com
    codium              ! 1.87.2.24072           ! 1.88.0.24096           ! 88.2MiB  ! optional !               ! main       ! download.vscodium.com
    qemu-system-data    ! 1:6.2+dfsg-2ubuntu6.17 ! 1:6.2+dfsg-2ubuntu6.18 ! 1.4MiB   ! optional ! jammy-updates ! main       ! de.archive.ubuntu.com
    qemu-system-gui     ! 1:6.2+dfsg-2ubuntu6.17 ! 1:6.2+dfsg-2ubuntu6.18 ! 214.9KiB ! optional ! jammy-updates ! main       ! de.archive.ubuntu.com


States
------

* WARN or CRIT if number of updates exceeds certain thresholds (default 1/disabled(0))
* CRIT if packages for dist-upgrade are available (default off)
* CRIT if packages from security sources are available (default off)


Perfdata / Metrics
------------------

.. csv-table::
    :widths: 25, 15, 60
    :header-rows: 1

    Name,                                       Type,               Description
    installed,                                  Number,             "Number of packages installed via dpkg/apt."
    upgradable,                                 Number,             "Total number of upgradable packages"
    security,                                   Number,             "Number of updates from distribution security sources."
    dist-upgrade,                               Number,             "Number of packages held back"


Credits, License
----------------

* Authors: `Linuxfabrik GmbH, Zurich <https://www.linuxfabrik.ch>`_
* License: The Unlicense, see `LICENSE file <https://unlicense.org/>`_.