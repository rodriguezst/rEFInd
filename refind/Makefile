#
# refind/Makefile
# Build control file for the rEFInd boot menu
#

SRCDIR = .

VPATH = $(SRCDIR)

ARCH            = $(shell uname -m | sed s,i[3456789]86,ia32,)

TARGET	= refind.efi

ifeq ($(ARCH),ia32)
  LIBEG = build32
  TARGET = refind_ia32.efi
endif

ifeq ($(ARCH),x86_64)
  LIBEG = build64
  TARGET = refind_x64.efi
endif

LOCAL_CPPFLAGS  = -I$(SRCDIR) -I$(SRCDIR)/../include -I$(SRCDIR)/../libeg -I$(SRCDIR)/../mok
LOCAL_LDFLAGS   = -L$(SRCDIR)/../libeg/ -L$(SRCDIR)/../mok/
LOCAL_LIBS      = -leg -lmok

OBJS            = main.o config.o menu.o screen.o icns.o lib.o driver_support.o
#OBJS            = main.o config.o menu.o screen.o icns.o lib.o mok.o driver_support.o variables.o sha256.o pecoff.o simple_file.o security_policy.o guid.o

all: $(TARGET)

include $(SRCDIR)/../Make.common

$(TARGET): $(SHLIB_TARGET)
	$(OBJCOPY) -j .text -j .sdata -j .data -j .dynamic -j .dynsym -j .rel \
		   -j .rela -j .reloc --target=$(FORMAT) $< $@
	chmod a-x $(TARGET)

# EOF
# DO NOT DELETE
