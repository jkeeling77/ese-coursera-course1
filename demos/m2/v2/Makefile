
.PHONY: clean build

#CC=gcc
CC=arm-none-eabi-gcc
CFLAGS= -Wall -v -std=c99

build: main.c
	$(CC) $(CFLAGS) -c main.c

clean:
	rm *.o
