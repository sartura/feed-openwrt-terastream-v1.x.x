include $(TOPDIR)/rules.mk

PKG_NAME:=dhcp-plugin
PKG_RELEASE:=4
PKG_VERSION:=2.0.0

PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=https://github.com/sartura/dhcp.git
PKG_SOURCE_VERSION:=2af7ad684aaf61ac037bbb43980cbf37b569d5da
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
  TITLE:=dhcp plugin
  DEPENDS:= +sysrepo +libyang +json-c +libuci +sysrepoctl +libubus +libubox +libblobmsg-json +srpo
endef

define Package/$(PKG_NAME)/description
	Sysrepo dhcp plugin
endef

CMAKE_OPTIONS:= \
	-DCMAKE_INSTALL_PREFIX=/usr \
	-DPLUGIN:BOLL=TRUE

define Package/$(PKG_NAME)/install
	$(INSTALL_DIR) $(1)/usr/lib/sysrepo/plugins/
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/lib/sysrepo-plugin-dt-dhcp.so $(1)/usr/lib/sysrepo/plugins/

	$(INSTALL_DIR) $(1)/etc/sysrepo/yang
	$(INSTALL_DATA) $(PKG_BUILD_DIR)/yang/terastream-dhcp@2017-12-07.yang $(1)/etc/sysrepo/yang/

	$(INSTALL_DIR) $(1)/etc/uci-defaults
	$(INSTALL_BIN) ./files/dhcp.default $(1)/etc/uci-defaults/99_dhcp
endef

$(eval $(call BuildPackage,$(PKG_NAME)))
