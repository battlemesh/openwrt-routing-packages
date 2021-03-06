#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=nodogsplash2
PKG_FIXUP:=autoreconf
PKG_VERSION:=2.0.1
PKG_RELEASE:=1

PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)-$(PKG_VERSION)/
PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=git://github.com/nodogsplash/nodogsplash.git
PKG_SOURCE_VERSION:=907f4e8c5a53868947ca547b0ebff5ae36fce7a8
PKG_MIRROR_HASH:=c54fccd5649b5c33873e14e8fa766c5ba24dd06fb1a2ed0bdceb1d86bd83295e
PKG_SOURCE_SUBDIR:=$(PKG_NAME)-$(PKG_VERSION)
PKG_MAINTAINER:=Moritz Warning <moritzwarning@web.de>
PKG_BUILD_PARALLEL:=1
PKG_LICENSE:=GPL-2.0+

include $(INCLUDE_DIR)/package.mk


define Package/nodogsplash2
	SUBMENU:=Captive Portals
	SECTION:=net
	CATEGORY:=Network
	DEPENDS:=+libpthread +iptables-mod-ipopt +libmicrohttpd-no-ssl
	TITLE:=Open public network gateway daemon
	URL:=https://github.com/nodogsplash/nodogsplash
	CONFLICTS:=nodogsplash
endef

define Package/nodogsplash2/description
	Nodogsplash offers a simple way to open a free hotspot providing
	restricted access to an internet connection.
endef

define Package/nodogsplash2/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/nodogsplash $(1)/usr/bin/
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/ndsctl $(1)/usr/bin/

	$(INSTALL_DIR) $(1)/etc/init.d
	$(INSTALL_BIN) files/nodogsplash.init $(1)/etc/init.d/nodogsplash
	$(INSTALL_DIR) $(1)/etc/config
	$(INSTALL_CONF) files/nodogsplash.config $(1)/etc/config/nodogsplash

	$(INSTALL_DIR) $(1)/etc/nodogsplash/htdocs/images
	$(CP) $(PKG_BUILD_DIR)/resources/splash.html $(1)/etc/nodogsplash/htdocs/
	$(CP) $(PKG_BUILD_DIR)/resources/infoskel.html $(1)/etc/nodogsplash/htdocs/
	$(CP) $(PKG_BUILD_DIR)/resources/splash.jpg $(1)/etc/nodogsplash/htdocs/images/
endef

define Package/nodogsplash2/postrm
#!/bin/sh
uci delete firewall.nodogsplash2
uci commit firewall
endef

define Package/nodogsplash2/conffiles
/etc/nodogsplash/nodogsplash.conf
endef

$(eval $(call BuildPackage,nodogsplash2))
