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

ACLOCAL_AMFLAGS = -I m4

aclocaldir = ${datadir}/aclocal

bin_SCRIPTS =
dist_aclocal_DATA =
man_MANS =
EXTRA_DIST =
CLEANFILES =
MOSTLYCLEANFILES =

EXTRA_DIST += m4/gnulib-cache.m4

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
#
# Make a ChangeLog automatically, if a Git repository is available.
#
# If the developer is using Git, then the repository will be in
# '$(top_srcdir)/.git'.
#
# If the developer is using Mercurial and Hg-git, then the repository
# will be in '$(top_srcdir)/.git' or, more likely, in
# '$(top_srcdir)/.hg/git'
#
# If no Git repository is found, and a ChangeLog file that does not
# start with ‘-*- fundamental -*-’ is present, then keep it. That way
# users can run ‘make dist’ from a dist package and retain the
# ChangeLog.

dist-hook: make-changelog

.PHONY: make-changelog possible-changelog-error

make-changelog:
	@(if test -d '$(top_srcdir)/.git'; then \
		gitdir='$(top_srcdir)/.git'; \
	elif test -d '$(top_srcdir)/.hg/git'; then \
		gitdir='$(top_srcdir)/.hg/git'; \
	else \
		gitdir=''; \
	fi; \
	if test -z "$${gitdir}"; then \
		$(MAKE) $(AM_MAKEFLAGS) possible-changelog-error; \
	elif (cd "$${gitdir}" && $(GITCL) log > /dev/null 2> /dev/null); then \
		(cd "$${gitdir}" && ($(GITCL) log | $(SHELL) $(abs_top_srcdir)/config/gitlog-to-changelog)) \
			> $(distdir)/ChangeLog; \
	else \
		$(MAKE) $(AM_MAKEFLAGS) possible-changelog-error; \
	fi)

possible-changelog-error:
	@if $(AWK) -- 'NR==1 {print $0}' < $(top_srcdir)/ChangeLog | \
			$(EGREP) -q '^[[:space:]]*-\*- fundamental -\*-'; then \
		echo ""; \
		echo "********************************************************************************************"; \
		echo "***** I could not make the ChangeLog. Please install Git and try to remake the tarball *****"; \
		echo "********************************************************************************************"; \
		echo ""; \
		echo "If you do not mind, please report that the ChangeLog is missing." > $(distdir)/ChangeLog; \
		echo "Report at: https://bitbucket.org/sortsmill/sortsmill-tig/issues" >> $(distdir)/ChangeLog; \
	fi

#--------------------------------------------------------------------------
#
# ‘make readme’ regenerates the README file.
#
# This target is meant for developers.

.PHONY: readme

readme: sortsmill-tig.1
#	Turn off justification.
	echo '.na' >  README.nroff
	echo '.de ad' >> README.nroff
	echo '..' >> README.nroff
#	Turn off hyphenation.
	echo '.nh' >> README.nroff
	echo '.de hy' >> README.nroff
	echo '..' >> README.nroff
#	Copy the manpage source.
	cat sortsmill-tig.1 >> README.nroff
#	Generate the page.
	groff -man -Tascii -P -c -P -b -P -u README.nroff > $(srcdir)/README

MOSTLYCLEANFILES += README.nroff

#--------------------------------------------------------------------------
