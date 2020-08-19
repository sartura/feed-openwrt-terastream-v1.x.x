include $(TOPDIR)/rules.mk

PKG_NAME:=sip-plugin
PKG_RELEASE:=4
PKG_VERSION:=2.0.0

PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=https://github.com/sartura/sip-plugin.git
PKG_SOURCE_VERSION:=122f6f4f88cd8a76553d6adca64d8f6fe8bfa71b
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
  TITLE:=sip plugin
  DEPENDS:= +sysrepo +libuci +sysrepoctl +libubus +libubox +libblobmsg-json +voice-client +srpo
endef

define Package/sip-plugin/description
	Sysrepo sip plugin
endef

CMAKE_OPTIONS:= \
	-DCMAKE_INSTALL_PREFIX=/usr \
	-DPLUGIN:BOOL=TRUE

define Package/$(PKG_NAME)/install
	$(INSTALL_DIR) $(1)/usr/lib/sysrepo/plugins/
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/lib/sysrepo-plugin-dt-sip.so $(1)/usr/lib/sysrepo/plugins/

	$(INSTALL_DIR) $(1)/etc/sysrepo/yang
	$(INSTALL_DATA) $(PKG_BUILD_DIR)/yang/terastream-sip@2017-08-09.yang $(1)/etc/sysrepo/yang/

	$(INSTALL_DIR) $(1)/etc/uci-defaults
	$(INSTALL_BIN) ./files/sip.default $(1)/etc/uci-defaults/99_sip

	$(INSTALL_DIR) $(1)/etc/sysrepo/scripts/sip
	$(INSTALL_BIN) ./files/secret.sh $(1)/etc/sysrepo/scripts/sip
endef

$(eval $(call BuildPackage,$(PKG_NAME)))
