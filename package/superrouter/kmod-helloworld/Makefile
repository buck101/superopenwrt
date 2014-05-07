#
# Copyright (C) 2007-2013 OpenWrt.org
# Copyright (C) 2010 Vertical Communications
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#
include $(TOPDIR)/rules.mk
include $(INCLUDE_DIR)/kernel.mk

PKG_NAME:=helloworld
PKG_VERSION:=1.0.0
PKG_RELEASE:=1

#PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.xz
#PKG_SOURCE_URL:=@SF/helloworld
PKG_BUILD_DIR:=$(KERNEL_BUILD_DIR)/$(PKG_NAME)
#PKG_MD5SUM:=9b7dc52656f5cbec846a7ba3299f73bd
#PKG_CAT:=zcat

include $(INCLUDE_DIR)/package.mk

define KernelPackage/$(PKG_NAME)
	CATEGORY:=Super Router
	TITLE:=Kernel Hello World
	DEFAULT:=m
	FILES:=$(PKG_BUILD_DIR)/helloworld.$(LINUX_KMOD_SUFFIX)
	AUTOLOAD:=$(call AutoLoad,50,helloworld)
	MAINTAINER:=chenhui101@gmail.com
endef

define KernelPackage/$(PKG_NAME)/description
	This is a hello world package that contains a program to only print "hello world".
endef

EXTRA_KCONFIG:= \
	CONFIG_KMOD_HELLOWORLD=m

EXTRA_CFLAGS:= \
	$(patsubst CONFIG_%, -DCONFIG_%=1, $(patsubst %=m,%,$(filter %=m,$(EXTRA_KCONFIG)))) \
	$(patsubst CONFIG_%, -DCONFIG_%=1, $(patsubst %=y,%,$(filter %=y,$(EXTRA_KCONFIG)))) \

MAKE_OPTS:= \
	ARCH="$(LINUX_KARCH)" \
	CROSS_COMPILE="$(TARGET_CROSS)" \
	SUBDIRS="$(PKG_BUILD_DIR)" \
	EXTRA_CFLAGS="$(EXTRA_CFLAGS)" \
	$(EXTRA_KCONFIG)

# Specify what needs to be done to prepare for building the package.
# In our case, we need to copy the source files to the build directory.
# This is NOT the default.  The default uses the PKG_SOURCE_URL and the
# PKG_SOURCE which is not defined here to download the source from the web.
# In order to just build a simple program that we have just written, it is
# much easier to do it this way.
define Build/Prepare
	$(call Build/Prepare/Default)
	$(CP) -r files/. $(PKG_BUILD_DIR)

endef

define Build/Compile
	$(MAKE) -C "$(LINUX_DIR)" \
		$(MAKE_OPTS) \
		modules
endef
#
#define KernelPackage/$(PKG_NAME)/install
#	$(INSTALL_DIR) $(1)/usr/sbin
#	$(INSTALL_BIN) $(PKG_BUILD_DIR)/helloworld $(1)/usr/sbin/
#endef

# This line executes the necessary commands to compile our program.
# The above define directives specify all the information needed, but this
# line calls BuildPackage which in turn actually uses this information to
# build a package.
$(eval $(call KernelPackage,$(PKG_NAME)))

