#
# Copyright (C) 2017 OpenWrt.org
# Copyright (C) 2017 Jiri Slachta <jiri@slachta.eu>
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#
include $(TOPDIR)/rules.mk

PKG_NAME:=libsrtp
PKG_VERSION:=2.4.2
PKG_RELEASE:=2

PKG_SOURCE:=libsrtp-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=https://codeload.github.com/cisco/libsrtp/tar.gz/v$(PKG_VERSION)?
PKG_HASH:=3b1bcb14ebda572b04b9bdf07574a449c84cb924905414e4d94e62837d22b628

PKG_LICENSE:=BSD-3-Clause
PKG_LICENSE_FILES:=LICENSE
PKG_MAINTAINER:=Jiri Slachta <jiri@slachta.eu>

include $(INCLUDE_DIR)/package.mk

CONFIGURE_ARGS+=--enable-openssl

define Package/libsrtp2
  SUBMENU:=Telephony
  SECTION:=libs
  CATEGORY:=Libraries
  TITLE:=Secure RTP (SRTP) library, v$(PKG_VERSION)
  URL:=https://github.com/cisco/libsrtp
  DEPENDS:=+libopenssl
  ABI_VERSION:=1
endef

define Package/libsrtp2/description
Open-source implementation of the Secure Real-time Transport
Protocol (SRTP) originally authored by Cisco Systems, Inc.
It is available under a BSD-style license.
endef

define Build/Install
	$(call Build/Install/Default,all shared_library install)
endef

define Build/InstallDev
	$(INSTALL_DIR) $(1)/opt/include
	$(CP) $(PKG_INSTALL_DIR)/opt/include/srtp2 $(1)/opt/include/
	$(INSTALL_DIR) $(1)/opt/lib
	$(CP) $(PKG_INSTALL_DIR)/opt/lib/libsrtp2.{a,so*} $(1)/opt/lib/
	$(INSTALL_DIR) $(1)/opt/lib/pkgconfig
	$(CP) $(PKG_INSTALL_DIR)/opt/lib/pkgconfig/libsrtp2.pc $(1)/opt/lib/pkgconfig/
endef

define Package/libsrtp2/install
	$(INSTALL_DIR) $(1)/opt/lib
	$(CP) \
		$(PKG_INSTALL_DIR)/opt/lib/libsrtp2.so.* \
		$(1)/opt/lib/
endef

$(eval $(call BuildPackage,libsrtp2))
