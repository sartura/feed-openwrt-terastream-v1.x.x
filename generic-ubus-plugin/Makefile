include $(TOPDIR)/rules.mk

PKG_NAME:=generic-ubus-plugin
PKG_RELEASE:=3
PKG_VERSION:=2.0.0

PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=https://github.com/sartura/generic-ubus-plugin
PKG_SOURCE_VERSION:=12186e35e4f1d20a2fe4f736915b0177fb6c5f96
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
  TITLE:=generic ubus plugin
  DEPENDS:= +sysrepo +sysrepoctl +libubus +libubox +libblobmsg-json +generic-ubus-yang-modules +srpo
endef

define Package/$(PKG_NAME)/description
	Sysrepo generic ubus plugin
endef

CMAKE_OPTIONS:= \
	-DCMAKE_INSTALL_PREFIX=/usr \
	-DPLUGIN:BOLL=TRUE \

define Package/$(PKG_NAME)/install
	$(INSTALL_DIR) $(1)/usr/lib/sysrepo/plugins/
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/lib/sysrepo-plugin-dt-generic-ubus.so $(1)/usr/lib/sysrepo/plugins/

	$(INSTALL_DIR) $(1)/etc/sysrepo/yang
	$(INSTALL_DATA) $(PKG_BUILD_DIR)/yang/terastream-generic-ubus@2019-06-28.yang $(1)/etc/sysrepo/yang/

	$(INSTALL_DIR) $(1)/etc/uci-defaults
	$(INSTALL_BIN) ./files/generic-ubus.default $(1)/etc/uci-defaults/99_generic_ubus
endef

$(eval $(call BuildPackage,$(PKG_NAME)))
