# -*- tab-width: 4 -*-

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

ACLOCAL_AMFLAGS = -I m4 --install

aclocaldir = ${datadir}/aclocal

bin_SCRIPTS =
dist_aclocal_DATA =
man_MANS =
CLEANFILES =
MOSTLYCLEANFILES =

bin_SCRIPTS += sortsmill-tig
dist_aclocal_DATA += sortsmill-tig.m4

if HAVE_HELP2MAN

man_MANS += sortsmill-tig.1
CLEANFILES += sortsmill-tig.1

sortsmill-tig.1: sortsmill-tig
	$(HELP2MAN) --no-info --output=$@					\
		--name='Sorts Mill Type Inspector Generator'	\
	 	--source='Sorts Mill' ./sortsmill-tig

endif HAVE_HELP2MAN

#--------------------------------------------------------------------------
# Automatic ChangeLog generation at `make dist', if one has
# sortsmill-changelogger.

dist-hook: dist-changelog
@dist_changelog_rules@

#--------------------------------------------------------------------------
#
# ‘make readme’ regenerates the README file. This target is meant for
# developers and requires groff.

PACKAGE_README = $(srcdir)/README
@make_readme@

#--------------------------------------------------------------------------
