#
# Copyright (C) 2008-2012 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=wfx
PKG_RELEASE:=1

#added backports
STAMP_CONFIGURED_DEPENDS := $(STAGING_DIR)/usr/include/mac80211-backport/backport/autoconf.h

include $(INCLUDE_DIR)/kernel.mk
include $(INCLUDE_DIR)/package.mk

define KernelPackage/wfx
 $(call KernelPackage/mac80211/Default)
  SUBMENU:=Wireless Drivers
  TITLE:=Silabs WF200 Wireless Driver
  DEPENDS:= \
	+wf200-firmware +kmod-mac80211 +kmod-cfg80211 +@DRIVER_11N_SUPPORT
  FILES:=$(PKG_BUILD_DIR)/wfx.ko
  AUTOLOAD:=$(call AutoProbe,mac80211 wfx)
  PROVIDES:=kmod-wfx
endef

define KernelPackage/wfx/description
 Silabs WF200 Wireless Driver
endef

NOSTDINC_FLAGS = \
	-I$(PKG_BUILD_DIR) \
	-I$(STAGING_DIR)/usr/include/mac80211-backport/uapi \
	-I$(STAGING_DIR)/usr/include/mac80211-backport \
	-I$(STAGING_DIR)/usr/include/mac80211/uapi \
	-I$(STAGING_DIR)/usr/include/mac80211 \
	-include backport/autoconf.h \
	-include backport/backport.h


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

define Build/Compile
#	$(MAKE) -C "$(LINUX_DIR)" \
#		$(MAKE_OPTS) \
#		modules
	+$(MAKE) -C "$(LINUX_DIR)" \
		$(MAKE_OPTS) \
		$(PKG_MAKE_FLAGS) \
		NOSTDINC_FLAGS="$(NOSTDINC_FLAGS)" \
		modules
endef

$(eval $(call KernelPackage,wfx))
