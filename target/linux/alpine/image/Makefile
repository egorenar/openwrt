# Copyright (c) 2014 The Linux Foundation. All rights reserved.
#
include $(TOPDIR)/rules.mk
include $(INCLUDE_DIR)/image.mk

DEVICE_VARS += NETGEAR_BOARD_ID NETGEAR_HW_ID

define Device/Default
	PROFILES := Default
	KERNEL_DEPENDS = $$(wildcard $(DTS_DIR)/$$(DEVICE_DTS).dts)
	KERNEL_LOADADDR = 0x8000
	DEVICE_DTS = $$(SOC)-$(lastword $(subst _, ,$(1)))
	IMAGES := sysupgrade.bin
	IMAGE/sysupgrade.bin = sysupgrade-tar | append-metadata
	IMAGE/sysupgrade.bin/squashfs :=
endef

define Device/DniImage
	KERNEL_SUFFIX := -uImage
	KERNEL = kernel-bin | append-dtb | uImage none
	KERNEL_NAME := zImage
	NETGEAR_BOARD_ID :=
	NETGEAR_HW_ID :=
	UBINIZE_OPTS := -E 5
	IMAGES += factory.img
	IMAGE/factory.img := append-string -e '\xff\xff\xff\xff' | append-kernel | pad-offset $$$$(BLOCKSIZE) 64 | append-uImage-fakehdr filesystem | pad-to $$$$(KERNEL_SIZE) | append-ubi | netgear-dni
	IMAGE/sysupgrade.bin := append-string -e '\xff\xff\xff\xff' | append-kernel | pad-offset $$$$(BLOCKSIZE) 64 | append-uImage-fakehdr filesystem | sysupgrade-tar kernel=$$$$@ | append-metadata
endef

define Device/netgear_r9000
	$(call Device/DniImage)
	DEVICE_VENDOR := NETGEAR
	DEVICE_MODEL := Nighthawk X10 R9000
	SOC := alpine
	KERNEL_SIZE := 32768k
	NETGEAR_BOARD_ID := R9000
	NETGEAR_HW_ID := 29765235+0+512+1024+4x4+4x4
	BLOCKSIZE := 128k
	PAGESIZE := 2048
	BOARD_NAME := r9000
	SUPPORTED_DEVICES += r9000
	DEVICE_PACKAGES :=
	IMAGES += dtb nand.ubi
	IMAGE/dtb := install-dtb
	IMAGE/nand.ubi := append-ubi
endef
TARGET_DEVICES += netgear_r9000

$(eval $(call BuildImage))
