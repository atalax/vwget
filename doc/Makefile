# Generated automatically from Makefile.in by configure.
# Makefile for `wget' utility
# Copyright (C) 1995, 1996, 1997 Free Software Foundation, Inc.

# This program is free software; you can redistribute it and/or modify
# it under the terms of the GNU General Public License as published by
# the Free Software Foundation; either version 2 of the License, or
# (at your option) any later version.

# This program is distributed in the hope that it will be useful,
# but WITHOUT ANY WARRANTY; without even the implied warranty of
# MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
# GNU General Public License for more details.

# You should have received a copy of the GNU General Public License
# along with this program; if not, write to the Free Software
# Foundation, Inc., 675 Mass Ave, Cambridge, MA 02139, USA.

#
# Version: 1.5.2
#

SHELL = /bin/sh

# Program to format Texinfo source into Info files.
MAKEINFO = emacs -batch -q -no-site-file -eval '(find-file "$(srcdir)/wget.texi")' -l texinfmt -f texinfo-format-buffer -f save-buffer
# Program to format Texinfo source into DVI files.
TEXI2DVI = texi2dvi
# Program to convert DVI files to PostScript
DVIPS = dvips -D 300
# Program to convert texinfo files to html
TEXI2HTML = texi2html -expandinfo -split_chapter

top_srcdir = ..
srcdir     = .

prefix     = /usr/local
infodir    = ${prefix}/info
mandir     = ${prefix}/man
manext     = 1
sysconfdir = ${prefix}/etc

INSTALL      = /boot/apps/GeekGadgets/bin/install -c
INSTALL_DATA = ${INSTALL} -m 644
RM = rm -f

MAN        = wget.$(manext)
WGETRC     = $(sysconfdir)/wgetrc

#
# Dependencies for building
#

all: wget.info # wget.cat

everything: all wget_us.ps wget_a4.ps wget_toc.html

wget.info: wget.texi
	-$(MAKEINFO)

#wget.cat: $(MAN)
#	nroff -man $(srcdir)/$(MAN) > wget.cat

dvi: wget.dvi

wget.dvi: wget.texi
	$(TEXI2DVI) $(srcdir)/wget.texi

wget_us.ps: wget.dvi
	$(DVIPS) -t letter -o $@ wget.dvi

wget_a4.ps: wget.dvi
	$(DVIPS) -t a4 -o $@ wget.dvi

wget_toc.html: wget.texi
	$(TEXI2HTML) $(srcdir)/wget.texi

#
# Dependencies for installing
#

# install all the documentation
install: install.info install.wgetrc # install.man

# uninstall all the documentation
uninstall: uninstall.info # uninstall.man

# install info pages, creating install directory if necessary
install.info: wget.info
	$(top_srcdir)/mkinstalldirs $(infodir)
	-for file in $(srcdir)/wget.info $(srcdir)/wget.info-*[0-9]; do \
	   test -f "$$file" && $(INSTALL_DATA) $$file $(infodir) ; \
	done

# install man page, creating install directory if necessary
#install.man:
#	$(top_srcdir)/mkinstalldirs $(mandir)/man$(manext)
#	$(INSTALL_DATA) $(srcdir)/$(MAN) $(mandir)/man$(manext)/$(MAN)

# install sample.wgetrc
install.wgetrc:
	$(top_srcdir)/mkinstalldirs $(sysconfdir)
	@if test -f $(WGETRC); then \
	  if cmp -s $(srcdir)/sample.wgetrc $(WGETRC); then echo ""; \
	     else \
	     echo ' $(INSTALL_DATA) $(srcdir)/sample.wgetrc $(WGETRC).new'; \
	     $(INSTALL_DATA) $(srcdir)/sample.wgetrc $(WGETRC).new; \
	     echo "WARNING: File \`$(WGETRC)' already exists and is spared."; \
	     echo "         You might want to consider \`$(WGETRC).new',"; \
	     echo "         and merge both into \`$(WGETRC)', for the best."; \
	  fi; \
	else \
	  $(INSTALL_DATA) $(srcdir)/sample.wgetrc $(WGETRC); \
	fi

# uninstall info pages
uninstall.info:
	$(RM) $(infodir)/wget.info*

# uninstall man page
#uninstall.man:
#	$(RM) $(mandir)/man$(manext)/$(MAN)

#
# Dependencies for cleanup
#

clean:
	$(RM) *~ *.bak *.cat *.html
	$(RM) *.dvi *.aux *.cp *.cps *.fn *.toc *.tp *.vr *.ps *.ky *.pg *.log

distclean: clean
	$(RM) Makefile

realclean: distclean
	$(RM) wget.info*

#
# Dependencies for maintenance
#

subdir = doc

Makefile: Makefile.in ../config.status
	cd .. && CONFIG_FILES=$(subdir)/$@ CONFIG_HEADERS= ./config.status
