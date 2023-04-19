#
# Copyright (C) 2006-2012 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk
#include $(INCLUDE_DIR)/kernel.mk

PKG_NAME:=eoipcr
PKG_VERSION:=1.0.2
PKG_RELEASE:=3

PKG_BUILD_DIR := $(BUILD_DIR)/$(PKG_NAME)

PKG_LICENSE:=GPL-2.0+

include $(INCLUDE_DIR)/package.mk

define Package/eoipcr
  SECTION:=net
  CATEGORY:=Network
  TITLE:=Kernel mode EOIP (need kernel module eoip+gre)
  DEPENDS:=+kmod-eoipk
endef

define Package/eoipcr/description
 Kernel mode EOIP (Ethernet Over IP) tunnel compatible with MikroTik RouterOS
endef

define Build/Prepare
		mkdir -p $(PKG_BUILD_DIR)
		cp $(CURDIR)/scr/* $(PKG_BUILD_DIR)
		$(Build/Patch)
endef

define Build/Compile
	$(TARGET_CC) -O3 -fno-stack-protector -flto -std=gnu90 -Wall -Wextra -c -o $(PKG_BUILD_DIR)/eoipcr.o $(PKG_BUILD_DIR)/eoipcr.c
	$(TARGET_CC) -O3 -fno-stack-protector -flto -std=gnu90 -Wall -Wextra -c -o $(PKG_BUILD_DIR)/libnetlink.o $(PKG_BUILD_DIR)/libnetlink.c
	$(TARGET_CC) -o $(PKG_BUILD_DIR)/eoipcr $(PKG_BUILD_DIR)/eoipcr.o $(PKG_BUILD_DIR)/libnetlink.o -O3 -fno-stack-protector -flto
endef

define Package/eoipcr/install
	$(INSTALL_DIR) $(1)/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/eoipcr $(1)/bin/
endef

$(eval $(call BuildPackage,eoipcr))
