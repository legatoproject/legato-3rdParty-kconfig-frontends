ACLOCAL_AMFLAGS = -I scripts/.autostuff/m4
MAKEFLAGS = $(SILENT_MAKEFLAGS)

SUBDIRS = libs
EXTRA_DIST = .version

bin_PROGRAMS =
bin_SCRIPTS =
dist_bin_SCRIPTS =

CLEAN_FILES =
BUILT_SOURCES =

#===============================================================================
# Docs
dist_doc_DATA = \
	docs/kconfig-language.txt \
	docs/kconfig.txt

#===============================================================================
# Frontends

#--------------------------
# kconfig meta frontend
if COND_kconfig

bin_SCRIPTS += frontends/kconfig

frontends/kconfig: frontends/kconfig.in
	$(AM_V_GEN)$(SED) -e 's/@KCFG_LIST@/$(kcfg_list)/g' \
		$< >$@
	@chmod +x $@

EXTRA_DIST += frontends/kconfig.in

endif # COND_kconfig

#--------------------------
# conf frontend
if COND_conf

bin_PROGRAMS += frontends/conf/kconfig-conf

frontends_conf_kconfig_conf_SOURCES = frontends/conf/conf.c
frontends_conf_kconfig_conf_CPPFLAGS = \
	$(AM_CPPFLAGS) \
	$(intl_CPPFLAGS) \
	-I$(top_srcdir)/libs/parser
frontends_conf_kconfig_conf_CFLAGS = \
	$(AM_CFLAGS) \
	$(kf_CFLAGS)
frontends_conf_kconfig_conf_LDADD = \
	$(top_builddir)/libs/parser/libkconfig-parser.la \
	$(intl_LIBS) \
	$(conf_EXTRA_LIBS)

endif # COND_conf

#--------------------------
# mconf frontend
if COND_mconf

bin_PROGRAMS += frontends/mconf/kconfig-mconf

frontends_mconf_kconfig_mconf_SOURCES = frontends/mconf/mconf.c
frontends_mconf_kconfig_mconf_CPPFLAGS = \
	$(AM_CPPFLAGS) \
	$(ncurses_mconf_CPPFLAGS) \
	$(intl_CPPFLAGS) \
	-I$(top_srcdir)/libs \
	-I$(top_srcdir)/libs/parser
frontends_mconf_kconfig_mconf_CFLAGS = \
	$(AM_CFLAGS) \
	$(kf_CFLAGS)
frontends_mconf_kconfig_mconf_LDADD = \
	$(top_builddir)/libs/parser/libkconfig-parser.la \
	$(top_builddir)/libs/lxdialog/libkconfig-lxdialog.a \
	$(intl_LIBS) $(ncurses_LIBS) $(mconf_EXTRA_LIBS)

endif # COND_mconf

#--------------------------
# nconf frontend
if COND_nconf

bin_PROGRAMS += frontends/nconf/kconfig-nconf

frontends_nconf_kconfig_nconf_SOURCES = \
	frontends/nconf/nconf.c \
	frontends/nconf/nconf.gui.c \
	frontends/nconf/nconf.h
frontends_nconf_kconfig_nconf_CPPFLAGS = \
	$(AM_CPPFLAGS) \
	$(intl_CPPFLAGS) \
	$(ncurses_nconf_CPPFLAGS) \
	-I$(top_srcdir)/libs/parser
frontends_nconf_kconfig_nconf_CFLAGS = \
	$(AM_CFLAGS) \
	$(kf_CFLAGS)
frontends_nconf_kconfig_nconf_LDADD = \
	$(top_builddir)/libs/parser/libkconfig-parser.la \
	$(intl_LIBS) $(ncurses_panel_menu_LIBS) $(ncurses_LIBS) \
	$(nconf_EXTRA_LIBS)

endif # COND_nconf

#--------------------------
# gconf frontend
if COND_gconf

bin_PROGRAMS += frontends/gconf/kconfig-gconf

frontends_gconf_kconfig_gconf_SOURCES = \
	frontends/gconf/gconf.c \
	frontends/gconf/gconf.glade
