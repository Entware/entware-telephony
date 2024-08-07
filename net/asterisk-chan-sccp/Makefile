#
# Copyright (C) 2016 OpenWrt.org
# Copyright (C) 2016 Cesnet, z.s.p.o.
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=asterisk-chan-sccp
PKG_RELEASE:=2

# Updated to v4.3.3 release
PKG_SOURCE_URL:=https://github.com/chan-sccp/chan-sccp.git
PKG_SOURCE_VERSION:=968caa458920965c5dd15c31bcd50d21a891ab20
PKG_SOURCE_DATE:=2020-12-19
PKG_MIRROR_HASH:=705cd1cd30fc5db3143f87077e2c6511aaa463e1e160ad161a23ccd978fde24e
PKG_SOURCE_PROTO:=git

PKG_FIXUP:=autoreconf

PKG_LICENSE:=GPL-1.0
PKG_LICENSE_FILES:=COPYING LICENSE
PKG_MAINTAINER:=Jiri Slachta <jiri@slachta.eu>

PKG_INSTALL:=1

# need iconv.m4, otherwise error during autoreconf
PKG_BUILD_DEPENDS:=gettext-full

include $(INCLUDE_DIR)/package.mk
# chan-sccp needs iconv
include $(INCLUDE_DIR)/nls.mk

define Package/asterisk-chan-sccp
  SUBMENU:=Telephony
  SECTION:=net
  CATEGORY:=Network
  TITLE:=SCCP channel support
  URL:=https://github.com/chan-sccp/chan-sccp
  DEPENDS:=asterisk $(ICONV_DEPENDS) +libltdl \
	  +asterisk-bridge-holding \
	  +asterisk-bridge-native-rtp \
	  +asterisk-bridge-simple \
	  +asterisk-bridge-softmix \
	  +asterisk-res-stasis-device-state
  CONFLICTS:=asterisk-chan-skinny
endef

define Package/asterisk-chan-sccp/description
Replacement for the SCCP channel driver (chan_skinny) in Asterisk.
Extended features include shared lines, presence / BLF, customizable
feature buttons and custom device state.
endef

CONFIGURE_ARGS += \
	--disable-debug \
	--enable-advanced-functions \
	--enable-conference \
	--enable-video \
	--with-asterisk=$(STAGING_DIR)/opt

define Package/asterisk-chan-sccp/conffiles
/opt/etc/asterisk/sccp.conf
endef

define Package/asterisk-chan-sccp/install
	$(INSTALL_DIR) $(1)/opt/etc/asterisk
	$(INSTALL_DATA) $(PKG_INSTALL_DIR)/opt/etc/asterisk/sccp.conf $(1)/opt/etc/asterisk
	$(INSTALL_DIR) $(1)/opt/lib/asterisk/modules
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/opt/lib/asterisk/modules/chan_sccp.so $(1)/opt/lib/asterisk/modules/
endef

$(eval $(call BuildPackage,asterisk-chan-sccp))
