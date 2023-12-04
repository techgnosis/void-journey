you can run dbus yourself

dbus-daemon is the executable

you have to set DBUS_SESSION_BUS_ADDRESS afterwards or programs that need dbus won't know where to find it

correct flags are

`dbus-daemon --session --fork --print-address 1`

that will print the address of the bus (some kind of socket)

so its easiest to do

`export DBUS_SESSION_BUS_ADDRESS=$(dbus-daemon --session --fork --print-address 1)`

If you export variables from a bash script, you can capture them by running `source thescript`


I don't seem to need a system bus to run sway.


https://stackoverflow.com/questions/41242460/how-to-export-dbus-session-bus-address