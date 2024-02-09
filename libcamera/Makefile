# Copyright (C) 2024 Fusion CCTV, Inc.

include $(TOPDIR)/rules.mk

PKG_NAME:=libcamera
PKG_VERSION:=v0.2.0
PKG_RELEASE:=1

PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=https://git.linuxtv.org/libcamera.git
PKG_SOURCE_DATE:=2024-01-09
PKG_SOURCE_VERSION:=a3690f601bf9a90e1a936d9f361aebd789e3b073
PKG_MAINTAINER:= Marcus Folkesson <marcus.folkesson@gmail.com>
PKG_LICENSE:= \
	LGPL-2.1+ (library), \
	GPL-2.0+ (utils), \
	MIT (qcam/assets/feathericons), \
	BSD-2-Clause (raspberrypi), \
	GPL-2.0 with Linux-syscall-note or BSD-3-Clause (linux kernel headers), \
	CC0-1.0 (meson build system), \
	CC-BY-SA-4.0 (doc)

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/meson.mk

define Package/libcamera/default
  SECTION:=libs
  CATEGORY:=Multimedia
  DEPENDS:=+libyaml +libgnutls +libstdcpp
  TITLE:=libcamera
  URL:=https://libcamera.org/
endef

define Package/libcamera
  #$(call Package/libcamera/default)
endef

define Package/libcamera/description
  libcamera provides a software stack to support
  complex devices that need heavy hardware image
  processing operations.

  http://www.libcamera.org/
endef


define Package/libcamera-v4l2
   $(call Package/libcamera/default)
   TITLE+= v4l2 compatibility layer
endef

define Package/libcamera-pipeline-imx8-isi
   $(call Package/libcamera/default)
   TITLE+= imx8-isi pipeline
endef

define Package/libcamera-pipeline-imx8-isi/description
  Pipeline for i.MX8 SoC ISI capture interface
endef

define Package/libcamera-pipeline-ipu3
  $(call Package/libcamera/default)
  TITLE+= ipu3 pipeline
endef

define Package/libcamera-pipeline-ipu3/description
  Pipeline for Intel IPU3.
endef

define Package/libcamera-pipeline-rkisp1
  $(call Package/libcamera/default)
  TITLE+= rkisp1 pipeline
endef

define Package/libcamera-pipeline-rkisp1/description
  Pipeline for Rockchip ISP1.
endef

define Package/libcamera-pipeline-rpi-vc4
  $(call Package/libcamera/default)
  TITLE+= rpi/vc4 pipeline
  DEPENDS+= +boost
endef

define Package/libcamera-pipeline-rpi-vc4/description
  Pipeline for Raspberry Pi devices.
endef

define Package/libcamera-pipeline-simple
  $(call Package/libcamera/default)
  TITLE+= simple pipeline
endef

define Package/libcamera-pipeline-simple/description
  Pipeline for simple pipelines.
endef

define Package/libcamera-pipeline-uvcvideo
  $(call Package/libcamera/default)
  TITLE+= uvcvideo pipeline
endef

define Package/libcamera-pipeline-uvcvideo/description
  Pipeline for uvcvideo devices.
endef

define Package/libcamera-pipeline-vimc
  $(call Package/libcamera/default)
  TITLE+= vimc pipeline
endef

define Package/libcamera-pipeline-vimc/description
 Pieline for the vimc device.
endef

ifeq ($(CONFIG_PACKAGE_libcamera-pipeline-imx8-isi),y)
	LIBCAMERA_PIPELINES += imx8-isi
endif
ifeq ($(CONFIG_PACKAGE_libcamera-pipeline-ipu3),y)
	LIBCAMERA_PIPELINES += ipu3
endif
ifeq ($(CONFIG_PACKAGE_libcamera-pipeline-rkisp1),y)
	LIBCAMERA_PIPELINES += rkisp1
endif
ifeq ($(CONFIG_PACKAGE_libcamera-pipeline-rpi-vc4),y)
	LIBCAMERA_PIPELINES += rpi/vc4
endif
ifeq ($(CONFIG_PACKAGE_libcamera-pipeline-simple),y)
	LIBCAMERA_PIPELINES += simple
endif
ifeq ($(CONFIG_PACKAGE_libcamera-pipeline-vimc),y)
	LIBCAMERA_PIPELINES += vimc
endif
MESON_ARGS += -Dpipelines=$(subst $(space),$(comma),$(LIBCAMERA_PIPELINES))

ifeq ($(CONFIG_PACKAGE_libcamera-v4l2),y)
	MESON_ARGS += -Dv4l2=true
endif

ifeq ($(CONFIG_PACKAGE_gstreamer),y)
	LIBCAMERA_CONF_OPTS += -Dgstreamer=enabled
	LIBCAMERA_DEPENDENCIES += CONFIG_PACKAGE_gstreamer
endif

MESON_ARGS += \
	-Dgstreamer=$(if $(CONFIG_PACKAGE_libevent2),en,dis)abled \
	-Dandroid=disabled \
	-Ddocumentation=disabled \
	-Dtest=false \
	-Dpycamera=disabled \
	-Dwerror=false

define Build/InstallDev
  $(INSTALL_DIR) $(1)/usr/include
  $(CP) $(PKG_INSTALL_DIR)/usr/include/* $(1)/usr/include/
  $(INSTALL_DIR) $(1)/usr/lib
  $(CP) $(PKG_INSTALL_DIR)/usr/lib/lib*.so* $(1)/usr/lib/
  $(INSTALL_DIR) $(1)/usr/lib/pkgconfig
  $(CP) $(PKG_INSTALL_DIR)/usr/lib/pkgconfig/*.pc $(1)/usr/lib/pkgconfig
endef

define Package/libcamera/install
  $(INSTALL_DIR) $(1)/usr/lib
  $(CP) $(PKG_INSTALL_DIR)/usr/lib/lib*.so.* $(1)/usr/lib/
endef

Package/libcamera-v4l2/install = $(Package/libcamera/install)
Package/libcamera-pipeline-imx8-isi/install = $(Package/libcamera/install)
Package/libcamera-pipeline-ipu3/install = $(Package/libcamera/install)
Package/libcamera-pipeline-rkisp1/install = $(Package/libcamera/install)
Package/libcamera-pipeline-rpi-vc4/install = $(Package/libcamera/install)
Package/libcamera-pipeline-uvcvideo/install = $(Package/libcamera/install)
Package/libcamera-pipeline-vimc/install = $(Package/libcamera/install)

$(eval $(call BuildPackage,libcamera))
$(eval $(call BuildPackage,libcamera-v4l2))
$(eval $(call BuildPackage,libcamera-pipeline-imx8-isi))
$(eval $(call BuildPackage,libcamera-pipeline-ipu3))
$(eval $(call BuildPackage,libcamera-pipeline-rkisp1))
$(eval $(call BuildPackage,libcamera-pipeline-rpi-vc4))
$(eval $(call BuildPackage,libcamera-pipeline-simple))
$(eval $(call BuildPackage,libcamera-pipeline-uvcvideo))
$(eval $(call BuildPackage,libcamera-pipeline-vimc))
