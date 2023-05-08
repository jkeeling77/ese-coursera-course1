#--------------------------------------------------------------
# Simple makefile for v3 demo
# 
# Use:
#   make [TARGET] [OVERRIDES]
#
# Build Targets:
#   <file>.o - Builds <file>.o object file
#   build    - Builds and linkes all source files
#   all      - Same as build
#   clean    - Removes all generated files
#
# Overides:
#   CPU      - ARM Cortex Architecture (cortex-m0plus, cortex-m4)
#   ARCH     - ARM Architecture (arm, thumb)
#   SPECS    - Specs files to give the linker (nosys.specs, nano.specs)
#   PLATFORM - [HOST || MSB432]
#--------------------------------------------------------------

ARCH  := $(shell arch)
UNAME := $(shell uname)
CWD   := $(shell pwd)
PLATFORM := HOST

CPU=cortex-m4

#ifndef PLATFORM
#   $(error "testing error")
#endif

#ifdef MSB 
#   PLATFORM := MSB
#else ifdef KL25Z
#   PLATFORM := LK25Z
#endif


CFLAGS := -Wall -v
ifeq ($(UNAME), Linux)
   CC=gcc
   CSTD=c99
   CFLAGS := $(CFLAGS) -std=$(CSTD)
   CFLAGS := $(CFLAGS) -D$(PLATFORM)
else
   CC=arm-none-eabi-gcc
   CSTD=c99
   CFLAGS := $(CFLAGS) -std=$(CSTD) --specs=nosys.specs --mcpu=$(CPU) -mthumb -march=arm7e-m
   CFLAGS := $(CFLAGS) -D$(PLATFORM)
endif  

SRCS=            \
       main.c    \
       kl25z.c   \
       msp.c     \
       my_file.c

OBJS:=$(SRCS:.c=.o)


$(info ===========================================================)
$(info = ARCH:     $(ARCH))
$(info = UNAME:    $(UNAME))
$(info = PLATFORM: $(PLATFORM))
$(info = CPU:      $(CPU))
$(info = CWD:      $(CWD))
$(info = CC:       $(CC))
$(info = CSTD:     $(CSTD))
$(info = CFLAGS:   $(CFLAGS))
$(info = SRCS:     $(SRCS))
$(info = OBJS:     $(OBJS))
$(info ===========================================================)


.PHONY: clean preprocess compile assemble build debug all

%.0: %.c
	$(CC) -C $@ -o $< $(CFLAGS)

preprocess: main.c kl25z.c msp.c my_file.c
	$(CC) $(CFLAGS) -E main.c -o main.i

assemble: main.c
	$(CC) $(CFLAGS) -S main.c

compile: main.c
	$(CC) $(CFLAGS) -c main.c

build: main.c
	$(CC) $(CFLAGS) -c main.c

main.out: $(OBJS)
	$(CC) $(CFLAGS) -o $@ $(OBJS)

all: main.out

clean:
	rm -f *.o
	rm -f *.s
	rm -f *.i
