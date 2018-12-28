MANIFEST_SRC = manifest.json.in

MCPACK_INSTALLATION_DIRECTORY = $(MCPACK_INSTALLATION_DIRECTORY_resource)
MCPACK_FILES = \
	manifest.json \
	pack_icon.png \
	ui/inventory_screen.json \
	ui/inventory_screen_pocket.json \
	ui/start_screen.json

EXTRA_DIST= \
	ui-tweaks.svg

pack_icon.png: ui-tweaks.svg
	$(AM_V_GEN)
	$(AM_V_at)$(INKSCAPE) --export-png="$@" --export-width=128 --export-height=128 "$<"

CLEANFILES=
noinst_DATA=
include $(top_srcdir)/am/manifest.am
include $(top_srcdir)/am/mcpack.am
