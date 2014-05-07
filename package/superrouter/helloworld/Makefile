#
# Copyright (C) 2007-2013 OpenWrt.org
# Copyright (C) 2010 Vertical Communications
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#
include $(TOPDIR)/rules.mk

PKG_NAME:=helloworld
PKG_VERSION:=1.0.0
PKG_RELEASE:=1

#PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.xz
#PKG_SOURCE_URL:=@SF/helloworld
PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)
#PKG_MD5SUM:=9b7dc52656f5cbec846a7ba3299f73bd
#PKG_CAT:=zcat

include $(INCLUDE_DIR)/package.mk

define Package/$(PKG_NAME)
	CATEGORY:=Super Router
	TITLE:=Hello World
	DEFAULT:=m
	MAINTAINER:=chenhui101@gmail.com
endef

define Package/$(PKG_NAME)/description
	This is a hello world package that contains a program to only print "hello world".
endef

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

define Package/$(PKG_NAME)/Compile
	$(MAKE) -C $(PKG_BUILD_DIR) helloworld
endef

# Specify where and how to install the program.
# The $(1) variable represents the root directory on the router running 
# OpenWrt. The $(INSTALL_DIR) variable contains a command to prepare the install 
# directory if it does not already exist.  Likewise $(INSTALL_BIN) contains the 
# command to copy the binary file from its current location (in our case the build
# directory) to the install directory.
define Package/$(PKG_NAME)/install
	$(INSTALL_DIR) $(1)/usr/sbin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/helloworld $(1)/usr/sbin/
endef

# This line executes the necessary commands to compile our program.
# The above define directives specify all the information needed, but this
# line calls BuildPackage which in turn actually uses this information to
# build a package.
$(eval $(call BuildPackage,$(PKG_NAME)))

