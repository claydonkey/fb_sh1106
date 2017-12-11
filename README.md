# fb_sh1106
SH1106 oled linux device tree overlay and kernel module for 32bit Raspberry Pi 4.9.x

An omittion in the nostro and linux mainline kernels (< 4.12). 
Compile and copy for SH1106 oled displays.

as of 2015-01-19 The FBTFT drivers are now in the Linux kernel staging tree: https://git.kernel.org/cgit/linux/kernel/git/gregkh/staging.git/tree/drivers/staging/fbtft?h=staging-testing
Development in this github repo has ceased.

## Instructions

Make sure you have:

A kernel supporting device tree overlays

The relevent kernel-headers: 
$ pacman -S  linux-raspberrypi-headers #for arch-linux

The device tree compiler: 
$ pacman -S dtc

## Compile and Install

$ make 
$ gzip fb_sh1106.ko 
$ sudo cp fb_sh1106.ko.gz /lib/modules/`uname -r`/extramodules
$ sudo depmod -a
$ dtc -O dtb -o sh1106.dtbo -b 0 -@ sh1106-overlay.dts
$ sudo cp sh1106.dtbo /boot/overlays

add to /boot/config.txt
dtparam=spi=on
dtoverlay=sh1106
