#                                               -*- Autoconf -*-
# Process this file with autoconf to produce a configure script.

AC_PREREQ([2.69])
AC_INIT([twitter-cli], [0.2], [https://github.com/dvalcarce/twitter-cli/issues], [twitter-cli], [https://github.com/dvalcarce/twitter-cli])

AC_REVISION([$Id$])

AC_CONFIG_SRCDIR([src/headers.h])
AC_CONFIG_HEADERS([src/config.h])

AM_SILENT_RULES([yes])
AM_INIT_AUTOMAKE([foreign -Wall -Werror])

# Checks for programs.
AC_PROG_YACC
AC_PROG_CC
AC_PROG_LEX
AC_PROG_INSTALL

# Checks for header files.
AC_CHECK_HEADERS([arpa/inet.h netdb.h netinet/in.h stdlib.h string.h strings.h sys/socket.h unistd.h])

# Checks for libraries
AC_CHECK_LIB([ssl], [SSL_library_init])
AC_CHECK_LIB([curl], [curl_version])


AC_ARG_ENABLE([liboauth], AS_HELP_STRING([--disable-liboauth], [Disable builtin liboauth]))

ac_contrib_dir=`readlink -f $srcdir`/contrib
ac_liboauth_cflags=""
ac_liboauth_ldflags=""


AC_ARG_ENABLE([unicode],
	      AS_HELP_STRING([--enable-unicode], [Enable unicode characters in RT/Fav display (disabled by default)]),
	      [if test x$enableval = xyes; then
			AC_DEFINE([HAVE_UNICODE_ENABLED], [1], [Define this to enable unicode characters in RT and Favs])
		fi])


AS_IF([test "x$enable_liboauth" != "xno"], [
        AC_MSG_CHECKING([liboauth])
	AS_IF([test -f contrib/liboauth-1.0.1/src/.libs/liboauth.so], [
	       AC_MSG_RESULT([Already done])
	       ],
	       [
		( cd contrib && tar -zxf liboauth-1.0.1.tar.gz && \
		 cd liboauth-1.0.1 && \
		 ./configure CFLAGS="$ac_liboauth_cflags" LDFLAGS="$ac_liboauth_ldflags" && make)
		( cd libs && ln -s $srcdir/contrib/liboauth-1.0.1/src/.libs/liboauth.so )
		AC_MSG_RESULT([done])])
 
#        ( cd contrib && tar -xzf liboauth-1.0.1.tar.gz )
#        AC_CONFIG_SUBDIRS([contrib/liboauth-1.0.1])
       AC_SUBST([liboauth], [$srcdir/contrib/liboauth-1.0.1/src])
       ])



# Checks for typedefs, structures, and compiler characteristics.
AC_CHECK_HEADER_STDBOOL
AC_C_INLINE

# Checks for library functions.
AC_FUNC_MALLOC
AC_CHECK_FUNCS([gethostbyname memmove memset socket strdup strncasecmp strpbrk strtol])


AC_CONFIG_FILES([Makefile
                 src/Makefile
])
                 #contrib/Makefile])

# AC_CONFIG_SUBDIRS([contrib/liboauth-1.0.1])


AC_OUTPUT
