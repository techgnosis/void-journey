elogind still relies on polkitd so avoid elogind

XDG Desktop Portals rely on dbus so dbus can't be avoided
Pipewire also requires dbus so it definitely cannot be avoided
Sway seems to use dbus and that guy is a hard core minimalist so dbus must be OK

Darn. Flatpak relies on polkit


Use seatd for sway