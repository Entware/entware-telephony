#
# Copyright (C) 2014 - 2018 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=libosip2
PKG_VERSION:=5.3.0
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=@GNU/osip
PKG_HASH:=f4725916c22cf514969efb15c3c207233d64739383f7d42956038b78f6cae8c8

PKG_FIXUP:=autoreconf
PKG_INSTALL:=1
PKG_BUILD_PARALLEL:=1

PKG_LICENSE:=LGPL-2.1+
PKG_LICENSE_FILES:=COPYING

include $(INCLUDE_DIR)/package.mk

define Package/libosip2
  SUBMENU:=Telephony
  SECTION:=libs
  CATEGORY:=Libraries
  TITLE:=GNU oSIP library
  URL:=http://www.gnu.org/software/osip/
  ABI_VERSION:=15
  DEPENDS:=+librt
endef

define Package/libosip2/description
 GNU oSIP library, a Session Initiation Protocol (SIP) implementation.
endef

# toolchain __arc__ define conflicts with libosip2 source
TARGET_CFLAGS += $(if $(CONFIG_arc),-U__arc__)

CONFIGURE_ARGS += \
	--enable-shared \
	--enable-static \
	--disable-silent-rules \
	--disable-trace \
	--disable-mpatrol \
	--disable-gprof \
	--disable-mt \
	--enable-pthread \
	--enable-semaphore \
	--disable-gperf \
	--disable-test \
	--disable-minisize

define Build/InstallDev
	$(INSTALL_DIR) $(1)/opt/include
	$(CP) $(PKG_INSTALL_DIR)/opt/include/osip{,parser}2 $(1)/opt/include/

	$(INSTALL_DIR) $(1)/opt/lib
	$(CP) $(PKG_INSTALL_DIR)/opt/lib/libosip{,parser}2.{a,so*} $(1)/opt/lib/

	$(INSTALL_DIR) $(1)/opt/lib/pkgconfig
	$(CP) $(PKG_INSTALL_DIR)/opt/lib/pkgconfig/libosip2.pc $(1)/opt/lib/pkgconfig/
endef

define Package/libosip2/install
	$(INSTALL_DIR) $(1)/opt/lib
	$(CP) $(PKG_INSTALL_DIR)/opt/lib/libosip{,parser}2.so* $(1)/opt/lib/
endef

$(eval $(call BuildPackage,libosip2))
