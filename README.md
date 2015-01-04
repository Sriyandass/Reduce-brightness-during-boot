reduce-brightness-during-boot
=============================

Brightness is maupulated using the */sys/class/backlight/intel_backlight/brightness* file.
Inputs to that file changes the brightness of the machine. A few machines have */sys/class/backlight/acpi_video0/brightness*.
Follow the path to find out which one is yours. If your machine has */sys/class/backlight/acpi_video0/brightness* then,
that change has to be done in the code. 
That is, change 
*exec /bin/echo 150 > /sys/class/backlight/intel_backlight/brightness*
to, *exec /bin/echo 150 > /sys/class/backlight/acpi_video0/brightness*

Also, you have to find the lower and higher limits of inputs to your brightness file:
Lower limit is 0 higher limit is present in */sys/class/backlight/intel_backlight/max_brightness* (Ex. it is 4882 for me)

So I have given 150 as my input to the file. You can give what ever you wish. I would recommend 10% of the max value.
Once you have got the code compatible with your machine you have to add it to init. 
Fot that open terminal and add the following command

*gksu gedit /etc/init/fixbrightness.conf*

and enter the your code. Restart your computer to see if it works.

Note: This methord has only been tested on Ubuntu 14.04 and 14.10. It should work well on other Debian systems as well.
