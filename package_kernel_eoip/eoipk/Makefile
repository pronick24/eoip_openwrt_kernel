#
# Copyright (C) 2006-2009 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk
include $(INCLUDE_DIR)/kernel.mk

PKG_NAME:=eoipk
PKG_RELEASE:=0.2

include $(INCLUDE_DIR)/package.mk

define KernelPackage/eoipk
  SECTION:=kernel
  CATEGORY:=Kernel modules
  SUBMENU:=Network Support
  TITLE:=Kernel mode EOIP tunnel compatible with MikroTik
  FILES:=\
	$(PKG_BUILD_DIR)/gre.ko \
	$(PKG_BUILD_DIR)/eoip.ko
  AUTOLOAD:=$(call AutoLoad,30,eoip)
endef

define Build/Compile
	$(MAKE) -C "$(LINUX_DIR)" \
		$(KERNEL_MAKE_FLAGS) \
		M="$(PKG_BUILD_DIR)" \
		EXTRA_CFLAGS="$(BUILDFLAGS)" \
		modules
endef

$(eval $(call KernelPackage,eoipk))
