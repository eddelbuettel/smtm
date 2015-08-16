
#    Makefile for smtm 
#    Copyright (C) 1999 - 2005 Dirk Eddelbuettel <edd@debian.org>
#
#    This program is free software; you can redistribute it and/or modify
#    it under the terms of the GNU General Public License as published by
#    the Free Software Foundation; either version 2 of the License, or
#    (at your option) any later version.
#
#    This program is distributed in the hope that it will be useful,
#    but WITHOUT ANY WARRANTY; without even the implied warranty of
#    MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
#    GNU General Public License for more details.
#
#    You should have received a copy of the GNU General Public License
#    along with this program; if not, write to the Free Software
#    Foundation, Inc., 675 Mass Ave, Cambridge, MA 02139, USA.

file= 		smtm
version:=	$(shell pwd | cut -d- -f2)

prefix=		/usr/local
mandir=		$(prefix)/share/man/man1
bindir=		$(prefix)/bin

all:		$(file)

$(file):
ifeq ($(shell hostname --fqdn),sonny.eddelbuettel.com)
		@echo "Copying freshest source file"
		cp -afv $(HOME)/progs/perl-tk/smtm/$(file).pl $(file) 
		@echo "Setting to release version " ${version}
		perl -p -i -e "s/version = \".*\";/version = \""$(version)"\";/" $(file)
		@chmod 755 $(file)
endif
		@true

install:	$(file) $(file).1
		install -p    -m 0755 $(file)     $(bindir)/.
		install -p -D -m 0755 $(file).1   $(mandir)/$(file).1

$(file).html:	$(file)
		pod2html --flush $<  > $@
		-rm -f pod2html-itemcache pod2html-dircache

$(file).1:	$(file)
		pod2man $<  > $@

clean:		
		-rm -f $(file).1 *~


distclean:	clean
realclean:	clean

FILES=		$(file) $(file).html Makefile.PL COPYING BUGS README THANKS TODO \
		examples/* t/* 

dist:		$(file).html tar zip 

tar:		
		tar cvfz ../$(file)_$(version).tar.gz $(FILES)

zip:		
		zip ../$(file)_$(version).zip $(FILES)


