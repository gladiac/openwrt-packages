#
# Copyright (C) 2006-2015 OpenWrt.org
# Copyright (C) 2019 Christian Lachner <gladiac@gmail.com>
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=modsecurity
PKG_VERSION:=v3.0.3
PKG_RELEASE:=1

PKG_SOURCE:=modsecurity-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=https://github.com/SpiderLabs/ModSecurity/releases/download/$(PKG_VERSION)
PKG_HASH:=8aa1300105d8cc23315a5e54421192bc617a66246ad004bd89e67c232208d0f4
PKG_MAINTAINER:=Christian Lachner <gladiac@gmail.com>

PKG_LICENSE:=Apache-2.0
PKG_LICENSE_FILES:=LICENCE
PKG_CPE_ID:=cpe:/a:modsecurity:modsecurity

#PKG_FIXUP:=configure

PKG_INSTALL:=1

#PKG_CONFIG_DEPENDS:=\
#	CONFIG_PACKAGE_libpcrecpp \
#	CONFIG_PCRE_JIT_ENABLED

#include $(INCLUDE_DIR)/uclibc++.mk
include $(INCLUDE_DIR)/package.mk

define Package/modsecurity
  SECTION:=libs
  CATEGORY:=Libraries
  URL:=https://www.modsecurity.org/
  TITLE:=An open source, cross platform web application firewall (WAF) engine
  DEPENDS+= +libcurl +liblua5.3 +libpcre +libpthread +libstdcpp +libxml2
endef

TARGET_CFLAGS += $(FPIC)
TARGET_CXXFLAGS += $(FPIC)

CONFIGURE_ARGS += \
	--with-pic \
	--disable-doxygen-doc \
	--with-curl=no \
	--with-lua=no \
#	--with-pcre \
	--with-libxml=no

#	$(if $(CONFIG_PCRE_JIT_ENABLED),--enable-jit,--disable-jit) \
#	--with-match-limit-recursion=16000 \
#	$(if $(CONFIG_PACKAGE_libpcrecpp),--enable,--disable)-cpp

MAKE_FLAGS += \
	CFLAGS="$(TARGET_CFLAGS)" \
	CXXFLAGS="$(TARGET_CXXFLAGS)"

define Build/InstallDev
#	$(INSTALL_DIR) $(1)/usr/bin
#	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/bin/pcre-config $(1)/usr/bin/

#	$(INSTALL_DIR) $(2)/bin
#	$(LN) $(STAGING_DIR)/usr/bin/pcre-config $(2)/bin

#	$(INSTALL_DIR) $(1)/usr/include
#	$(CP) $(PKG_INSTALL_DIR)/usr/include/pcre*.h $(1)/usr/include/

#	$(INSTALL_DIR) $(1)/usr/lib
#	$(CP) $(PKG_INSTALL_DIR)/usr/lib/libpcre*.{a,so*} $(1)/usr/lib/

#	$(INSTALL_DIR) $(1)/usr/lib/pkgconfig
#	$(CP) $(PKG_INSTALL_DIR)/usr/lib/pkgconfig/libpcre*.pc $(1)/usr/lib/pkgconfig/
endef

define Package/modsecurity/install
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/libmodsecurity.so $(1)/usr/lib/
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/libmodsecurity.so.* $(1)/usr/lib/
endef

$(eval $(call BuildPackage,modsecurity))
