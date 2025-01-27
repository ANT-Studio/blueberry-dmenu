

Networkmanager-dmenu
====================

**NOTE: Python 2.x support ended as of 2019/11/13**

Manage NetworkManager connections with dmenu instead of nm-applet

Features
--------

- Connect to existing NetworkManager wifi or wired connections
- Connect to new wifi connections. Requests passphrase if required
- Connect to _existing_ VPN, Wireguard, GSM/WWAN and Bluetooth connections
- Enable/Disable wifi, WWAN, bluetooth and networking
- Launch nm-connection-editor GUI
- Support for multiple wifi adapters
- Optional Pinentry support for secure passphrase entry
- Delete existing connections
- Rescan wifi networks
- Uses notify-send for notifications if available

License
-------

- MIT

Requirements
------------

1. Python 3.2+
2. NetworkManager
3. Dmenu. Basic support is included for Rofi_, but most Rofi
   configuration/theming should be done via Xresources or Rofi themes. The
   `Suckless password patch`_ is supported if desired.
4. Python gobject (PyGObject, python-gobject, etc.)
5. (Debian/Ubuntu based distros) libnm-util-dev and gir1.2-nm-1.0 (you have to
   explicitly install the latter on Debian Sid)
6. (optional) The network-manager-applet package (in order to launch the GUI
   connection editor, if desired. The nm-applet does _not_ need to be started.)
7. (optional) Pinentry. Make sure to set which flavor of pinentry command to use
   in the config file.
8. (optional) ModemManager for WWAN support.
9. (optional) notify-send for notifications (connected, disconnected, etc.)

Installation
------------

- Copy script somewhere in $PATH OR

  - Archlinux: `AUR package`_ OR
  - Gentoo: `Woomy Overlay`_

- Set your dmenu_command in config.ini if it's not 'dmenu' (for example
  dmenu_run or rofi). The alternate command should still respect the -l, -p and
  -i flags.
- To customize dmenu appearance, copy config.ini.example to
  ~/.config/networkmanager-dmenu/config.ini and edit.
- If using dmenu for passphrase entry (pinentry not set), dmenu options in the
  [dmenu_passphrase] section of config.ini will override those in [dmenu] so you
  can, for example, set the normal foreground and background colors to be the
  same to obscure the passphrase. The `Suckless password patch`_ `-P` option is
  supported if that patch is installed.
- Set default terminal (xterm, urxvtc, etc.) command in config.ini if desired.
- If using Rofi, you can try some of the command line options in config.ini or
  set them using the `dmenu_command` setting, but I haven't tested most of them
  so I'd suggest configuring via .Xresources where possible. 
- Saved connections can be listed if desired. Set `list_saved = True` under
  `[dmenu]` in config.ini. If set to `False`, saved connections are still
  accessible under a "Saved connections" sub-menu.
- If desired, copy the networkmanager_dmenu.desktop to /usr/share/applications
  or ~/.local/share/applications.
- If you want to run the script as $USER instead of ROOT, set `PolicyKit
  permissions`_. The script is usable for connecting to pre-existing connections
  without setting these, but you won't be able to enable/disable networking or
  add new connections.

Usage
-----

- Run script or bind to keystroke combination
- If desired, dmenu or Rofi options can be passed on the command line instead of
  or in addition to the config file. These will override options in the config
  file.

.. _PolicyKit permissions: https://wiki.archlinux.org/index.php/NetworkManager#Set_up_PolicyKit_permissions
.. _AUR Package: https://aur.archlinux.org/packages/networkmanager-dmenu-git/
.. _Woomy Overlay: https://github.com/Woomy4680-exe/Woomy-overlay 
.. _Rofi: https://davedavenport.github.io/rofi/
.. _Suckless password patch: https://tools.suckless.org/dmenu/patches/password/
