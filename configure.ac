AC_INIT([glassimp],[0.1])
AC_CONFIG_SRCDIR([src/glassimp.h])
AC_CONFIG_AUX_DIR([config])
AC_CONFIG_MACRO_DIR([m4])
AM_INIT_AUTOMAKE([foreign])
AC_CONFIG_FILES(
	Makefile
	src/Makefile
	)

AC_PROG_CXX
AC_PROG_LIBTOOL
PKG_PROG_PKG_CONFIG

AC_LANG([C++])

AX_ENABLE_DEFAULT_PKGCONFIGDIR([pkgconfigdir],["${libdir}/pkgconfig"])
AX_CREATE_PKGCONFIG_INFO([src/glassimp.pc],[assimp])

# Look for the assimp library itself:
if ! `${PKG_CONFIG} --exists assimp`; then
AC_MSG_ERROR([cannot find assimp library in PKG_CONFIG_PATH])
fi

assimp_CPPFLAGS=`pkg-config --cflags assimp`
assimp_LDFLAGS=`pkg-config --libs-only-L assimp`
assimp_LIBS=`pkg-config --libs-only-l assimp`

AC_SUBST([assimp_CPPFLAGS])
AC_SUBST([assimp_LDFLAGS])
AC_SUBST([assimp_LIBS])

AC_OUTPUT
