#                                               -*- Autoconf -*-
# Process this file with autoconf to produce a configure script.

AC_PREREQ(2.59)
AC_INIT(STAT, 2.1.0, lee218@llnl.gov, The Stack Trace Analysis Tool, http://www.paradyn.org/STAT/STAT.html)
AC_COPYRIGHT([Copyright (c) 2007-2014, Lawrence Livermore National Security, LLC.])
AC_CONFIG_AUX_DIR([config])
AC_CONFIG_SRCDIR([configure.ac])
AC_CONFIG_HEADER([config.h])
AM_INIT_AUTOMAKE(STAT, 2.1.0)
AC_CANONICAL_HOST

# Checks for programs.
AC_PROG_CXX
AC_PROG_CC
AC_PROG_INSTALL
AC_DISABLE_STATIC
AC_PROG_LIBTOOL
X_AC_MPICC
X_AC_RSH

# Checks for libraries.
X_AC_TEMPORALORDERINGAPI
X_AC_GUI
X_AC_ARCH
X_AC_DEBUGLIBS
X_AC_GRAPHLIB
X_AC_FGFS
X_AC_DYSECTAPI
X_AC_LAUNCHMON
X_AC_RM_COMM
X_AC_MRNET

# Checks for header files.
AC_HEADER_STDC
AC_CHECK_HEADERS([arpa/inet.h fcntl.h stdlib.h sys/time.h unistd.h])

# Checks for typedefs, structures, and compiler characteristics.
AC_HEADER_STDBOOL
AC_C_CONST
AC_TYPE_SIZE_T
AC_HEADER_TIME
X_AC_ENABLE_DEBUG

AC_ARG_ENABLE(rpath,
  [AS_HELP_STRING([--enable-rpath],[Enable the use of rpaths, default=yes])],
  [WITH_RPATH=$enableval],
  [WITH_RPATH=yes]
)
if test "$WITH_RPATH" = "yes"
then
  LDFLAGS="$LDFLAGS $RPATH_FLAGS"
else
  LDFLAGS="$LDFLAGS"
fi
AC_ARG_ENABLE(statbench,
  [AS_HELP_STRING([--enable-statbench],[Enable the compilation of STATBench, the STAT performance emulator])],
  [WITH_STATBENCH=$enableval],
  [WITH_STATBENCH=no]
)
AM_CONDITIONAL([ENABLE_STATBENCH], [test "$WITH_STATBENCH" = yes])
AC_ARG_ENABLE(python-debug,
  [AS_HELP_STRING([--enable-python-debug],[Enable the ability to gather python script debugging])],
  [CXXFLAGS="-DPROTOTYPE_PY $CXXFLAGS"],
  [CXXFLAGS="$CXXFLAGS"]
)
AC_ARG_WITH(procspernode,
  [AS_HELP_STRING([--with-procspernode=num],[Set the maximum number of communication processes per node equal to num, defaults to 1 if not specified])],
  [AC_DEFINE_UNQUOTED([STAT_PROCS_PER_NODE], [$withval], [The max number of CPs per node])],
  [AC_DEFINE([STAT_PROCS_PER_NODE], [1], [The max number of CPs per node])]
)
AC_ARG_WITH(usagelog,
  [AS_HELP_STRING([--with-usagelog=path],[Enable usage logging and write log file to path])],
  [CXXFLAGS="$CXXFLAGS -DSTAT_USAGELOG=\\\"${withval}\\\""],
  [CXXFLAGS="$CXXFLAGS"]
)

# Checks for library functions.
AC_FUNC_MALLOC
AC_FUNC_REALLOC
AC_FUNC_SELECT_ARGTYPES
AC_FUNC_STRFTIME
AC_FUNC_VPRINTF
AC_CHECK_FUNCS([getcwd gethostname gettimeofday mkdir mkfifo pow select strdup getrlimit setrlimit])

AC_SUBST(CXX)
AC_SUBST(CXXFLAGS)
AC_SUBST(LDFLAGS)
AC_SUBST(FELIBS)
AC_SUBST(BELIBS)
AC_SUBST(MWLIBS)
AC_SUBST(MRNETCOMMNODEBIN)
AC_SUBST(DOTBINDIR)
AC_SUBST(LAUNCHMONBIN)
AC_SUBST(LAUNCHMONPREFIX)
AC_SUBST(GRAPHLIBPREFIX)
AC_SUBST(STATPYTHON)

AM_PROG_LEX
AC_PROG_YACC
AM_PATH_PYTHON

AC_CONFIG_FILES([Makefile
                 src/Makefile
                 src/dysect/Makefile
                 src/dysect/DysectAPI/Makefile
                 src/dysect/libDysectAPI/Makefile
                 src/dysect/libDysectAPI/include/Makefile
                 src/dysect/libDysectAPI/src/Makefile
                 doc/Makefile
                 doc/userguide/Makefile
                 doc/quickstart/Makefile
                 etc/Makefile
                 man/Makefile
                 examples/Makefile
                 examples/src/Makefile
                 examples/scripts/Makefile
                 examples/sessions/Makefile
                 scripts/STAT
                 scripts/dysectc
                 scripts/STATGUI
                 scripts/core_stack_merge
                 scripts/STATview
                 scripts/STATBench
                 scripts/stat-cl
                 scripts/stat-script
                 scripts/stat-gui
                 scripts/stat-view
                 scripts/stat-bench
                 scripts/Makefile])
AC_OUTPUT
