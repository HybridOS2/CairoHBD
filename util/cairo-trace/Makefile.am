cairolibdir = $(libdir)/cairo
cairooutdir = $(localstatedir)/lib/cairo-trace

bin_SCRIPTS = cairo-trace
cairolib_LTLIBRARIES = libhicairo-trace.la

AM_CPPFLAGS = -I$(top_srcdir)/src \
	      -I$(top_builddir)/src

libhicairo_trace_la_SOURCES = trace.c
libhicairo_trace_la_CPPFLAGS = -DCAIRO_TRACE_OUTDIR="\"$(cairooutdir)\"" \
			  $(AM_CPPFLAGS)
libhicairo_trace_la_CFLAGS = $(CAIRO_CFLAGS) $(real_pthread_CFLAGS)
libhicairo_trace_la_LDFLAGS = -module -no-undefined -avoid-version

libhicairo_trace_la_LIBADD = $(real_pthread_LIBS) -lz
if CAIRO_HAS_DL
libhicairo_trace_la_LIBADD += -ldl
endif

if CAIRO_HAS_SYMBOL_LOOKUP
libhicairo_trace_la_SOURCES += \
			 lookup-symbol.c \
			 lookup-symbol.h
libhicairo_trace_la_LIBADD += $(BFD_LIBS)
endif


system-install: install
	-mkdir -p $(cairooutdir)
	-chmod 01777 $(cairooutdir)
	grep -sq $(cairolibdir)/libhicairo-trace.so /etc/ld.so.preload || echo $(cairolibdir)/libhicairo-trace.so >> /etc/ld.so.preload

system-uninstall: uninstall
	sed -e '/libhicairo-trace.so/d' < /etc/ld.so.preload > /tmp/ld.so.preload && mv /tmp/ld.so.preload /etc/ld.so.preload;

EXTRA_DIST = \
	COPYING \
	COPYING-GPL-3 \
	cairo-trace.in
