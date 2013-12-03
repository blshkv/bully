prefix = /usr/local
exec_prefix = $(prefix)
bindir = $(exec_prefix)/bin

W_NAME	= bully
W_ROOT	= `pwd`

CFLAGS	+= -I$(W_ROOT) -I$(W_ROOT)/utils/ -I$(W_ROOT)/tls/
CFLAGS	+= -I$(W_ROOT)/wps/ -I$(W_ROOT)/crypto/ -I$(W_ROOT)/common/

LDFLAGS += -lpcap -lssl -lcrypto

HDRS	= $(W_NAME).h 80211.h frame.h iface.h bswap.h version.h
SRCS	= $(W_NAME).c 80211.c frame.c iface.c crc32.c timer.c utils.c

OBJS = utils/base64.o  utils/common.o  utils/eloop.o  utils/ip_addr.o  utils/os_unix.o  utils/radiotap.o  utils/trace.o  utils/uuid.o  utils/wpa_debug.o  utils/wpabuf.o
SUBDIRS=common crypto tls utils wps

all:  $(W_NAME)

$(W_NAME): $(HDRS) $(SRCS)
	for d in $(SUBDIRS); do [ -d $$d ] && $(MAKE) -C $$d; done
	$(CC) $(CFLAGS) -o $(@) $(OBJS) $(W_NAME).c $(LDFLAGS)

strip: $(W_NAME)
	strip $(W_NAME)

clean:
	for d in $(SUBDIRS); do [ -d $$d ] && $(MAKE) -C $$d clean; done
	-rm -f $(W_NAME) $(W_NAME).o

distclean: clean

install: all
	install -d $(DESTDIR)$(bindir)
	install -m 755 $(W_NAME) $(DESTDIR)$(bindir)

uninstall:
	-rm -f $(DESTDIR)$(bindir)/$(W_NAME)
