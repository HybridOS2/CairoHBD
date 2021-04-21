include $(top_srcdir)/util/cairo-script/Makefile.sources

SUBDIRS = examples

lib_LTLIBRARIES = libhicairo-script-interpreter.la
EXTRA_PROGRAMS = csi-replay csi-exec csi-bind

AM_CPPFLAGS = -I$(top_srcdir)/src -I$(top_builddir)/src

cairoincludedir=$(includedir)/cairo
cairoinclude_HEADERS = cairo-script-interpreter.h
libhicairo_script_interpreter_la_SOURCES = \
	$(libhicairo_script_interpreter_sources)	\
	$(libhicairo_script_interpreter_headers)	\
	$(NULL)
libhicairo_script_interpreter_la_CFLAGS = $(CAIRO_CFLAGS)
libhicairo_script_interpreter_la_LDFLAGS = -version-info $(CAIRO_LIBTOOL_VERSION_INFO) -no-undefined $(export_symbols)
libhicairo_script_interpreter_la_LIBADD = $(top_builddir)/src/libhicairo.la $(CAIRO_LIBS) $(lzo_LIBS) -lz

csi_replay_SOURCES = csi-replay.c
csi_replay_CFLAGS = $(CAIRO_CFLAGS)
csi_replay_LDADD = libhicairo-script-interpreter.la $(top_builddir)/src/libhicairo.la $(CAIRO_LIBS)

csi_exec_SOURCES = csi-exec.c
csi_exec_LDADD = libhicairo-script-interpreter.la $(top_builddir)/src/libhicairo.la $(CAIRO_LIBS)

if CAIRO_HAS_SCRIPT_SURFACE
EXTRA_PROGRAMS += csi-trace
csi_trace_SOURCES = csi-trace.c
csi_trace_LDADD = libhicairo-script-interpreter.la $(top_builddir)/src/libhicairo.la $(CAIRO_LIBS)
endif

EXTRA_DIST = \
	COPYING
