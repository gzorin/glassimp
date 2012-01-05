lib_LTLIBRARIES = libglassimp.la
include_HEADERS = glassimp.h

pkgconfigdir = $(libdir)/pkgconfig
pkgconfig_HEADERS = glassimp.pc

BUILT_SOURCES = glassimp.pc

libglassimp_la_SOURCES = glassimp.cc
libglassimp_la_CPPFLAGS = @assimp_CPPFLAGS@
libglassimp_la_LDFLAGS = @assimp_LDFLAGS@
libglassimp_la_LIBADD = @assimp_LIBS@
