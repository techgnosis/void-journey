`/etc/sv/` contains the services, packaged as directories with expected named files in them

`/etc/runit/runsvdir/` contains symlinks to directories in `/etc/sv` and those symlinks are launched at startup

`sv` cannot run a service without a corresponding symlink in `/etc/runit/runsvdir`

`/var/service` is a symlink to `/etc/runit/runsvdir`

All services are launched by a command called `runsv`