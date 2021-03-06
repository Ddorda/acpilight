acpilight: a backward-compatibile xbacklight replacement
========================================================

"acpilight" is a backward-compatibile replacement for xbacklight_, that uses
the ACPI interface to set the display brightness.


Motivation
----------

On some modern laptops "XRandR" might lack the ability to set the display
brightness. This capability was moved/unified to the kernel's ACPI interface,
via ``/sys/class/backlight/``.

"xbacklight" provides a drop-in replacement for the same command, using the
ACPI interface instead of "XRandR" in order to let old scripts run. As a
result, "xbacklight" can now also be used from the console and Wayland (X11 is
not used at all).


Setup
-----

Normally, users are prohibited to alter files in the ``sys`` filesystem. It's
advisable to setup an "udev" rule to allow users in the "video" group to set
the display brightness.

To do so, place a file in ``/etc/udev/rules.d/90-backlight.rules`` containing::

  SUBSYSTEM=="backlight", ACTION=="add", RUN+="/bin/chgrp video /sys/class/backlight/%k/brightness"
  SUBSYSTEM=="backlight", ACTION=="add", RUN+="/bin/chmod g+w /sys/class/backlight/%k/brightness"

to setup the relevant permissions at boot time.


Authors and Copyright
---------------------

| "acpilight" is distributed under GPLv3+ (see COPYING) WITHOUT ANY WARRANTY.
| Copyright(c) 2016 by wave++ "Yuri D'Elia" <wavexx@thregr.org>.

.. _xbacklight: http://cgit.freedesktop.org/xorg/app/xbacklight
