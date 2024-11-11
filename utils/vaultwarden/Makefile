# SPDX-License-Identifier: AGPL-3.0-only
#
# Copyright (C) 2023 Christian Lachner

include $(TOPDIR)/rules.mk

PKG_NAME:=vaultwarden
PKG_VERSION:=1.32.4
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=https://codeload.github.com/dani-garcia/vaultwarden/tar.gz/$(PKG_VERSION)?
PKG_HASH:=7cf9a5c7356df42b0da318a446bf576c2aa340581ec4c729f1cb616754cf66ad

PKG_MAINTAINER:=Christian Lachner <gladiac@gmail.com>
PKG_LICENSE:=AGPL-3.0-only
PKG_LICENSE_FILES:=LICENSE.txt

PKG_BUILD_DEPENDS:=rust/host
PKG_BUILD_PARALLEL:=1

CARGO_RUSTFLAGS:=-Cstrip=symbols
CARGO_RUSTFLAGS+=-Cpanic="abort"
RUST_PKG_FEATURES:=sqlite

export VW_VERSION=$(PKG_VERSION)-$(PKG_RELEASE)

include $(INCLUDE_DIR)/package.mk
include ../../lang/rust/rust-package.mk

define Package/vaultwarden
  SECTION:=utils
  CATEGORY:=Utilities
  TITLE:=vaultwarden - Unofficial Bitwarden compatible server written in Rust
  DEPENDS:=$(RUST_ARCH_DEPENDS) +libopenssl
  URL:=https://github.com/dani-garcia/vaultwarden
endef

define Package/vaultwarden/description
  Alternative implementation of the Bitwarden server API written in Rust and
  compatible with upstream Bitwarden clients, perfect for self-hosted
  deployment where running the official resource-heavy service might not be
  ideal.
endef

define Package/vaultwarden/conffiles
/etc/vaultwarden/.env
/etc/vaultwarden/data/
endef

define Package/vaultwarden/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/bin/vaultwarden $(1)/usr/bin/
	$(INSTALL_DIR) $(1)/etc/vaultwarden/data
	$(INSTALL_CONF) ./files/vaultwarden.env $(1)/etc/vaultwarden/.env
	$(INSTALL_DIR) $(1)/etc/init.d
	$(INSTALL_BIN) ./files/vaultwarden.init $(1)/etc/init.d/vaultwarden
endef

$(eval $(call RustBinPackage,vaultwarden))
$(eval $(call BuildPackage,vaultwarden))
