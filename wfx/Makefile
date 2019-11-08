#
# Copyright (C) 2008-2012 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk
include $(INCLUDE_DIR)/kernel.mk

PKG_NAME:=wfx
PKG_RELEASE:=1

include $(INCLUDE_DIR)/package.mk

define KernelPackage/wfx
 $(call KernelPackage/mac80211/Default)
  SUBMENU:=Wireless Drivers
  TITLE:=Silabs WF200 Wireless Driver
  DEPENDS+=+wf200-firmware +kmod-mac80211 +kmod-cfg80211 +@DRIVER_11N_SUPPORT
#DEPENDS:=+kmod-mac80211 +@DRIVER_11N_SUPPORT
  FILES:=$(PKG_BUILD_DIR)/wfx.ko
  AUTOLOAD:=$(call AutoProbe,mac80211 wfx)

#MAINTAINER:=Daniel de kock <daniel@riot.network>
#KCONFIG:=CONFIG_WFX
  PROVIDES:=kmod-wfx
endef

define KernelPackage/wfx/description
 Silabs WF200 Wireless Driver
endef

EXTRA_KCONFIG:= \
	CONFIG_WFX=m

EXTRA_CFLAGS:= \
	$(patsubst CONFIG_%, -DCONFIG_%=1, $(patsubst %=m,%,$(filter %=m,$(EXTRA_KCONFIG)))) \
	$(patsubst CONFIG_%, -DCONFIG_%=1, $(patsubst %=y,%,$(filter %=y,$(EXTRA_KCONFIG)))) \

MAKE_OPTS:= \
	$(KERNEL_MAKE_FLAGS) \
	SUBDIRS="$(PKG_BUILD_DIR)" \
	EXTRA_CFLAGS="$(EXTRA_CFLAGS)" \
	$(EXTRA_KCONFIG)

#define Build/Prepare
#	mkdir -p $(PKG_BUILD_DIR)
#	$(CP) ./src/* $(PKG_BUILD_DIR)/
#endef


define Build/Compile
	$(MAKE) -C "$(LINUX_DIR)" \
		$(MAKE_OPTS) \
		modules
endef

$(eval $(call KernelPackage,wfx))
