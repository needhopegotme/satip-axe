# satip-axe

Requirements:

  - git, python
  - STLinux 2.4 (all-sh4-glibc) - http://www.stlinux.com - installed to /opt/STM/STLinux-2.4/
  - fakeroot package/tools

Compilation:

  - just type 'make'
  - kernel with rootfs is in kernel/arch/sh/boot/uImage.gz

Booting uImage.gz on Inverto IDL-400s/Grundig GSS.BOX/Inverto IDL-400S from USB:

  - connect TTL USB serial adapter to J3 connector (4 pins at the power supply)
    - pin 1 = 3.6V (do not use), pin 2 = GND, pin 3 = RXD (STM CPU), pin 4 = TXD (STM CPU)
    - parameters: 115200,8N1
  - press 'Enter' when you turn on the box (you have only one second) to get 'idl4k> ' prompt
  - modify bootargs (optional - for original firmware)

  set bootargs=console=ttyAS0,115200

  - set debugfw environment variable

  set debugfw "debugfw=usb start;usb start;fatload usb 0 0x84000000 uimage.gz;set bootargs console=ttyAS0,115200 bigphysarea=20000 initrd=/sbin/init;bootm 0x84000000"

  - you may type 'save' to store this settings permanently
  - to execute the debugfw type 'run debugfw'
  - note that the USB stick should be in the first (upper) USB connector
