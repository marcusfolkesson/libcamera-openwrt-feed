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

PKG_BUILD_DEPENDS:= \
	python3/host \
	python-jinja2/host \
	python-ply/host \
	python-yaml/host \
	openssl

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/meson.mk


define Package/libcamera/config
  source "$(SOURCE)/Config.in"
endef

define Package/libcamera/default
	SECTION:=libs
	CATEGORY:=Multimedia
	DEPENDS:=+libyaml +libgnutls +libstdcpp \
		PACKAGE_gstreamer1:gstreamer1
	TITLE:=libcamera
	URL:=https://libcamera.org/
endef

define Package/libcamera
	$(call Package/libcamera/default)
endef

define Package/libcamera/description
	libcamera provides a software stack to support
	complex devices that need heavy hardware image
	processing operations.

	http://www.libcamera.org/
endef

ifeq ($(CONFIG_LIBCAMERA_PIPELINE_IMX8_ISI),y)
	LIBCAMERA_PIPELINES += imx8-isi
endif
ifeq ($(CONFIG_LIBCAMERA_PIPELINE_IPU3),y)
	LIBCAMERA_PIPELINES += ipu3
endif
ifeq ($(CONFIG_LIBCAMERA_PIPELINE_RKISP1),y)
	LIBCAMERA_PIPELINES += rkisp1
endif
ifeq ($(CONFIG_LIBCAMERA_PIPELINE_RPI_VC4),y)
	LIBCAMERA_PIPELINES += rpi/vc4
endif
ifeq ($(CONFIG_LIBCAMERA_PIPELINE_SIMPLE),y)
	LIBCAMERA_PIPELINES += simple
endif
ifeq ($(CONFIG_LIBCAMERA_PIPELINE_VIMC),y)
	LIBCAMERA_PIPELINES += vimc
endif
MESON_ARGS += -Dpipelines=$(subst $(space),$(comma),$(LIBCAMERA_PIPELINES))

ifeq ($(CONFIG_LIBCAMERA_V4L2),y)
	MESON_ARGS += -Dv4l2=true
endif

ifeq ($(CONFIG_PACKAGE_gstreamer),y)
	LIBCAMERA_CONF_OPTS += -Dgstreamer=enabled
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
	$(INSTALL_DIR) $(1)/usr/share/libcamera
	$(CP) $(PKG_INSTALL_DIR)/usr/share/libcamera/* $(1)/usr/share/libcamera/
	$(INSTALL_DIR) $(1)/usr/libexec/libcamera
	$(CP) $(PKG_INSTALL_DIR)/usr/libexec/libcamera/* $(1)/usr/libexec/libcamera/
	$(INSTALL_DIR) $(1)/usr/share/libcamera/ipa
	$(CP) $(PKG_INSTALL_DIR)/usr/share/libcamera/ipa/* $(1)/usr/share/libcamera/ipa/
	$(INSTALL_DIR) $(1)/usr/share/libcamera/ipa
	$(CP) $(PKG_INSTALL_DIR)/usr/share/libcamera/ipa/* $(1)/usr/share/libcamera/ipa/
endef

$(eval $(call BuildPackage,libcamera))
