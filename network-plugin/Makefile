include $(TOPDIR)/rules.mk

PKG_NAME:=network-plugin
PKG_RELEASE:=4
PKG_VERSION:=2.0.0

PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=https://github.com/sartura/network-plugin.git
PKG_SOURCE_VERSION:=f7a8ab025be6b84c74b3ed1b4a98ba071f354377
PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION)-$(PKG_SOURCE_VERSION).tar.xz
PKG_SOURCE_SUBDIR:=$(PKG_NAME)-$(PKG_VERSION)-$(PKG_SOURCE_VERSION)

PKG_BUILD_ROOT:=$(BUILD_DIR)/$(PKG_SOURCE_SUBDIR)
PKG_BUILD_DIR:=$(PKG_BUILD_ROOT)


PKG_MAINTAINER:=Luka Paulic <luka.paulic@sartura.hr>

PKG_BUILD_PARALLEL:=1

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/cmake.mk

define Package/$(PKG_NAME)
  SECTION:=Terastream
  CATEGORY:=Terastream
  TITLE:=network plugin
  DEPENDS:= +sysrepo +libuci +sysrepoctl +libubus +libblobmsg-json +libjson-c +srpo
endef

define Package/$(PKG_NAME)/description
	Sysrepo network plugin
endef

CMAKE_OPTIONS:= \
	-DCMAKE_INSTALL_PREFIX=/usr \
	-DPLUGIN:BOLL=TRUE

define Package/$(PKG_NAME)/install
	$(INSTALL_DIR) $(1)/usr/lib/sysrepo/plugins/
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/lib/sysrepo-plugin-dt-network.so $(1)/usr/lib/sysrepo/plugins/

	$(INSTALL_DIR) $(1)/etc/sysrepo/yang
	$(INSTALL_DATA) $(PKG_BUILD_DIR)/yang/iana-if-type@2014-05-08.yang $(1)/etc/sysrepo/yang/
	$(INSTALL_DATA) $(PKG_BUILD_DIR)/yang/ietf-interfaces@2014-05-08.yang $(1)/etc/sysrepo/yang/
	$(INSTALL_DATA) $(PKG_BUILD_DIR)/yang/ietf-ip@2014-06-16.yang $(1)/etc/sysrepo/yang/
	$(INSTALL_DATA) $(PKG_BUILD_DIR)/yang/terastream-interfaces-opto@2017-09-27.yang $(1)/etc/sysrepo/yang/
	$(INSTALL_DIR) $(1)/etc/uci-defaults
	$(INSTALL_BIN) ./files/terastream.default $(1)/etc/uci-defaults/99_network
endef

$(eval $(call BuildPackage,$(PKG_NAME)))
