# 
# Copyright (C) 2007-2011 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=polipo
PKG_VERSION:=1.0.5.2

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=git://github.com/jech/polipo.git
PKG_REV:=ec4d6385fa910cfd50ec099efee25d9e1d4eec23
PKG_SOURCE_SUBDIR:=$(PKG_NAME)-$(PKG_VERSION)
PKG_SOURCE_VERSION:=$(PKG_REV)

include $(INCLUDE_DIR)/package.mk

define Package/polipo
  SUBMENU:=Web Servers/Proxies
  SECTION:=net
  CATEGORY:=Network
  TITLE:=A caching web proxy
  URL:=http://www.pps.jussieu.fr/~jch/software/polipo/
  MAINTAINER:=Gabriel Kerneis <kerneis@pps.jussieu.fr>
endef

define Package/polipo/description
 Polipo is a small and fast caching web proxy (a web cache, an HTTP proxy, 
 a proxy server). While Polipo was designed to be used by one person or a 
 small group of people, there is nothing that prevents it from being used 
 by a larger group.
endef

define Build/Compile
	$(MAKE) -C $(PKG_BUILD_DIR) \
		CC="$(TARGET_CC)" \
		CFLAGS="$(TARGET_CFLAGS)" \
		polipo
endef

define Package/polipo/conffiles
/etc/config/polipo
/etc/polipo/config
endef

define Package/polipo/install
	$(INSTALL_DIR) $(1)/usr/sbin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/polipo $(1)/usr/sbin/
	$(INSTALL_DIR) $(1)/etc/polipo
	$(INSTALL_CONF) $(PKG_BUILD_DIR)/config.sample $(1)/etc/polipo/config
	$(INSTALL_DIR) $(1)/etc/config
	$(INSTALL_DATA) ./files/polipo.config $(1)/etc/config/polipo
	$(INSTALL_DIR) $(1)/etc/init.d
	$(INSTALL_BIN) ./files/polipo.init $(1)/etc/init.d/polipo
endef

$(eval $(call BuildPackage,polipo))
