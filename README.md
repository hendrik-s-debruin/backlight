Backlight
================================================================================

An overly simple script to control the backlight of monitors controlled by Intel
graphics cards.

The script makes no attempt to support other cards. I wrote this since
`xbacklight` and other utilities did not work for my machine. Refer to [the Arch
wiki](https://wiki.archlinux.org/index.php/Backlight) for more information on
how such scripts work.

Usage
================================================================================

To set percentage power of the backlight:

	$ backlight set <int>

Where `int` is a percentage expressed as an integer.

To decrease the brightness relative to the current brightness:

	$ backlight dec <int>

To increase, call:

	$ backlight inc <int>

Again, `int` is a percentage expressed as an integer.

Installation
================================================================================

Simply put the script in your `PATH`. In order for the script to work,  you need
write access to the file `/sys/class/backlight/intel_backlight/brightness`.
Typically only root can do this.

To fix this, add the following `udev` rule inside
`/etc/udev/rules.d/backlight.rules`:

	ACTION=="add", SUBSYSTEM=="backlight", KERNEL=="intel_backlight", RUN+="/bin/chgrp video /sys/class/backlight/%k/brightness"
	ACTION=="add", SUBSYSTEM=="backlight", KERNEL=="intel_backlight", RUN+="/bin/chmod g+w /sys/class/backlight/%k/brightness"

Then, add your user to the `video` group.

For more information, see [the
wiki](https://wiki.archlinux.org/index.php/Backlight#ACPI).