frontends_gconf_kconfig_gconf_CPPFLAGS = \
	$(AM_CPPFLAGS) \
	$(intl_CPPFLAGS) \
	-I$(top_srcdir)/libs/parser \
	-I$(top_builddir)/libs/images \
	-DGUI_PATH='"$(pkgdatadir)/gconf.glade"'
frontends_gconf_kconfig_gconf_CFLAGS = \
	$(AM_CFLAGS) \
	$(kf_CFLAGS) \
	$(gtk_CFLAGS)
frontends_gconf_kconfig_gconf_LDADD = \
	$(top_builddir)/libs/parser/libkconfig-parser.la \
	$(top_builddir)/libs/images/libkconfig-images.a \
	$(intl_LIBS) \
	$(gtk_LIBS) \
	$(gconf_EXTRA_LIBS)
frontends_gconf_kconfig_gconfdir = $(pkgdatadir)
frontends_gconf_kconfig_gconf_DATA = frontends/gconf/gconf.glade

EXTRA_DIST += frontends/gconf/gconf.c.patch

endif # COND_gconf

#--------------------------
# gconf frontend
if COND_qconf

bin_PROGRAMS += frontends/qconf/kconfig-qconf

frontends_qconf_kconfig_qconf_SOURCES = \
	frontends/qconf/qconf.cc \
	frontends/qconf/qconf.h
BUILT_SOURCES += frontends/qconf/qconf.moc
frontends_qconf_kconfig_qconf_CPPFLAGS = \
	$(AM_CPPFLAGS) \
	$(intl_CPPFLAGS) \
	-I$(top_srcdir)/libs/parser \
	-I$(top_builddir)/libs/images
frontends_qconf_kconfig_qconf_CXXFLAGS = \
	$(AM_CXXFLAGS) \
	$(kf_CFLAGS) \
	$(Qt5_CFLAGS) \
	-fPIC
frontends_qconf_kconfig_qconf_LDADD = \
	$(top_builddir)/libs/parser/libkconfig-parser.la \
	$(top_builddir)/libs/images/libkconfig-images.a \
	$(intl_LIBS) $(Qt5_LIBS) $(qconf_EXTRA_LIBS)

AM_V_MOC = $(AM_V_MOC_$(V))
AM_V_MOC_ = $(AM_V_MOC_$(AM_DEFAULT_VERBOSITY))
AM_V_MOC_0 = @echo "  MOC     " $@;

.h.moc:
	$(AM_V_MOC)$(MOC) -i $< -o $@

CLEAN_FILES += frontends/qconf/qconf.moc
EXTRA_DIST += frontends/qconf/qconf.cc.patch

endif # COND_qconf

#===============================================================================
# Utilities
if COND_utils

bin_SCRIPTS += utils/kconfig-tweak
dist_bin_SCRIPTS += utils/kconfig-diff utils/kconfig-merge

if COND_utils_gettext
MAYBE_utils_gettext = utils/kconfig-gettext
endif
bin_PROGRAMS += $(MAYBE_utils_gettext)

utils_kconfig_gettext_SOURCES = utils/gettext.c
utils_kconfig_gettext_CPPFLAGS = \
	$(AM_CPPFLAGS) \
	-I$(top_srcdir)/libs/parser
utils_kconfig_gettext_CFLAGS = \
	$(AM_CFLAGS) \
	$(kf_CFLAGS)
utils_kconfig_gettext_LDADD = \
	$(top_builddir)/libs/parser/libkconfig-parser.la \
	$(intl_LIBS)

CLEAN_FILES += utils/kconfig-tweak
EXTRA_DIST += \
	utils/kconfig-tweak.in \
	utils/kconfig-tweak.in.patch

utils/kconfig-tweak: utils/kconfig-tweak.in
	$(AM_V_GEN)$(SED) -e "s/@CONFIG_@/$(config_prefix)/g" \
		$< >$@
	@chmod +x $@

endif # COND_utils

#===============================================================================
# Misc. scripts
EXTRA_DIST += \
	scripts/ksync.sh \
	scripts/ksync.list \
	scripts/version.sh
