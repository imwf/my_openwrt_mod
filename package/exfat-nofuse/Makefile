#
# Copyright (C) 2008-2010 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk
include $(INCLUDE_DIR)/kernel.mk

PKG_NAME:=exfat-nofuse
PKG_VERSION:=1.2.5
PKG_RELEASE=$(PKG_SOURCE_VERSION)

PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=https://github.com/addison/exfat-nofuse
PKG_SOURCE_SUBDIR:=$(PKG_NAME)-$(PKG_VERSION)
PKG_SOURCE_VERSION:=42250d562293704a4b266fdb1ac4abd02289d922
PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION)-$(PKG_SOURCE_VERSION).tar.gz

include $(INCLUDE_DIR)/package.mk

define KernelPackage/fs-exfat
  SUBMENU:=Filesystems
  TITLE:=EXFAT filesystem support
  DEPENDS:=+kmod-nls-base
  FILES:= $(PKG_BUILD_DIR)/exfat.ko
  AUTOLOAD:=$(call AutoLoad,30,exfat,1)
endef

define KernelPackage/fs-exfat/description
  Kernel module to exfat native driver leak from Samsung
endef

MAKE_OPTS:= \
	ARCH="$(LINUX_KARCH)" \
	CROSS_COMPILE="$(TARGET_CROSS)" \
	SUBDIRS="$(PKG_BUILD_DIR)" \

define Build/Compile
	$(MAKE) -C "$(LINUX_DIR)" \
		$(MAKE_OPTS) \
		modules
endef

$(eval $(call KernelPackage,fs-exfat))