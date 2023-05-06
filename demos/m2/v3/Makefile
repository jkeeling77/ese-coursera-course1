
UNAME := $(shell uname)

CFLAGS := -Wall -v
ifeq ($(UNAME), Linux)
   CC=gcc
   CFLAGS := $(CFLAGS) -std=c99
else
   CC=arm-none-eabi-gcc
   CFLAGS := $(CFLAGS) -std=c99 --specs=nosys.specs --mcpu=cortex-m4 -mthumb -march=arm7e-m
endif  


$(info ============================================)
$(info UNAME:  $(UNAME))
$(info CC:     $(CC))
$(info CFLAGS: $(CFLAGS))
$(info ============================================)

.PHONY: clean build compile assemble

assemble: main.c
	$(CC) $(CFLAGS) -S main.c

compile: main.c
	$(CC) $(CFLAGS) -c main.c

build: main.c
	$(CC) $(CFLAGS) -c main.c

clean:
	rm -f *.o
	rm -f *.s
