# Makefile to put U-Boot or and/or bl1 onto an SD card

# Mac address for my board:
# GENERIC ether read: -1
# MAC address:  [d2:a5:61:c9:2e:e4] (tjt)

all: uboot

DD = dd

# Make a card to do the network boot via U-boot
uboot:
	$(DD) if=bl1-sd.bin of=${DEV} bs=512 seek=1 conv=fdatasync
	$(DD) if=u-boot.bin of=${DEV} bs=512 seek=129 conv=fdatasync
	$(DD) if=env.img of=${DEV} bs=512 seek=5889 conv=fdatasync
	sync

bl1-usb:
	$(DD) if=bl1-usb.bin of=${DEV} bs=512 seek=1 conv=fdatasync

bl1-sd:
	$(DD) if=bl1-sd.bin of=${DEV} bs=512 seek=1 conv=fdatasync

zap:
	dd if=/dev/zero of=${DEV} bs=512 seek=1 count=8192

# ------------------------------------

img:
	$(DD) if=u-boot.img of=${DEV} conv=fdatasync
	sync

fetch_img:
	$(DD) if=${DEV} of=u-boot.img bs=512 count=8192
	sync

# ------------------------------------

# See U-boot sources include/configs for
# CONFIG_ENV_SIZE and CONFIG_ENV_OFFSET

env:
	$(DD) if=env.img of=${DEV} bs=512 seek=5889 conv=fdatasync
	sync

fetch_env:
	$(DD) if=${DEV} of=env.img bs=512 skip=5889 count=32
	sync

# THE END
