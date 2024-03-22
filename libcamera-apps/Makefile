# Copyright (C) 2024 Fusion CCTV, Inc.

include $(TOPDIR)/rules.mk
include $(TOPDIR)/rules.mk

PKG_NAME:=libcamera-apps
PKG_VERSION:=1.2.1
PKG_RELEASE:=1

PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=https://github.com/raspberrypi/rpicam-apps.git
PKG_SOURCE_DATE:=2024-01-09
PKG_SOURCE_VERSION:=7e4d3d71867f60f5398687180972798baad85f1b

PKG_MAINTAINER:=Marcus Folkesson <marcus.folkesson@gmail.com>
PKG_LICENSE:=BSD-2-Clause
PKG_LICENSE_FILES:=license.txt
PKG_BUILD_PARALLEL:=1

CMAKE_INSTALL:=1
PKG_USE_NINJA:=1
CMAKE_BINARY_SUBDIR:=build

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/cmake.mk

define Package/libcamera-apps
	SECTION:=multimedia
	CATEGORY:=Multimedia
	TITLE:=libcamera-apps
	URL:=https://github.com/raspberrypi/rpicam-apps.git
	DEPENDS:=+pkgconf +boost-program_options +libjpeg +libcamera +libexif +libpng +libtiff
endef


CMAKE_OPTIONS += -DENABLE_DRM=OFF
CMAKE_OPTIONS += -DENABLE_LIBAV=OFF
CMAKE_OPTIONS += -DENABLE_X11=OFF
CMAKE_OPTIONS += -DENABLE_QT=OFF
CMAKE_OPTIONS += -DENABLE_OPENCV=OFF
CMAKE_OPTIONS += -DENABLE_TFLITE=OFF

define Package/libcamera-apps/description
This is a small suite of libcamera-based applications to drive the cameras on a Raspberry Pi platform.
endef

define Package/libcamera-apps/install
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/lib*.so.* $(1)/usr/lib/
	$(INSTALL_DIR) $(1)/usr/bin
	$(CP) $(PKG_INSTALL_DIR)/usr/bin/libcamera-* $(1)/usr/bin/
endef

$(eval $(call BuildPackage,libcamera-apps))
