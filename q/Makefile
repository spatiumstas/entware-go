# SPDX-License-Identifier: GPL-2.0-only
#
# Copyright (C) 2025 Entware

# https://github.com/Entware/Entware/issues/1128

include $(TOPDIR)/rules.mk

PKG_NAME:=q
PKG_VERSION:=0.19.5
PKG_RELEASE:=1

PKG_SOURCE_PROTO:=git
PKG_SOURCE_DATE:=2025-07-07
PKG_SOURCE_VERSION:=6be15521947155e80f47a4eb88b850de57ecd596
PKG_SOURCE_URL:=https://github.com/natesales/q
PKG_MIRROR_HASH:=dfba4484eb05fa3164bf10f549c1acc9d1212f8416d2c46377fd11dd941c2e1e

PKG_MAINTAINER:=Entware team, https://entware.net
PKG_LICENSE:=GPL-3.0-only
PKG_LICENSE_FILES:=LICENSE

PKG_BUILD_PARALLEL:=1

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/golang.mk

define Package/q/Default
  SECTION:=net
  CATEGORY:=Network
  SUBMENU:=IP Addresses and Names
  TITLE:=command line DNS client
  URL:=https://github.com/natesales/q
endef

define Package/q
  $(call Package/q/Default)
  VARIANT:=hf
endef

define Package/q_nohf
  $(call Package/q/Default)
  VARIANT:=nohf
  DEPENDS:=@arm
endef

define Package/q/description
  A tiny CLI DNS client library with support for UDP, TCP, DoT, DoH,
 and DoQ.
endef

Package/q_nohf/description=$(Package/q/description)

GO_LDFLAGS += \
	-X 'main.version=$(PKG_VERSION)' \
	-X 'main.commit=$(COMMIT_SHORT)' \
	-X 'main.date=$(PKG_SOURCE_DATE)'

define Package/q/install
	$(INSTALL_DIR) $(1)/opt/sbin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/bin/q $(1)/opt/sbin
endef

Package/q_nohf/install=$(Package/q/install)

$(eval $(call BuildPackage,q))
$(eval $(call BuildPackage,q_nohf))
