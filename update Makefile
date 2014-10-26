
OPTS = -DCHECK_NEXTDCW -DHTTP_SRV -DMGCAMD_SRV -DCCCAM_SRV -DFREECCCAM_SRV -DCCCAM_CLI -DRADEGAST_CLI

ifeq ($(target),x32)
  CC        = gcc
  CXX       = g++
  STRIP     = strip
  OUTPUT	= x32/
  CFLAGS	= -s -ggdb3 -m32 -O2 -I. -DTARGET=1 $(OPTS)
  LFLAGS	= $(CFLAGS)
else
ifeq ($(target),x64)
  CC        = gcc
  CXX       = g++
  STRIP     = strip
  OUTPUT	= x64/
  CFLAGS	= -s -ggdb3 -m64 -O2 -I. -DTARGET=1 $(OPTS)
  LFLAGS	= $(CFLAGS)
else
ifeq ($(target),ppc-old)
  CC        = powerpc-tuxbox-linux-gnu-gcc
  CXX       = powerpc-tuxbox-linux-gnu-g++
  STRIP     = powerpc-tuxbox-linux-gnu-strip
  OUTPUT	= ppc-old/
  CFLAGS	= -s -ggdb3 -O2 -DTARGET=3 $(OPTS) -DINOTIFY
  LFLAGS	= $(CFLAGS)
else
ifeq ($(target),mips)
  CC        = mipsel-linux-gnu-gcc
  CXX       = mipsel-linux-gnu-g++
  STRIP     = mipsel-linux-gnu-strip
  OUTPUT	= mips/
  CFLAGS	= -s -ggdb3 -O2 -DTARGET=3 $(OPTS)
  LFLAGS	= $(CFLAGS)
else
ifeq ($(target),openwrt)
  CC        = armeb-linux-gcc
  CXX       = armeb-linux-g++
  STRIP     = armeb-linux-strip
  OUTPUT	= openwrt/
  CFLAGS	= -s -ggdb3 -O2 -DTARGET=3 $(OPTS)
  LFLAGS	= $(CFLAGS)
else
ifeq ($(target),ppc)
  CC        = powerpc-linux-gcc
  CXX       = powerpc-linux-g++
  STRIP     = powerpc-linux-strip
  OUTPUT	= ppc/
  CFLAGS	= -s -ggdb3 -O2 -DTARGET=3 $(OPTS) -DINOTIFY
  LFLAGS	= $(CFLAGS)
else
ifeq ($(target),sh4)
  CC        = /opt/STM/STLinux-2.4/devkit/sh4/bin/sh4-linux-gcc
  CXX       = /opt/STM/STLinux-2.4/devkit/sh4/bin/sh4-linux-g++
  STRIP     = /opt/STM/STLinux-2.4/devkit/sh4/bin/sh4-linux-strip
  OUTPUT	= sh4/
  CFLAGS	= -ggdb3 -O2 $(OPTS) -DST_7201  -DST_OSLINUX  -DARCHITECTURE_ST40
  LFLAGS	= $(CFLAGS)
else
ifeq ($(target),win32)
  CC        = i586-mingw32msvc-gcc
  CXX       = i586-mingw32msvc-g++
  STRIP     = i586-mingw32msvc-strip
  OUTPUT	= win32/
  CFLAGS	= -s -ggdb3 -O2 -DTARGET=2 -DWIN32 $(OPTS)
  LFLAGS	= $(CFLAGS)
else
  CC        = gcc
  CXX       = g++
  STRIP     = strip
  OUTPUT	= x/
  CFLAGS	= -ggdb3 -O2 -Wall -I. -DTARGET=2 $(OPTS)
  LFLAGS	= $(CFLAGS)
endif
endif
endif
endif
endif
endif
endif
endif

ifndef name
	AOUT	= $(OUTPUT)multics
else
	AOUT	= $(name)
endif


OBJECTS = $(OUTPUT)sha1.o $(OUTPUT)des.o $(OUTPUT)md5.o $(OUTPUT)convert.o $(OUTPUT)tools.o $(OUTPUT)threads.o $(OUTPUT)debug.o \
	$(OUTPUT)sockets.o $(OUTPUT)msg-newcamd.o $(OUTPUT)msg-cccam.o $(OUTPUT)msg-radegast.o $(OUTPUT)parser.o $(OUTPUT)config.o \
	$(OUTPUT)ecmdata.o $(OUTPUT)httpserver.o $(OUTPUT)main.o

link: main.c $(OBJECTS)
	$(CC) $(LFLAGS) -o $(AOUT) $(OBJECTS) -lpthread

%.o: ../%.c Makefile common.h httpserver.h config.h
	$(CC) -c $(CFLAGS) $< -o $@

clean:
	-rm $(OUTPUT)*

cleanall:
	$(MAKE) clean
	$(MAKE) target=x64 clean
	$(MAKE) target=x32 clean
	$(MAKE) target=ppc clean
	$(MAKE) target=ppc-old clean
	$(MAKE) target=mips clean
	$(MAKE) target=sh4 clean

