lib_LTLIBRARIES = libhicairo-gobject.la

AM_CPPFLAGS = -I$(top_srcdir)/src -I$(top_builddir)/src

cairoincludedir=$(includedir)/cairo
cairoinclude_HEADERS = cairo-gobject.h
libhicairo_gobject_la_SOURCES = \
	cairo-gobject-enums.c \
	cairo-gobject-structs.c \
	$(NULL)

libhicairo_gobject_la_CFLAGS = $(CAIRO_CFLAGS) $(GOBJECT_CFLAGS)
libhicairo_gobject_la_LDFLAGS = -version-info $(CAIRO_LIBTOOL_VERSION_INFO) -no-undefined $(export_symbols)
libhicairo_gobject_la_LIBADD = $(top_builddir)/src/libhicairo.la $(CAIRO_LIBS) $(GOBJECT_LIBS)

