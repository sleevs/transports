# Process this file with autoconf to produce a configure script.
AC_INIT([jggtrans], [2.2.4+xk1], [tomek@xiaoka.com])

AC_CONFIG_MACRO_DIR([m4])
AC_CONFIG_SRCDIR([src/ggtrans.h])
AM_INIT_AUTOMAKE
AM_GNU_GETTEXT_VERSION(0.14.1)
AM_CONFIG_HEADER([config.h])

# Checks for programs.
AC_PROG_CC
AM_PROG_CC_C_O
AC_C_BIGENDIAN
AC_PROG_MAKE_SET
AM_PROG_LIBTOOL
AM_GNU_GETTEXT([external])

CFLAGS="$CFLAGS -Wall"

AM_PATH_GLIB_2_0([2.0.0],[],AC_MSG_ERROR("You need glib >= 2.0.0 to compile this."))
PKG_CHECK_MODULES([JK_LIBIDN], [libidn >= 0.3.0])

AC_SUBST(JK_LIBIDN_LIBS)
AC_SUBST(JK_LIBIDN_CFLAGS)

AC_ARG_ENABLE([debug],AC_HELP_STRING([--disable-debug],[Disable debugging code]))

AC_ARG_WITH([efence],AC_HELP_STRING([--with-efence],[Link against ElectricFence library]))

AC_ARG_WITH([dmalloc],AC_HELP_STRING([--with-dmalloc],[Link against dmalloc library]))

if test "x$enable_debug" != "xno" ; then
	AC_DEFINE(DEBUG,1,[Define to enable debugging code])
fi

if test "x$with_efence" = "xyes" ; then
	AC_CHECK_LIB([efence], [malloc])
fi

if test "x$with_dmalloc" = "xyes" ; then
	AC_CHECK_LIB([dmalloc], [malloc])
	AC_DEFINE(DMALLOC,1,[Define to enable dmalloc])
	AC_DEFINE(DMALLOC_FUNC_CHECK,1,[Define to enable dmalloc function arguments check])
fi

# Checks for header files.
AC_HEADER_DIRENT
AC_HEADER_STDC
AC_HEADER_SYS_WAIT
AC_CHECK_HEADERS([stdlib.h string.h])
AC_CHECK_HEADERS([sys/socket.h netdb.h netinet/in.h])
AC_CHECK_HEADERS([sys/time.h unistd.h errno.h fcntl.h])

# Checks for typedefs, structures, and compiler characteristics.
AC_C_CONST
AC_TYPE_SIZE_T
AC_HEADER_TIME

# Checks for library functions.
AC_FUNC_ERROR_AT_LINE
AC_TYPE_SIGNAL
AC_FUNC_STAT

AC_SEARCH_LIBS([gethostbyname],[resolv nsl],[],AC_MSG_ERROR("Some functions needed are missing"))
AC_SEARCH_LIBS([inet_aton],[resolv nsl],[],AC_MSG_ERROR("Some functions needed are missing"))
AC_SEARCH_LIBS([socket],[socket],[],AC_MSG_ERROR("Some functions needed are missing"))
AC_CHECK_FUNCS([isascii],[],AC_MSG_ERROR("Some functions needed are missing"))
AC_CHECK_FUNCS([select],[],AC_MSG_ERROR("Some functions needed are missing"))
AC_CHECK_FUNCS([memset strchr],[],AC_MSG_ERROR("Some functions needed are missing"))

AC_CONFIG_SUBDIRS([libxode libgadu])

MKINSTALLDIRS="${MKINSTALLDIRS} -m 755"
XGETTEXT="${XGETTEXT} --keyword=L_"

AC_CONFIG_FILES([Makefile src/Makefile po/Makefile.in])
AC_OUTPUT
