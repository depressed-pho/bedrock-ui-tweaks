MANIFEST_SRC = manifest.json.in

MCPACK_INSTALLATION_DIRECTORY = $(MCPACK_INSTALLATION_DIRECTORY_resource)
MCPACK_FILES = \
	manifest.json \
	pack_icon.png \
	ui/inventory_screen.json \
	ui/loom_screen.json \
	ui/loom_screen_pocket.json \
	ui/play_screen.json \
	ui/start_screen.json \
	ui/stonecutter_screen.json \
	ui/ui_template_tabs.json

EXTRA_DIST= \
	ui-tweaks.svg

# Strip comments from JSON.
%.json: %.json.in Makefile
	$(AM_V_GEN)
	$(AM_V_at)set -eu; \
	$(MKDIR_P) "$(dir $@)"; \
	$(SED) \
		-e "/^[ 	]*\/\//d" \
		< $< > $@.tmp; \
	mv $@.tmp $@

pack_icon.png: ui-tweaks.svg
	$(AM_V_GEN)
	$(AM_V_at)$(INKSCAPE) -o "$@" --export-width=128 --export-height=128 "$<"

CLEANFILES=
noinst_DATA=
include $(top_srcdir)/am/manifest.am
include $(top_srcdir)/am/mcpack.am
