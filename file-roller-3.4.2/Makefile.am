ACLOCAL_AMFLAGS=-I m4

if ENABLE_ATHENA_ACTIONS
ATHENA = athena
else
ATHENA =
endif

SUBDIRS =		\
	copy-n-paste	\
	data		\
	src		\
	help		\
	$(ATHENA)	\
	po

distcleancheck_listfiles = find . -type f -print | grep -v 'omf\.out'

distuninstallcheck_listfiles = find . -type f -print | grep -v '^\./var/scrollkeeper' | grep -v 'omf' | grep -v 'figures'


EXTRA_DIST = 			\
	AUTHORS			\
	HACKING			\
	MAINTAINERS		\
	NEWS			\
	README			\
	file-roller.spec	\
	file-roller.spec.in	\
	intltool-merge.in	\
	intltool-update.in	\
	intltool-extract.in	\
	gnome-doc-utils.make

DISTCLEANFILES =                        \
	gnome-doc-utils.make		\
	po/.intltool-merge-cache        \
	intltool-extract                \
	intltool-merge                  \
	intltool-update

DISTCHECK_CONFIGURE_FLAGS = --disable-scrollkeeper

MAINTAINERCLEANFILES = \
	$(srcdir)/ABOUT-NLS \
	$(srcdir)/INSTALL \
	$(srcdir)/aclocal.m4 \
	$(srcdir)/autoscan.log \
	$(srcdir)/compile \
	$(srcdir)/config.guess \
	$(srcdir)/config.h.in \
	$(srcdir)/config.rpath \
	$(srcdir)/config.sub \
	$(srcdir)/configure.scan \
	$(srcdir)/depcomp \
 	$(srcdir)/install-sh \
	$(srcdir)/ltmain.sh \
	$(srcdir)/m4 \
	$(srcdir)/missing \
	$(srcdir)/mkinstalldirs \
	$(srcdir)/omf.make \
	$(srcdir)/xmldocs.make \
	$(srcdir)/gtk-doc.make \
	$(srcdir)/ChangeLog \
	$(srcdir)/po/Makevars.template \
	$(srcdir)/po/Rules-quot \
	$(srcdir)/po/boldquot.sed \
	$(srcdir)/po/en@boldquot.header \
	$(srcdir)/po/en@quot.header \
	$(srcdir)/po/insert-header.sin \
	$(srcdir)/po/quot.sed \
	$(srcdir)/po/remove-potcdate.sin \
	`find "$(srcdir)" -type f -name Makefile.in -print`

GITIGNOREFILES = build .cdt* .cproject .project .settings/

CLEANFILES = ChangeLog

# Build ChangeLog from GIT history
ChangeLog:
	@echo Creating $@
	@if test -d $(top_srcdir)/.git; then \
		(GIT_DIR=$(top_srcdir)/.git $(top_srcdir)/missing --run git log --stat -M -C --name-status  --date=short --no-color) | fmt --split-only > $@.tmp \
		 && mv -f $@.tmp $@ \
		 || ($(RM) $@.tmp; \
		     echo Failed to generate ChangeLog, your ChangeLog may be outdated >&2; \
		     (test -f $@ || echo git-log is required to generate this file >> $@)); \
	else \
		test -f $@ || \
		(echo A git checkout and git-log is required to generate ChangeLog >&2 && \
		echo A git checkout and git-log is required to generate this file >> $@); \
	fi

dist: ChangeLog

.PHONY: ChangeLog

-include $(top_srcdir)/git.mk
