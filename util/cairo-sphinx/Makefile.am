cairolibdir = $(libdir)/cairo

cairolib_LTLIBRARIES = cairo-sphinx.la
bin_PROGRAMS = cairo-sphinx

AM_CPPFLAGS = -I$(top_srcdir)/src \
	      -I$(top_builddir)/src \
	      -I$(top_srcdir)/boilerplate \
	      -I$(top_srcdir)/util/cairo-script

cairo_sphinx_la_SOURCES = fdr.c
cairo_sphinx_la_CPPFLAGS = $(AM_CPPFLAGS)
cairo_sphinx_la_CFLAGS = $(CAIRO_CFLAGS)
cairo_sphinx_la_LDFLAGS = -module -no-undefined -avoid-version
if CAIRO_HAS_DL
cairo_sphinx_la_LIBADD = -ldl
endif

cairo_sphinx_SOURCES = sphinx.c
cairo_sphinx_CPPFLAGS = $(AM_CPPFLAGS) -DLIBDIR="\"$(cairolibdir)\""
cairo_sphinx_CFLAGS = $(CAIRO_CFLAGS) $(real_pthread_CFLAGS)  $(glib_CFLAGS)
cairo_sphinx_LDADD = \
	$(real_pthread_LIBS)					\
        $(top_builddir)/util/cairo-script/libhicairo-script-interpreter.la \
        $(top_builddir)/boilerplate/libhicairoboilerplate.la	\
	$(top_builddir)/src/libhicairo.la 			\
	$(glib_LIBS) 						\
	$(CAIRO_LDADD)						\
	$(shm_LIBS)
cairo_sphinx_DEPENDENCIES = \
        $(top_builddir)/util/cairo-script/libhicairo-script-interpreter.la \
        $(top_builddir)/boilerplate/libhicairoboilerplate.la	\
	$(top_builddir)/src/libhicairo.la

# Install rules to rebuild the libraries and add explicit dependencies
$(top_builddir)/boilerplate/libhicairoboilerplate.la: $(top_builddir)/src/libhicairo.la
	cd $(top_builddir)/boilerplate && $(MAKE) $(AM_MAKEFLAGS) libhicairoboilerplate.la

$(top_builddir)/src/libhicairo.la:
	cd $(top_builddir)/src && $(MAKE) $(AM_MAKEFLAGS) libhicairo.la

$(top_builddir)/util/cairo-script/libhicairo-script-interpreter.la: $(top_builddir)/src/libhicairo.la
	cd $(top_builddir)/util/cairo-script && $(MAKE) $(AM_MAKEFLAGS) libhicairo-script-interpreter.la
