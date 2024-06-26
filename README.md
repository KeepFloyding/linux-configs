# Linux Configs

## Raspberry Pi OS (Bookworm)

Details can be found here: https://www.raspberrypi.com/news/bookworm-the-new-version-of-raspberry-pi-os/. 

Some notes:
* Wayfire is the compositor (uses a library called wlroots)
* Options for keyboard shortcuts amongst other things can be found in `.config/wayfire.ini`
* Panel is `wf-panel-pi`
* File Manager is `pcmanfm`
* Locking mechanism is `swaylock`
* `wlogout` can be used for a quick shutdown screen
* Some additional applications are needed such as wofi https://sr.ht/~scoopta/wofi/ (a launcher), slurp https://github.com/emersion/slurp (gives the bounding box co-ordinates determined from a mouse that is used for screenshoting) and grim (screenshoting). These can be installed as follows:

```
hg clone https://hg.sr.ht/~scoopta/wofi
cd wofi
meson setup build
ninja -C build
sudo ninja -C build install
```

Note that you need the following dependencies:

```
libwayland-dev
libgtk-3-dev
pkgconf
meson
mercurial-common
```

## Wofi

Wofi requires some configuation. See the Wofi tutorial here: https://mephisto.cc/en/tech/wofi/. I configured Super key to start wofi and to kill it. 

## Wayfire.ini

Sample wayfire config is given below. Latest up to date one is saved as file in this repo. A lot is taken from here: https://github.com/WayfireWM/wayfire/blob/master/wayfire.ini. 
Note that I configured wofi to run as `wofi --show run` and the print command to automatically go via selective screenshot. The Print button for me is `KEY_SYSRQ`. 
I also only use `fast-switcher` cause I hate the Compiz style animation in the normal switcher.



```
[command]
repeatable_binding_volume_up=KEY_VOLUMEUP
command_volume_up=wfpanelctl volumepulse volu
repeatable_binding_volume_down=KEY_VOLUMEDOWN
command_volume_down=wfpanelctl volumepulse vold
binding_mute=KEY_MUTE
command_mute=wfpanelctl volumepulse mute
binding_launcher=<super>
command_launcher=wofi --show run
binding_terminal=<super> KEY_T
command_terminal=lxterminal
binding_bluetooth=<ctrl> <alt> KEY_B
command_bluetooth=wfpanelctl bluetooth menu
binding_netman=<ctrl> <alt> KEY_W
command_netman=wfpanelctl netman menu
#binding_grim=KEY_SYSRQ
#command_grim=grim
binding_orca=<ctrl> <alt> KEY_SPACE
command_orca=gui-pkinst orca reboot
binding_quit=<ctrl> <alt> KEY_DELETE
command_quit=lxde-pi-shutdown-helper
binding_power=KEY_POWER
command_power=pwrkey

# Screenshots
# https://wayland.emersion.fr/grim/
# https://wayland.emersion.fr/slurp/
#binding_screenshot = KEY_PRINT
#command_screenshot = grim $(date '+%F_%T').webp
binding_screenshot_interactive = KEY_SYSRQ
command_screenshot_interactive = slurp | grim -g -

[input-device:10-0038 generic ft5x06 (79)]
output=DSI-1

[input-device:6-0038 generic ft5x06 (79)]
output=DSI-1

[input-device:4-0038 generic ft5x06 (79)]
output=DSI-2

[input-device:10-0038 generic ft5x06 (00)]
output=DSI-1

[input-device:6-0038 generic ft5x06 (00)]
output=DSI-1

[input-device:4-0038 generic ft5x06 (00)]
output=DSI-2

[input]
xkb_model=pc105
xkb_layout=gb
xkb_variant=
kb_repeat_delay=400
kb_repeat_rate=40
mouse_cursor_speed=0
left_handed_mode=false

# Windows ──────────────────────────────────────────────────────────────────────

# Actions related to window management functionalities.
#
# Example configuration:
#
# [wm-actions]
# toggle_fullscreen = <super> KEY_F
# toggle_always_on_top = <super> KEY_X
# toggle_sticky = <super> <shift> KEY_X

# Position the windows in certain regions of the output.
[grid]
#
# ⇱ ↑ ⇲   │ 7 8 9
# ← f →   │ 4 5 6
# ⇱ ↓ ⇲ d │ 1 2 3 0
# ‾   ‾
slot_bl = <super> KEY_KP1
slot_b = <super> KEY_KP2
slot_br = <super> KEY_KP3
slot_l = <super> KEY_LEFT | <super> KEY_KP4
slot_c = <super> KEY_UP | <super> KEY_KP5
slot_r = <super> KEY_RIGHT | <super> KEY_KP6
slot_tl = <super> KEY_KP7
slot_t = <super> KEY_KP8
slot_tr = <super> KEY_KP9
# Restore default.
restore = <super> KEY_DOWN | <super> KEY_KP0

# Change active window with an animation.
[switcher]
next_view = <alt> KEY_TAB
prev_view = <alt> <shift> KEY_TAB

# Simple active window switcher.
[fast-switcher]
activate = <alt> KEY_ESC
```


