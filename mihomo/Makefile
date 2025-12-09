# SPDX-License-Identifier: GPL-2.0-only
#
# Copyright (C) 2025 Entware

include $(TOPDIR)/rules.mk

PKG_NAME:=mihomo
PKG_VERSION:=1.19.17
PKG_RELEASE:=1

PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=https://github.com/MetaCubeX/mihomo.git
PKG_SOURCE_VERSION:=v$(PKG_VERSION)
PKG_MIRROR_HASH:=27b0641d25b485cbff74f4cc6290adb3418e6a3e94e50137f59a8f62ddd1a27f

PKG_LICENSE:=MIT
PKG_LICENSE_FILES:=LICENSE

PKG_BUILD_PARALLEL:=1

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/golang.mk

define Package/mihomo/Default
	SECTION:=net
	CATEGORY:=Network
	SUBMENU:=Web Servers/Proxies
	TITLE:=Mihomo (MetaCubeX) universal proxy
	URL:=https://github.com/MetaCubeX/mihomo
	MAINTAINER:=Entware team, https://entware.net
	DEPENDS:=+ca-certificates
endef

define Package/mihomo
	$(call Package/mihomo/Default)
	VARIANT:=hf
endef

define Package/mihomo_nohf
	$(call Package/mihomo/Default)
	VARIANT:=nohf
	DEPENDS:=+ca-certificates @arm
endef

define Package/mihomo/description
Mihomo is a rule-based proxy platform written in Go.
endef

Package/mihomo_nohf/description=$(Package/mihomo/description)

define Package/mihomo/conffiles
/opt/etc/mihomo/config.yaml
endef

Package/mihomo_nohf/conffiles=$(Package/mihomo/conffiles)

XIMPORTPATH:=$(call tolower,$(XIMPORTPATH))

GO_LDFLAGS += \
	-X '$(XIMPORTPATH)/constant.Version=$(PKG_VERSION)'

GO_TARGET:=./

define Package/mihomo/install
	$(INSTALL_DIR) $(1)/opt/sbin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/bin/mihomo $(1)/opt/sbin/mihomo
	$(INSTALL_DIR) $(1)/opt/etc/init.d
	$(INSTALL_BIN) ./files/S99mihomo $(1)/opt/etc/init.d
	$(INSTALL_DIR) $(1)/opt/etc/mihomo
	$(INSTALL_CONF) ./files/config.yaml $(1)/opt/etc/mihomo
endef

Package/mihomo_nohf/install=$(Package/mihomo/install)

$(eval $(call BuildPackage,mihomo))
$(eval $(call BuildPackage,mihomo_nohf))
