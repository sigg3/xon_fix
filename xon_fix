#!/bin/bash
# Usage: ./xon_fix --config OR ./xon_fix --restore
# Written by Sigge Smelror (C) 2020, GNU GPL v. 3+
#
# xon_fix is free software: you can redistribute it and/or modify it
# under the terms of the GNU General Public License as published by
# the Free Software Foundation, version 3 or newer.
#
# xon_fix is distributed in the hope that it will be useful and fun,
# but WITHOUT ANY WARRANTY; without even the implied warranty of
# MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
# GNU General Public License for more details.
# URL: <https://www.gnu.org/licenses/old-licenses/gpl-2.0.txt>
#
# Submit issues and get updates @ <https://github.com/sigg3/xon_fix>
echo "This script prepares your Xonotic default config.cfg for pro play."
case "$1" in
"--restore" | "-restore" | "-r" ) do_restore=1 ;;
"--config" | "-config" ) do_restore=0 ;;
* ) echo "Usage:  ./$(basename $0) --config OR ./$(basename $0) --restore" && exit 0 ;;
esac
old_sets="$HOME/.xonotic/data/config.cfg"
bak_sets="${old_sets}.backup"

if [ -f "$old_sets" ] ; then
	if [ "$do_restore" -eq 0 ] ; then
		echo -n "Backing up $old_sets to $bak_sets .. " ; cp -f "$old_sets" "$bak_sets" ; echo "OK"
	else
		if [ -f "$bak_sets" ] ; then
			echo -n "Restoring settings from backup .. " ; cp -f "$bak_sets" "$old_sets" ; echo -e "OK\n\nDone." ; exit 0
		else
			echo "ERR: No backup in $bak_sets :(" ; exit 1
		fi
	fi
else
	echo -e "No config file in $old_sets\nPlease run Xonotic once to generate this file and try again." && exit 0
fi

read -r -n 1 -p "Use simple item flags instead of 3D models? [y/N] " prompt
case "$prompt" in
"y" | "Y" ) use_simple="1" ;;
*) use_simple="0" ;;
esac


echo -en "\nAppending fixes .. "
cat <<"END_OF_XON_SETTINGS" >> "$old_sets"
# Customizations
hud_damage_blur "0"
hud_damage "0.4"
fov "120"
playermodel "models/player/megaerebus.iqm"
cl_forceplayermodels "1"
cl_forceplayercolors "1"
cl_gentle_gibs "1"
cl_particles_alpha "0.2"
cl_particles_sparks "0"
cl_particles_blood "0"
r_coronas "0"
r_bloom "0"
gl_picmip_world "10"
gl_texturecompression "1"
cl_zoomspeed "-1"
cl_bobfall "0"
cl_bobmodel "0"
cl_bobup "0"
END_OF_XON_SETTINGS
if [ "$use_simple" -eq 1 ] ; then echo "cl_simple_items \"1\"" >> "$old_sets" ; fi
echo "OK"

# Tidy up
echo "Restore to original with: ./$(basename $0) --restore"
echo -en "\nEdit/configure using: \$ "
if [ -n "$EDITOR" ] ; then echo -n "$EDITOR" ; else echo -n "nano" ; fi
echo " $old_sets"
echo "Backup in $bak_sets."
echo "Done."
