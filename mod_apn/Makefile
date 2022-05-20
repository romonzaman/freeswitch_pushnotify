################################
### FreeSwitch headers files found in libfreeswitch-dev ###
FS_INCLUDES=/usr/include/freeswitch
FS_MODULES=/usr/lib/freeswitch/mod
################################

### END OF CUSTOMIZATION ###
SHELL := /bin/bash
PROC?=$(shell uname -m)

CC=gcc
CFLAGS=-fPIC -O3 -fomit-frame-pointer -fno-exceptions -Wall -std=c99 -pedantic
ifeq (${PROC},x86_64)
	CFLAGS+=-m64 -mtune=generic
else
	CFLAGS+=-m32 -march=i686
endif

INCLUDES=-I/usr/include -I/usr/src/freeswitch/src/include  -I$(FS_INCLUDES)
LDFLAGS=-lm -Wl,-static  -Wl,-Bdynamic

all : mod_apn.o
	$(CC) $(CFLAGS) $(INCLUDES) -shared -Xlinker -x -o mod_apn.so mod_apn.o $(LDFLAGS)

mod_apn.o: mod_apn.c
	$(CC) $(CFLAGS) $(INCLUDES) -c mod_apn.c

clean:
	rm -f *.o *.so *.a *.la; && make clean; cd ..

distclean: clean
	rm -fR bcg729

install: all
	/usr/bin/install -c mod_apn.so $(INSTALL_PREFIX)/$(FS_MODULES)/mod_apn.so
