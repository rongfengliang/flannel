IPERF_IMG ?= iperf3:latest

ARCH ?= amd64

TEMP_DIR := $(shell mktemp -d)

ifeq ($(ARCH),amd64)
        BASEIMAGE=amd64/alpine:3.16
endif
ifeq ($(ARCH),arm64)
	BASEIMAGE=arm64v8/alpine:3.16
endif
ifeq ($(ARCH),ppc64le)
	BASEIMAGE=ppc64le/alpine:3.16
endif

all: container

container:
	cp ./* $(TEMP_DIR)
	cd $(TEMP_DIR) && sed -i 's|BASEIMAGE|$(BASEIMAGE)|g' Dockerfile
	docker build --pull -t $(IPERF_IMG) -f $(TEMP_DIR)/Dockerfile $(TEMP_DIR)
