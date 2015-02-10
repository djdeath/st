m4_define([st_major_version], [0])
m4_define([st_minor_version], [1])
m4_define([st_micro_version], [0])
m4_define([st_version],
          [st_major_version.st_minor_version.st_micro_version])

AC_INIT([st],
        [st_version],
        [],
        [st])

AC_CONFIG_HEADERS([config.h])
AC_CONFIG_SRCDIR([st/st-types.h])

AM_INIT_AUTOMAKE([1.10 no-define foreign dist-xz no-dist-gzip])
AM_MAINTAINER_MODE([enable])

# Initialize libtool
LT_PREREQ([2.2.6])
LT_INIT([disable-static])

PKG_PROG_PKG_CONFIG([0.22])

# Sets GLIB_GENMARSHAL and GLIB_MKENUMS
AM_PATH_GLIB_2_0()

CLUTTER_MIN_VERSION=1.20.0
GTK_MIN_VERSION=3.14.0
GOBJECT_INTROSPECTION_MIN_VERSION=0.10.1
LIBCROCO_MIN_VERSION=0.6.8

GOBJECT_INTROSPECTION_CHECK([$GOBJECT_INTROSPECTION_MIN_VERSION])

PKG_CHECK_MODULES(ST, [
    gtk+-3.0                  >= $GTK_MIN_VERSION
    clutter-1.0               >= $CLUTTER_MIN_VERSION
    gobject-introspection-1.0 >= $GOBJECT_INTROSPECTION_MIN_VERSION
    libcroco-0.6              >= $LIBCROCO_MIN_VERSION
])

GLIB_GSETTINGS

AC_CONFIG_FILES([
    Makefile
    st/Makefile
])
AC_OUTPUT
