# Note: All source files are listed in Makefile.sources.

include $(top_srcdir)/build/Makefile.am.common
include $(srcdir)/Makefile.am.features

EXTRA_DIST += Makefile.win32      Makefile.win32.features
#MAINTAINERCLEANFILES += $(srcdir)/Makefile.win32.features

AM_CPPFLAGS = \
	-I$(srcdir) \
	-I$(top_builddir)/src \
	-I$(top_srcdir)/src \
	$(CAIRO_CFLAGS) \
	$(NULL)
AM_LDFLAGS = $(CAIRO_LDFLAGS)

if BUILD_CXX
cxx_boilerplate_lib = libhicairoboilerplate_cxx.la
else
cxx_boilerplate_lib =
endif

EXTRA_LTLIBRARIES += libhicairoboilerplate.la $(cxx_boilerplate_lib)


libhicairoboilerplate_la_SOURCES = \
	$(enabled_cairo_boilerplate_headers) \
	$(enabled_cairo_boilerplate_private) \
	$(enabled_cairo_boilerplate_sources) \
	cairo-boilerplate-constructors.c \
	$(NULL)
libhicairoboilerplate_cxx_la_SOURCES = \
	$(enabled_cairo_boilerplate_cxx_sources) \
	$(NULL)
libhicairoboilerplate_la_LIBADD = $(top_builddir)/src/libhicairo.la \
	$(cxx_boilerplate_lib) \
	$(CAIRO_LIBS) \
	$(CAIROBOILERPLATE_LIBS) \
	$(NULL)
libhicairoboilerplate_cxx_la_LIBADD = $(top_builddir)/src/libhicairo.la \
	$(CAIRO_LIBS) \
	$(CAIROBOILERPLATE_LIBS) \
	$(NULL)
libhicairoboilerplate_la_DEPENDENCIES = \
	$(cxx_boilerplate_lib) \
	$(NULL)

if CAIRO_HAS_DL
libhicairoboilerplate_la_LIBADD += -ldl
endif

if CAIRO_HAS_BEOS_SURFACE
# BeOS system headers trigger this warning
libhicairoboilerplate_cxx_la_CXXFLAGS = -Wno-multichar
endif

if CAIRO_HAS_WIN32_SURFACE
libhicairoboilerplate_la_LIBADD += -lwinspool
endif

cairo-boilerplate-constructors.c: Makefile $(enabled_cairo_boilerplate_sources) $(enabled_cairo_boilerplate_cxx_sources) make-cairo-boilerplate-constructors.sh
	(cd $(srcdir) && sh ./make-cairo-boilerplate-constructors.sh $(enabled_cairo_boilerplate_sources) $(enabled_cairo_boilerplate_cxx_sources)) > $@

BUILT_SOURCES += cairo-boilerplate-constructors.c
EXTRA_DIST += $(BUILT_SOURCES) make-cairo-boilerplate-constructors.sh
CLEANFILES += $(BUILT_SOURCES)

test: check

if CROSS_COMPILING
else
TESTS += check-link$(EXEEXT)
endif

check_PROGRAMS += check-link
check_link_LDADD = libhicairoboilerplate.la
