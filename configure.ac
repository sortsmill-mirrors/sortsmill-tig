#                                               -*- Autoconf -*-
# Process this file with autoconf to produce a configure script.

# Copyright (C) 2013 Khaled Hosny and Barry Schwartz
# This file is part of Sorts Mill TIG.
# 
# Sorts Mill TIG is free software; you can redistribute it and/or modify
# it under the terms of the GNU General Public License as published by
# the Free Software Foundation; either version 3 of the License, or
# (at your option) any later version.
# 
# Sorts Mill TIG is distributed in the hope that it will be useful,
# but WITHOUT ANY WARRANTY; without even the implied warranty of
# MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
# GNU General Public License for more details.
# 
# You should have received a copy of the GNU General Public License
# along with this program; if not, see <http://www.gnu.org/licenses/>.

AC_PREREQ([2.68])
AC_INIT([Sorts Mill TIG],
        [1.1.0],
        [http://bitbucket.org/sortsmill/sortsmill-tig/issues],
        [sortsmill-tig],
        [http://bitbucket.org/sortsmill/sortsmill-tig])

AC_CONFIG_SRCDIR([sortsmill-tig.in])

AC_CONFIG_MACRO_DIR([m4])
AC_CONFIG_AUX_DIR([config])        dnl Where things like install-sh go.
AC_CANONICAL_BUILD                 dnl On what platform are we compiling?
AC_CANONICAL_HOST                  dnl For what platform are we compiling?
AC_USE_SYSTEM_EXTENSIONS           dnl Define such macros as _GNU_SOURCE.

AM_INIT_AUTOMAKE([1.11 dist-xz -Wall -Wno-portability -Werror])

# I am going to enable silent-rules by default, so builders are
# more likely to see warnings. Use --disable-silent-rules or "make
# V=1" if you need to see the rules.
AM_SILENT_RULES([yes])

StM_ANALYZE_PACKAGE_VERSION

#--------------------------------------------------------------------------
#
# Checks for programs.

AC_PROG_AWK
AC_PROG_GREP
AC_PROG_INSTALL
AC_PROG_LN_S
AC_PROG_MAKE_SET
AC_PROG_MKDIR_P
AC_PROG_SED

StM_PROG_HELP2MAN
AM_CONDITIONAL([HAVE_HELP2MAN],[test x"${HELP2MAN}" != x])

m4_ifdef([GUILE_PROGS],[GUILE_PROGS],
         [AC_MSG_ERROR([
I could not find a usable installation of Guile.
${PACKAGE_NAME} requires Guile 2.0.x from
http://www.gnu.org/software/guile/])])

if test x"${GUILE_EFFECTIVE_VERSION}" != x"2.0"; then
   AC_MSG_WARN([
Found Guile effective version ${GUILE_EFFECTIVE_VERSION}.
${PACKAGE_NAME} is written for Guile 2.0.x
from http://www.gnu.org/software/guile/
but we will try the one we found.])
fi

#--------------------------------------------------------------------------
#
# Checks for libraries.

#--------------------------------------------------------------------------
#
# Checks for header files.

#--------------------------------------------------------------------------
#
# Checks for typedefs, structures, and compiler characteristics.

#--------------------------------------------------------------------------
#
# Checks for library functions.

#--------------------------------------------------------------------------

StM_CHANGELOGGERIZE
StM_MAKE_README([make_readme],[sortsmill-tig.1])

AC_CONFIG_FILES([Makefile])
AC_CONFIG_FILES([sortsmill-tig],[chmod +x sortsmill-tig])

AC_OUTPUT

#--------------------------------------------------------------------------
