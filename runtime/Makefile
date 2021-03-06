# Copyright (c) 2017-2018, NVIDIA CORPORATION. All rights reserved.

DOCKER ?= docker
MKDIR  ?= mkdir

VERSION := 3.1.0
PKG_REV := 1

DIST_DIR  := $(CURDIR)/../dist

.NOTPARALLEL:
.PHONY: all

all: ubuntu18.04 ubuntu16.04 debian9 centos7 amzn2 amzn1

ubuntu%: ARCH := amd64
ubuntu%:
	$(DOCKER) build --build-arg VERSION_ID="$*" \
                        --build-arg PKG_VERS="$(VERSION)" \
			--build-arg PKG_REV="$(PKG_REV)" \
                        -t "nvidia/runtime/ubuntu:$*" -f Dockerfile.ubuntu .
	$(MKDIR) -p "$(DIST_DIR)/ubuntu$*/$(ARCH)"
	$(DOCKER) run --cidfile $@.cid "nvidia/runtime/ubuntu:$*"
	$(DOCKER) cp $$(cat $@.cid):/dist/. "$(DIST_DIR)/ubuntu$*/$(ARCH)/"
	$(DOCKER) rm $$(cat $@.cid) && rm $@.cid

debian%: ARCH := amd64
debian%:
	$(DOCKER) build --build-arg VERSION_ID="$*" \
                        --build-arg PKG_VERS="$(VERSION)" \
			--build-arg PKG_REV="$(PKG_REV)" \
                        -t "nvidia/runtime/debian:$*" -f Dockerfile.debian .
	$(MKDIR) -p "$(DIST_DIR)/debian$*/$(ARCH)"
	$(DOCKER) run --cidfile $@.cid "nvidia/runtime/debian:$*"
	$(DOCKER) cp $$(cat $@.cid):/dist/. "$(DIST_DIR)/debian$*/$(ARCH)/"
	$(DOCKER) rm $$(cat $@.cid) && rm $@.cid

centos%: ARCH := x86_64
centos%:
	$(DOCKER) build --build-arg VERSION_ID="$*" \
                        --build-arg PKG_VERS="$(VERSION)" \
			--build-arg PKG_REV="$(PKG_REV)" \
                        -t "nvidia/runtime/centos:$*" -f Dockerfile.centos .
	$(MKDIR) -p "$(DIST_DIR)/centos$*/$(ARCH)"
	$(DOCKER) run --cidfile $@.cid "nvidia/runtime/centos:$*"
	$(DOCKER) cp $$(cat $@.cid):/dist/. "$(DIST_DIR)/centos$*/$(ARCH)/"
	$(DOCKER) rm $$(cat $@.cid) && rm $@.cid

amzn%: ARCH := x86_64
amzn%:
	$(DOCKER) build --build-arg VERSION_ID="$*" \
                        --build-arg PKG_VERS="$(VERSION)" \
			--build-arg PKG_REV="$(PKG_REV)" \
                        -t "nvidia/runtime/amzn:$*" -f Dockerfile.amzn .
	$(MKDIR) -p "$(DIST_DIR)/amzn$*/$(ARCH)"
	$(DOCKER) run --cidfile $@.cid "nvidia/runtime/amzn:$*"
	$(DOCKER) cp $$(cat $@.cid):/dist/. "$(DIST_DIR)/amzn$*/$(ARCH)/"
	$(DOCKER) rm $$(cat $@.cid) && rm $@.cid
