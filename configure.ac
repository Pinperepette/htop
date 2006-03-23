#                                               -*- Autoconf -*-
# Process this file with autoconf to produce a configure script.

AC_PREREQ(2.57)
AC_INIT([htop],[UNRELEASED-2006.01.12],[loderunner@users.sourceforge.net])
AM_INIT_AUTOMAKE
AC_CONFIG_SRCDIR([htop.c])
AC_CONFIG_HEADER([config.h])

# Checks for programs.
AC_PROG_CC

# Checks for libraries.
AC_CHECK_LIB([ncurses], [refresh])
AC_CHECK_LIB([m], [ceil])

# Checks for header files.
AC_HEADER_DIRENT
AC_HEADER_STDC
AC_CHECK_HEADERS([stdlib.h string.h strings.h sys/param.h sys/time.h unistd.h curses.h])

# Checks for typedefs, structures, and compiler characteristics.
AC_HEADER_STDBOOL
AC_C_CONST
AC_TYPE_PID_T
AC_TYPE_UID_T

# Checks for library functions.
AC_FUNC_CLOSEDIR_VOID
AC_FUNC_MALLOC
AC_FUNC_REALLOC
AC_TYPE_SIGNAL
AC_FUNC_STAT
AC_CHECK_FUNCS([memmove strncasecmp strstr strdup])

CFLAGS="${CFLAGS} -std=c99"
AC_MSG_CHECKING([whether gcc -std=c99 option works])
AC_TRY_COMPILE(AC_INCLUDES_DEFAULT, [char *a; a = strdup("foo"); int i = 0; i++; // C99],
   AC_MSG_RESULT([yes]),
   AC_MSG_ERROR([htop is written in C99. A newer version of gcc is required.]))

PROCDIR=/proc
AC_ARG_WITH(proc, [  --with-proc=DIR      Location of a Linux-compatible proc filesystem (default=/proc).],

   if test -n "$withval"; then
      AC_DEFINE_UNQUOTED(PROCDIR, "$withval", [Path of proc filesystem])
   fi,
   AC_DEFINE(PROCDIR, "/proc", [Path of proc filesystem]))

AC_CHECK_FILE(/proc/stat,,AC_MSG_ERROR(Cannot find /proc/stat. Make sure you have a Linux-compatible /proc filesystem mounted. See the file README for help.))
AC_CHECK_FILE(/proc/meminfo,,AC_MSG_ERROR(Cannot find /proc/meminfo. Make sure you have a Linux-compatible /proc filesystem mounted. See the file README for help.))

AC_CONFIG_FILES([Makefile])
AC_OUTPUT