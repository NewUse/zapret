# Copyright Zapret
# This is free software, licensed under the GNU General Public License v2.

include $(TOPDIR)/rules.mk

PKG_NAME:=nfqws
PKG_VERSION:=1
PKG_RELEASE:=1

PKG_LICENSE:=GPL-2.0-or-later
PKG_MAINTAINER:=Zapret

include $(INCLUDE_DIR)/package.mk

define Package/nfqws
	SECTION:=net
	CATEGORY:=Network
	TITLE:=NFQWS DPI bypass proxy server
	SUBMENU:=Zapret
 	DEPENDS:=+zlib +libcap
endef

define Package/nfqws/description
DPI bypass proxy
endef

define Build/Prepare
	mkdir -p $(PKG_BUILD_DIR)
	$(CP) ./nfq/* $(PKG_BUILD_DIR)/
endef

define Build/Compile
	$(MAKE) -C $(PKG_BUILD_DIR) $(TARGET_CONFIGURE_OPTS)
endef

define Package/nfqws/conffiles
/etc/config/zapret
endef

define Package/tpws/install
	$(INSTALL_DIR) $(1)/etc/config
	$(INSTALL_DATA) ./files/zapret.conf $(1)/etc/config/zapret
	$(INSTALL_DIR) $(1)/etc/zapret/fake
	$(INSTALL_DATA) ./files/fake/* $(1)/etc/zapret/fake
	$(INSTALL_DIR) $(1)/etc/init.d
	$(INSTALL_BIN) ./files/zapret.init $(1)/etc/init.d/zapret
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/nfqws $(1)/usr/bin
endef

$(eval $(call BuildPackage,nfqws))
