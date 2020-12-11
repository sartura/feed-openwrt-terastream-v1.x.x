include $(TOPDIR)/rules.mk

PKG_NAME:=srpo
PKG_RELEASE:=1
PKG_VERSION:=1.0.0

PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=https://github.com/sartura/srpo.git
PKG_SOURCE_VERSION:=93d0b7ba447564ddf6bae5f887cfee2dbd512af8
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
  TITLE:=srpo library
  DEPENDS:= +sysrepo +libuci2 +libubus +libubox +libblobmsg-json
endef

define Package/$(PKG_NAME)/description
	Sysrepo plugin Openwrt library for wrapping UCI and UBUS data operations.
endef

CMAKE_OPTIONS:= \
	-DCMAKE_INSTALL_PREFIX=/usr

define Build/InstallDev
	$(INSTALL_DIR) $(1)/usr/lib
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/lib/libsrpo.so $(1)/usr/lib/

	$(INSTALL_DIR) $(1)/usr/include
	$(CP) $(PKG_INSTALL_DIR)/usr/include/srpo_ubus.h $(1)/usr/include
	$(CP) $(PKG_INSTALL_DIR)/usr/include/srpo_uci.h $(1)/usr/include
endef

define Package/$(PKG_NAME)/install
	$(INSTALL_DIR) $(1)/usr/lib
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/lib/libsrpo.so $(1)/usr/lib
endef

$(eval $(call BuildPackage,$(PKG_NAME)))
