####################################################################

MODULE = OtdTouchDriver

GCC = gcc

INCLUDE = -I include

C_FLAGS = -Wall -O -pipe $(INCLUDE)

####################################################################

ifneq ($(KERNELRELEASE),)
obj-m := $(MODULE).o
else
KDIR := /lib/modules/$(shell uname -r)/build
PWD := $(shell pwd)

all:
	$(MAKE) -C $(KDIR) SUBDIRS=$(PWD) modules

new rebuild:	clean all

clean:
	rm -f *.o *.mod.o *.ko *.mod.c *.cmd *.*~ *~ Module.* modules.*
endif
