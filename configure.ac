AC_INIT([eif],[1.3.4],[marcolz@stack.nl])
AC_CONFIG_SRCDIR([src/eif.c])
AM_INIT_AUTOMAKE
AC_CONFIG_HEADERS(config.h)

dnl Checks for programs.

dnl Why doesn't configure do this by itself ? It might be necessary for
dnl header checks...

if test x$includedir != x
then
	CPPFLAGS="${CPPFLAGS} -I${includedir}"
fi

if test x$oldincludedir != x
then
	CPPFLAGS="${CPPFLAGS} -I${oldincludedir}"
fi

CPPFLAGS="${CPPFLAGS} -I/usr/local/include -I/usr/pkg/include"
LDFLAGS="${LDFLAGS} -L/usr/local/lib -L/usr/pkg/lib"

if test x$libdir != x
then
	LDFLAGS="${LDFLAGS} -L${libdir}"
fi

if test x$GCC != x
then
	CFLAGS="${CFLAGS} -Wall -W -Wshadow -Wbad-function-cast -Wcast-qual -Wwrite-strings"
fi

AC_PROG_CC
AC_PROG_LN_S
AC_PROG_RANLIB

dnl Checks for libraries.

AC_CHECK_LIB(bsd, bsd_ioctl)
AC_CHECK_LIB(curses, tgetent)

dnl AC_CHECK_LIB(dl, main)

AC_CHECK_LIB(readline, rl_unbind_key, ,AC_MSG_ERROR([You really need this one !.]))

AC_CHECK_LIB(termcap, main)

dnl Checks for header files.
AC_HEADER_DIRENT
AC_CHECK_HEADERS(fcntl.h malloc.h stdlib.h string.h strings.h sys/file.h sys/ioctl.h sys/select.h sys/time.h termcap.h termio.h unistd.h readline/tilde.h)
AC_CHECK_HEADERS(readline/readline.h, , AC_MSG_ERROR([You really need this one !.]))

dnl Checks for typedefs, structures, and compiler characteristics.
AC_C_CONST

dnl Checks for library functions.
AC_FUNC_ALLOCA
AC_FUNC_VPRINTF
AC_CHECK_FUNCS(getaddrinfo getnameinfo getwd select setenv socket strdup unsetenv)

dnl old acconfig.h
AH_TOP([#ifndef EIF_CONFIG_H
#define EIF_CONFIG_H
])

AH_BOTTOM([#ifdef  HAVE_GETADDRINFO
#ifdef  HAVE_GETNAMEINFO
#define USE_IPv6
#endif  /* HAVE_GETNAMEINFO */
#endif  /* HAVE_GETADDRINFO */

#ifndef HAVE_READLINE_TILDE_H
#ifdef  READLINE_HANDLES_CONST
extern char *tilde_expand(const char *);
#else   /* READLINE_HANDLES_CONST */
extern char *tilde_expand(char *);
#endif  /* READLINE_HANDLES_CONST */
#endif  /* HAVE_READLINE_TILDE_H */

#ifndef READLINE_UNBIND_KEY
int     rl_unbind_key(int key);
#endif  /* READLINE_UNBIND_KEY */
#endif  /* EIF_CONFIG_H */
])

dnl Local additions from aclocal.m4
EIF_READLINE_HANDLES_CONST
EIF_READLINE_UNBIND_KEY

AC_SUBST(AM_CFLAGS)

AC_CONFIG_FILES([ \
	Makefile \
	src/Makefile \
	src/connect/Makefile \
	contrib/Makefile \
	doc/Makefile \
	])
AC_OUTPUT
