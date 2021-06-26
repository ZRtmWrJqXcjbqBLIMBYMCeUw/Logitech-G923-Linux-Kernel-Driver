# Logitech G923 Linux Kernel Driver
This project is intended to add support for the Logitech G923 steering wheel to the Linux kernel.

## Latest Updates

### G923 PS4 Version
This appears to work similar to the G29 and will require the [new-lg4ff](https://github.com/berarma/new-lg4ff) module, with the code from this [pull request](https://github.com/berarma/new-lg4ff/pull/50). Automatic mode switching does not currently work and will require the following udev rule in order to work:
```
ATTR{idVendor}=="046d", ATTR{idProduct}=="c267", RUN+="/usr/sbin/usb_modeswitch -v 046d -p c267 -M 30f8090701010000 -m 03 -r 03"
```

Usually placed in a file in `/etc/udev/rules.d` followed by running `sudo udevadm control --reload`.

Big thanks to @JacKeTUs for figuring this out and to @berarma for maintaining the new-lg4ff module.

### G923 XBox Version
The following patch has been recently submitted to the Linux input mailing list: https://patchwork.kernel.org/project/linux-input/list/?series=489571. The compilation error appears to be resolved by replacing `g923_hidpp_init` with `switch_to_hidpp_cmd`. I am not able to test this as I do not have the XBox version of the wheel. Discussion of this patch's functionality is more than welcome on this project.

As a result of this patch being publicly available, the patch in this project will be removed.

## Useful references
1. https://lekensteyn.nl/files/logitech/logitech_hidpp_2.0_specification_draft_2012-06-04.pdf
1. https://opensource.logitech.com/opensource/images/c/ce/Logitech_Force_Feedback_Protocol_V1.5.pdf
1. https://github.com/cvuchener/hidpp
1. https://www.logitech.com/assets/54557/2/g920-driving-forcetm-racing-wheel.pdf
1. https://usb.org/sites/default/files/hut1_2.pdf
1. https://lekensteyn.nl/files/logitech/logitech_hidpp10_specification_for_Unifying_Receivers.pdf
1. https://www.usb.org/sites/default/files/documents/hut1_12v2.pdf
1. https://who-t.blogspot.com/2018/12/understanding-hid-report-descriptors.html
1. https://www.usb.org/sites/default/files/hid1_11.pdf
1. https://opensource.logitech.com/opensource/images/6/6e/Logitech_Force_Feedback_Protocol_V1.6.pdf

### Useful tools
1. https://gitlab.freedesktop.org/libevdev/hid-tools

