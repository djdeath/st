st_cflags =					\
	-I$(top_srcdir)				\
	-DPREFIX=\""$(prefix)"\"		\
	-DLIBDIR=\""$(libdir)"\"		\
	-DG_LOG_DOMAIN=\"St\"			\
	-DST_COMPILATION			\
	-DCLUTTER_ENABLE_EXPERIMENTAL_API	\
	-DCOGL_ENABLE_EXPERIMENTAL_API		\
	-DPACKAGE_DATA_DIR=\"$(pkgdatadir)\"	\
	$(ST_CFLAGS)				\
	$(NULL)

st_built_sources =				\
	st-enum-types.h				\
	st-enum-types.c

BUILT_SOURCES = $(st_built_sources)

EXTRA_DIST =					\
	test-theme.css				\
	st-enum-types.h.in			\
	st-enum-types.c.in

CLEANFILES = stamp-st-enum-types.h

st-enum-types.h: stamp-st-enum-types.h Makefile
	@true
stamp-st-enum-types.h: $(source_h) $(srcdir)/st-enum-types.h.in $(st_source_h)
	$(AM_V_GEN) (							\
	  $(GLIB_MKENUMS)						\
	    --template $(srcdir)/st-enum-types.h.in			\
	  $(addprefix $(srcdir)/, $(st_source_h)) ) >> $@.tmp &&	\
	(cmp -s $@.tmp st-enum-types.h || cp $@.tmp st-enum-types.h) &&	\
	rm -f $@.tmp &&							\
	echo timestamp > $(@F)

st-enum-types.c: stamp-st-enum-types.h $(srcdir)/st-enum-types.c.in
	$(AM_V_GEN) (				\
	  $(GLIB_MKENUMS)			\
	    --template $(srcdir)/st-enum-types.c.in	\
	  $(addprefix $(srcdir)/,$(st_source_h)) ) >> $@.tmp &&		\
	cp $@.tmp $@ &&				\
	rm -f $@.tmp

# please, keep this sorted alphabetically
st_source_h =					\
	st-adjustment.h				\
	st-bin.h				\
	st-border-image.h			\
	st-box-layout.h				\
	st-box-layout-child.h			\
	st-button.h				\
	st-clipboard.h				\
	st-drawing-area.h			\
	st-entry.h				\
	st-focus-manager.h			\
	st-generic-accessible.h			\
	st-icon.h				\
	st-icon-colors.h			\
	st-im-text.h				\
	st-label.h				\
	st-private.h				\
	st-scrollable.h				\
	st-scroll-bar.h				\
	st-scroll-view.h			\
	st-shadow.h				\
	st-table.h				\
	st-table-child.h			\
	st-texture-cache.h			\
	st-theme.h				\
	st-theme-context.h			\
	st-theme-node.h				\
	st-types.h				\
	st-widget.h				\
	st-widget-accessible.h			\
	$(NULL)

st.h: stamp-st.h
	@true
stamp-st.h: Makefile
	$(AM_V_GEN) (echo "#define ST_H_INSIDE 1";	\
	for name in $(st_source_h); do			\
	  echo "#include <"$$name">";			\
	done; echo "#undef ST_H_INSIDE") > $@.tmp &&	\
	(cmp -s $@.tmp st.h || cp $@.tmp st.h) &&	\
	rm -f $@.tmp &&					\
	echo timestamp > $(@F)

BUILT_SOURCES += st.h
CLEANFILES += stamp-st.h

st-scroll-view-fade-generated.c: stamp-st-scroll-view-fade-generated.c
	@true
stamp-st-scroll-view-fade-generated.c: $(srcdir)/st-scroll-view-fade.glsl $(srcdir)/data-to-c.pl
	$(AM_V_GEN) $(srcdir)/data-to-c.pl $(srcdir)/st-scroll-view-fade.glsl st_scroll_view_fade_glsl > $@.tmp && \
	(cmp -s $@.tmp st-scroll-view-fade-generated.c || cp $@.tmp st-scroll-view-fade-generated.c) && \
	rm -f $@.tmp &&				\
	echo timestamp > $(@F)

BUILT_SOURCES += st-scroll-view-fade-generated.c
CLEANFILES += stamp-st-scroll-view-fade-generated.c
EXTRA_DIST += 					\
	st-scroll-view-fade.glsl		\
	data-to-c.pl				\
	$(NULL)

st_source_private_h =				\
	st-private.h				\
	st-table-private.h			\
	st-theme-private.h			\
	st-theme-node-private.h			\
	st-theme-node-transition.h

# please, keep this sorted alphabetically
st_source_c =					\
	st-adjustment.c				\
	st-bin.c				\
	st-border-image.c			\
	st-box-layout.c				\
	st-box-layout-child.c			\
	st-button.c				\
	st-clipboard.c				\
	st-drawing-area.c			\
	st-entry.c				\
	st-focus-manager.c			\
	st-generic-accessible.c			\
	st-icon.c				\
	st-icon-colors.c			\
	st-im-text.c				\
	st-label.c				\
	st-private.c				\
	st-scrollable.c				\
	st-scroll-bar.c				\
	st-scroll-view.c			\
	st-shadow.c				\
	st-table.c				\
	st-table-child.c			\
	st-texture-cache.c			\
	st-theme.c				\
	st-theme-context.c			\
	st-theme-node.c				\
	st-theme-node-drawing.c			\
	st-theme-node-transition.c		\
	st-widget.c				\
	$(NULL)

st_non_gir_sources =           \
	st-scroll-view-fade.c	\
	st-scroll-view-fade.h	\
	$(NULL)

lib_LTLIBRARIES = libst-1.0.la

libst_1_0_la_LIBADD = -lm $(ST_LIBS)
libst_1_0_la_SOURCES =				\
	$(st_source_c)				\
	$(st_non_gir_sources)			\
	$(st_source_private_h)			\
	$(st_source_private_c)			\
	$(st_source_h)				\
	$(NULL)
nodist_libst_1_0_la_SOURCES =			\
	$(st_built_sources)			\
	st.h					\
	$(NULL)
libst_1_0_la_CPPFLAGS = $(st_cflags)
libst_1_0_la_LDFLAGS = $(LDADD)

noinst_PROGRAMS = test-theme

test_theme_CPPFLAGS = $(st_cflags)
test_theme_LDADD = $(ST_LIBS) libst-1.0.la

test_theme_SOURCES = test-theme.c

-include $(INTROSPECTION_MAKEFILE)
INTROSPECTION_GIRS =
INTROSPECTION_SCANNER_ARGS = --warn-all --warn-error --add-include-path=$(srcdir)
INTROSPECTION_COMPILER_ARGS = --includedir=$(top_srcdir) --includedir=$(top_builddir)

St-1.0.gir: libst-1.0.la
St_1_0_gir_INCLUDES = Clutter-1.0 Gtk-3.0
St_1_0_gir_CFLAGS = $(st_cflags) -DST_COMPILATION
St_1_0_gir_LIBS = libst-1.0.la
St_1_0_gir_FILES = $(filter-out %-private.h $(st_non_gir_sources), $(addprefix $(srcdir)/,$(st_source_h))) \
	$(addprefix $(srcdir)/,$(st_source_c))
INTROSPECTION_GIRS += St-1.0.gir
CLEANFILES += St-1.0.gir

BUILT_GIRSOURCES = St-1.0.gir

girdir = $(datadir)/gir-1.0
gir_DATA = $(BUILT_GIRSOURCES)

typelibsdir = $(libdir)/girepository-1.0/
typelibs_DATA = $(BUILT_GIRSOURCES:.gir=.typelib)
