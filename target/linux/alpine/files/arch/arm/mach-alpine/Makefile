# SPDX-License-Identifier: GPL-2.0-only

ccflags-$(CONFIG_ARCH_MULTIPLATFORM) := -I$(srctree)/$(src)/include

obj-y				+= alpine_machine.o
obj-y				+= al_hal_serdes.o
obj-y				+= al_fabric.o
obj-y				+= al_init_sys_fabric.o
obj-$(CONFIG_SMP)		+= platsmp.o alpine_cpu_pm.o
obj-$(CONFIG_HOTPLUG_CPU)	+= sleep-alpine.o
ifneq ($(CONFIG_HOTPLUG_CPU), y)
obj-$(CONFIG_CPU_IDLE_ALPINE)	+= sleep-alpine.o
endif

