## Makefile

PREFIX=/usr/local
BINDIR=bin

TARGET		= galasm
OBJS		= galasm.o support.o jedec.o localize.o

CFLAGS		= -Wall -Wextra -O2

ifeq ($(WIN),y)
# 32 bit Windows executable:
   CC		= i686-w64-mingw32-gcc
# 64 bit Windows executable:
#  CC		= x86_64-w64-mingw32-gcc
   TARGET	= galasm.exe
   CFLAGS	+= -static
endif


default: $(TARGET)
all: $(TARGET) winexe galasm.com

winexe: $(OBJS)
	gmake WIN=y clean && gmake WIN=y

$(TARGET): $(OBJS)
	$(CC) $(CFLAGS) -o $@ $(OBJS)

# 16 bit DOS executable with OpenWatcom v2 compiler:
galasm.com: galasm.c support.c jedec.c localize.c
	PATH=/opt/watcom/binl64 WATCOM=/opt/watcom wcl -mt -fe=$@ -cc $^

clean:
	-rm -f $(OBJS)
	-rm -f *.[oa] $(TARGET) Makefile.bak
	-rm -f galasm galasm.com galasm.exe

cleantilde:
	/usr/bin/find . -regex ".+~$$" -exec /bin/rm {} \;


install: $(TARGET)
	@if [ `id -u` != "0" ] ; then echo "must be root!"; exit 1; fi;
	test -d $(PREFIX)/$(BINDIR) || mkdir -p $(PREFIX)/$(BINDIR)
	install -m 0755 $(TARGET) $(PREFIX)/$(BINDIR)

uninstall:
	@if [ `id -u` != "0" ] ; then echo "must be root!"; exit 1; fi;
	rm -f $(PREFIX)/$(BINDIR)/$(TARGET)


# Do not run multiple builds at the same time, this doesn't work
.NOTPARALLEL:

.PHONY: all install uninstall

