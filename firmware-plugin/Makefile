include $(TOPDIR)/rules.mk

PKG_NAME:=firmware-plugin
PKG_RELEASE:=4
PKG_VERSION:=2.0.0

PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=https://github.com/sartura/firmware-plugin.git
PKG_SOURCE_VERSION:=3ae9770bbada9302b437cf26149f591f1711f34b
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
  TITLE:=firmware plugin
  DEPENDS:= +sysrepo +sysrepoctl +sysrepocfg +libopenssl +libcurl +libubox +libubus +libblobmsg-json +libjson-c +libyang +srpo
endef

define Package/$(PKG_NAME)/description
	Sysrepo firmware plugin
endef

CMAKE_OPTIONS:= \
	-DCMAKE_INSTALL_PREFIX=/usr \
	-DPLUGIN:BOLL=TRUE

define Package/$(PKG_NAME)/install
	$(INSTALL_DIR) $(1)/usr/lib/sysrepo/plugins/
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/lib/sysrepo-plugin-dt-firmware.so $(1)/usr/lib/sysrepo/plugins/

	$(INSTALL_DIR) $(1)/etc/sysrepo/yang
	$(INSTALL_DATA) $(PKG_BUILD_DIR)/yang/iana-crypt-hash@2014-08-06.yang $(1)/etc/sysrepo/yang/

	$(INSTALL_DIR) $(1)/etc/sysrepo/yang
	$(INSTALL_DATA) $(PKG_BUILD_DIR)/yang/ietf-netconf-acm@2018-02-14.yang $(1)/etc/sysrepo/yang/

	$(INSTALL_DIR) $(1)/etc/sysrepo/yang
	$(INSTALL_DATA) $(PKG_BUILD_DIR)/yang/ietf-system@2014-08-06.yang $(1)/etc/sysrepo/yang/

	$(INSTALL_DIR) $(1)/etc/sysrepo/yang
	$(INSTALL_DATA) $(PKG_BUILD_DIR)/yang/terastream-software@2017-11-01.yang $(1)/etc/sysrepo/yang/

	$(INSTALL_DIR) $(1)/etc/uci-defaults
	$(INSTALL_BIN) ./files/firmware.default $(1)/etc/uci-defaults/99_firmware
endef

$(eval $(call BuildPackage,$(PKG_NAME)))
