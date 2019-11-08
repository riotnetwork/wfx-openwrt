# SPDX-License-Identifier: GPL-2.0


wfx-objs := \
	bh.o \
	hwio.o \
	fwio.o \
	data_rx.o \
	data_tx.o \
	main.o \
	queue.o \
	hif_tx.o \
	hif_rx.o \
	key.o \
	sta.o \
	scan.o \
	debug.o \
	bus_spi.o\
	bus_sdio.o \
	secure_link.o \
	mbedtls/library/aes.o \
	mbedtls/library/bignum.o \
	mbedtls/library/ccm.o \
	mbedtls/library/cipher.o \
	mbedtls/library/cipher_wrap.o \
	mbedtls/library/ecdh.o \
	mbedtls/library/ecp_curves.o \
	mbedtls/library/ecp.o \
	mbedtls/library/error.o \
	mbedtls/library/md.o \
	mbedtls/library/md_wrap.o \
	mbedtls/library/platform_util.o \
	mbedtls/library/sha256.o \
	mbedtls/library/sha512.o

CFLAGS_debug.o = -I$(src)
CFLAGS_sta.o += -DDEBUG

ccflags-y += \
	-I$(src)/mbedtls/include -DCONFIG_WFX_SECURE_LINK=y

ccflags-$(CONFIG_WF200_DEBUG) := -DDEBUG

obj-$(CONFIG_WFX) += wfx.o

