include $(TOPDIR)/rules.mk

PKG_NAME:=ola
PKG_VERSION:=0.10.2
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=https://github.com/OpenLightingProject/ola/releases/download/$(PKG_VERSION)
PKG_FIXUP:=libtool
PKG_INSTALL:=1

PKG_BUILD_PARALLEL:=1

PKG_BUILD_DEPENDS:=protobuf

include $(INCLUDE_DIR)/package.mk

define Package/ola
  SECTION:=multimedia
  CATEGORY:=Multimedia
  TITLE:=Open Lighting Architecture
  URL:=http://openlighting.org
  DEPENDS:=+libartnet +protobuf +libmicrohttpd +libusb-1.0 +libuuid +libstdcpp +libpthread +librt +zlib +libncurses
endef

define Package/ola/description
  The Open Lighting Architecture is a framework for lighting control information.
  It supports a range of protocols and over a dozen USB devices. It can run as
  a standalone service, which is useful for converting signals between protocols,
  or alternatively using the OLA API, it can be used as the backend for lighting
  control software. OLA runs on many different platforms including ARM,
  which makes it a perfect fit for low cost Ethernet to DMX gateways.
endef

define Build/Configure
  $(call Build/Configure/Default,--disable-dependency-tracking --disable-static --disable-root-check --disable-fatal-warnings --disable-unittests)
endef

define Build/InstallDev
	mkdir -p $(1)/usr/include
	$(CP) $(PKG_INSTALL_DIR)/usr/include/ola $(1)/usr/include/
	mkdir -p $(1)/usr/include
	$(CP) $(PKG_INSTALL_DIR)/usr/include/olad $(1)/usr/include/
	mkdir -p $(1)/usr/lib
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/*.so* $(1)/usr/lib/
endef

define Package/ola/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(CP) $(PKG_INSTALL_DIR)/usr/bin/* $(1)/usr/bin
	$(INSTALL_DIR) $(1)/usr/lib/olad
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/*.so* $(1)/usr/lib
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/olad/*.so* $(1)/usr/lib/olad
	$(INSTALL_DIR) $(1)/usr/share/olad/www
	$(CP) $(PKG_INSTALL_DIR)/usr/share/olad $(1)/usr/share
	$(INSTALL_DIR) $(1)/etc/init.d
	$(INSTALL_BIN) ./files/etc/init.d/olad $(1)/etc/init.d/olad
endef

$(eval $(call BuildPackage,ola))
