obj-m += rswap-client.o
rswap-client-y := rswap_client.o

ifeq ($(BACKEND),DRAM)
	rswap-client-y += rswap_dram.o
	rswap-client-y += rswap_dram_ops.o
else
	rswap-client-y += rswap_rdma_ops.o
	rswap-client-y += rswap_rdma.o
endif

RSWAP_ROOT_PATH := $(shell dirname $(abspath $(lastword $(MAKEFILE_LIST))))
ifneq ($(LINUXINCLUDE),)

LINUXINCLUDE :=                 \
	-I$(RSWAP_ROOT_PATH)/.. \
	$(LINUXINCLUDE)
else

KDIR ?= /lib/modules/`uname -r`/build

default:
	$(MAKE) -C $(KDIR) M=$(PWD) modules

clean:
	$(MAKE) -C $(KDIR) M=$$PWD clean
endif
