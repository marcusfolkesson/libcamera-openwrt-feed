# libcamera OpenWRT feed

## Description

libcamera is an open source camera stack for many platforms with a core userspace library, and support from the Linux kernel APIs and drivers already in place.
It aims to control the complexity of embedded camera hardware by providing an intuitive API and method of separating untrusted vendor code from the open source core.

libcamera aims to encourage the development of new embedded camera applications by limiting the complexity that developers have to deal with.
The interface is designed around the way that modern embedded camera hardware works.

- [Website](https://libcamera.org/)

## Usage

This repository is intended to be layered on-top of an OpenWrt buildroot. If you do not have an OpenWrt buildroot installed, see the documentation at: [OpenWrt Buildroot – Installation](https://openwrt.org/docs/guide-developer/build-system/install-buildsystem) on the OpenWrt support site.

To install this feed and all its package definitions, run the following in your OpenWRT root-folder:
```
echo "src-git libcamera https://github.com/marcusfolkesson/libcamera-openwrt-feed.git" >> ./feeds.conf
./scripts/feeds update libcamera
./scripts/feeds install -a -p libcamera
```

# Patches

Please submit any patches against the libcamera-openwrt-feed repository via pull request.


