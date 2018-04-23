## Makefile

TARGET		= galasm
OBJS		= galasm.o support.o jedec.o localize.o

CFLAGS		= -Wall -O2

ifeq ($(WIN),y)
   CC		= i686-w64-mingw32-gcc
   TARGET	= galasm.exe
   CFLAGS	+= -static
endif


all: $(TARGET)

$(TARGET): $(OBJS)
	$(CC) -Wall $(CFLAGS) -o $@ $(OBJS)

clean:
	-rm -f $(OBJS)
	-rm -f *.[oa] $(TARGET) Makefile.bak

cleantilde:
	/usr/bin/find . -regex ".+~$$" -exec /bin/rm {} \;

