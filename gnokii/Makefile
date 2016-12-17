#
# Copyright (C) 2006-2010 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=gnokii
PKG_VERSION:=0.6.32-pre
PKG_RELEASE:=3

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_PROTO:=git
PKG_SOURCE_VERSION:=2ec97fb4a7019e6cb6ae98d60cc7dfa707dbe0bc
PKG_SOURCE_SUBDIR:=$(PKG_NAME)-$(PKG_VERSION)

PKG_SOURCE_URL:=http://git.savannah.gnu.org/cgit/gnokii.git
PKG_MD5SUM:=fb1c190fef70451ff96cb758559f9fea

PKG_FIXUP:=intltoolize
PKG_FIXUP:=autoreconf
#PKG_FIXUP:=libtoolize
#PKG_FIXUP:=glib-gettextize -f
#PKG_FIXUP:=intltoolize --force --copy --automake
#PKG_FIXUP:=aclocal -I m4
#PKG_FIXUP:=autoheader -I m4
#PKG_FIXUP:=automake --add-missing
#PKG_FIXUP:=autoconf
CONFIGURE_CMD =./autogen.sh
#PKG_FIXUP:=autogen.sh

PKG_INSTALL:=1
PKG_BUILD_PARALLEL:=0

include $(INCLUDE_DIR)/package.mk

define Package/gnokii
  SECTION:=utils
  CATEGORY:=Utilities
  DEPENDS:=+libusb-compat +glib2 +libpq
  TITLE:=Gnokii - Datasuite for the mobile phones
  URL:=http://www.gnokii.org/
endef

define Package/gnokii/description
	Gnokii is a suite of programs linked against a backend
	library that allows communication with the phones. It
	currently supports the most mobile phones, all AT
	capable mobiles as well as Symbian phones.
endef

define Build/Configure
	(cd $(PKG_BUILD_DIR); intltoolize --force ; autoreconf --install -v);
	$(call Build/Configure/Default, \
		--without-libiconv-prefix \
		--without-libintl-prefix \
		--without-readline \
		--disable-rlpdebug \
		--disable-xdebug \
		--enable-postgres=yes \
		--disable-static \
		--disable-debug \
		--enable-shared \
		--disable-libpcsclite \
		--disable-libical \
		--disable-irda \
		--disable-bluetooth \
		--disable-phonet \
		--without-x \
		PGCONFIG=/home/paul/openwrt/build_dir/target-mips_34kc_musl-1.1.15/host/postgresql-9.5.4/src/bin/pg_config/pg_config \
		)
#PGCONFIG=/home/paul/openwrt/build_dir/target-mips_34kc_uClibc-0.9.33.2/postgresql-9.4.4/src/bin/pg_config/pg_config.host \
#		PGCONFIG=/home/paul/openwrt/staging_dir/target-mips_34kc_uClibc-0.9.33.2/usr/bin/pg_config \


endef

define Package/gnokii/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_DIR) $(1)/usr/sbin
	$(INSTALL_DIR) $(1)/usr/lib
	$(INSTALL_DIR) $(1)/usr/lib/smsd
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/bin/gnokii $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/bin/gnokiid $(1)/usr/sbin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/bin/smsd $(1)/usr/sbin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/sbin/mgnokiidev $(1)/usr/sbin
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/libgnokii.so.7.0.0 $(1)/usr/lib
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/libgnokii.so.7 $(1)/usr/lib
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/smsd/libsmsd_file.so $(1)/usr/lib/smsd
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/smsd/libsmsd_pq.so $(1)/usr/lib/smsd
endef
$(eval $(call BuildPackage,gnokii))
