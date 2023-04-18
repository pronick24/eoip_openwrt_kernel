#
# Copyright (C) 2006-2012 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk
#include $(INCLUDE_DIR)/kernel.mk

PKG_NAME:=eoipcr
PKG_VERSION:=1.0.1
PKG_RELEASE:=26

PKG_BUILD_DIR := $(BUILD_DIR)/$(PKG_NAME)
SOURCE_DIR:=/home/dope/openwrt/package/network/services/eoipcr/scr/

#STAMP_PREPARED := $(STAMP_PREPARED)_$(call confvar,CONFIG_MTD_REDBOOT_PARTS)

#PKG_LICENSE:=GPL-2.0+
#PKG_LICENSE_FILES:=

#PKG_FLAGS:=nonshared

include $(INCLUDE_DIR)/package.mk

define Package/eoipcr
  SECTION:=base
  CATEGORY:=Base system
  TITLE:=eoip new
endef

define Package/eoipcr/description
 eoipcr des
 big des
endef

define Build/Prepare
		mkdir -p $(PKG_BUILD_DIR)
		cp $(SOURCE_DIR)/* $(PKG_BUILD_DIR)
		$(Build/Patch)
endef

#define Build/Compile
#        $(MAKE) \
#                $(KERNEL_MAKE_FLAGS) \
#                M="$(PKG_BUILD_DIR)" \
#                EXTRA_CFLAGS="$(BUILDFLAGS)"
#endef

define Build/Compile

	$(TARGET_CC) -O3 -fno-stack-protector -flto -std=gnu90 -Wall -Wextra -c -o $(PKG_BUILD_DIR)/eoipcr.o $(PKG_BUILD_DIR)/eoipcr.c
	$(TARGET_CC) -O3 -fno-stack-protector -flto -std=gnu90 -Wall -Wextra -c -o $(PKG_BUILD_DIR)/libnetlink.o $(PKG_BUILD_DIR)/libnetlink.c
	$(TARGET_CC) -o $(PKG_BUILD_DIR)/eoipcr $(PKG_BUILD_DIR)/eoipcr.o $(PKG_BUILD_DIR)/libnetlink.o -O3 -fno-stack-protector -flto

       # $(TARGET_CC) $(TARGET_CFLAGS) $(TARGET_CPPFLAGS) -Wall \
       #         -o $(PKG_BUILD_DIR)/eoipcr $(PKG_BUILD_DIR)/eoipcr.c $(TARGET_LDFLAGS)

#eoipcr: eoipcr.o libnetlink.o
#	$(E) LD $@
#	$(Q)$(CC) -o $@ $^ $(MYLDFLAGS)
#
#libnetlink.o: libnetlink.c libnetlink.h
#	$(E) CC $@
#	$(Q)$(CC) $(MYCFLAGS) -c -o $@ $<
#
#eoipcr.o: eoipcr.c libnetlink.h version.h
#	$(E) CC $@
#	$(Q)$(CC) $(MYCFLAGS) -c -o $@ $<
#
#install: $(TARGET)
#	$(E) STRIP $(TARGET)
#	$(Q)$(STRIP) $(TARGET)
#	$(E) INSTALL $(TARGET)
#	$(Q)install -TD -m 0755 $(TARGET) $(PREFIX)sbin/$(TARGET)

#uninstall:
#	$(E) UNINSTALL $(TARGET)
#	$(Q)rm $(PREFIX)sbin/$(TARGET)
#
#clean:
#	rm -f eoipcr eoipcr.o libnetlink.o

#		$(TARGET_CC) $(TARGET_CFLAGS) -o $(PKG_BUILD_DIR)/eoipcr.o -c $(PKG_BUILD_DIR)/eoipcr.c
#		$(TARGET_CC) $(TARGET_LDFLAGS) -o $(PKG_BUILD_DIR)/$1 $(PKG_BUILD_DIR)/eoipcr.o
endef

define Package/eoipcr/install
	$(INSTALL_DIR) $(1)/sbin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/eoipcr $(1)/sbin/
endef

$(eval $(call BuildPackage,eoipcr))
