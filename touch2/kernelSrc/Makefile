####################################################################

MODULE = optictouch

GCC = gcc

INCLUDE = -I include

C_FLAGS = -Wall -O -pipe $(INCLUDE)

####################################################################

ifneq ($(KERNELRELEASE),)
obj-m := $(MODULE).o
else
KVER ?= $(shell uname -r)
KDIR ?= /lib/modules/$(KVER)/build

PWD := $(shell pwd)

all:
	$(MAKE) -C $(KDIR) SUBDIRS=$(PWD) modules

new rebuild:	clean all

clean:
	rm -f $(MODULE).o $(MODULE).mod.o $(MODULE).ko $(MODULE).mod.c *.*~ *~ Module.* modules.*
endif
