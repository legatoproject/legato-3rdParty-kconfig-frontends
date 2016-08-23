ACLOCAL_AMFLAGS = -I scripts/.autostuff/m4
MAKEFLAGS = $(SILENT_MAKEFLAGS)

SUBDIRS = libs frontends
EXTRA_DIST = .version

bin_PROGRAMS =
bin_SCRIPTS =
dist_bin_SCRIPTS =

CLEAN_FILES =

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
