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

dbus has "service" files in its config. those files tell dbus how to start other services automatically. that is probably how pipewire and wireplumber and all the portal stuff gets started when i run steam

there is a lot of policy defined for the system bus that dictates what bus apps are allowed to do. session bus usually does not have any policy


https://stackoverflow.com/questions/41242460/how-to-export-dbus-session-bus-address

gdbus
dbus-send - part of dbus
dbus-monitor - part of dbus
busctl
pacman -S dbus-python

Some things that make dbus stand out
---------
Single owner "bus names". 
On-demand starting of services (service files), like starting pipewire automatically. This seems to be a big part of dbus. I'm curious how this holds up against a systemd world.
bus activation seems like a useful feature for void linux since it does not use systemd

dbus messages have a type, and types are made of a collection of primitive types, each with 1 letter identifiers

an app connected to the bus has a "bus name". you could say a connection has a bus name.
bus names can be random or "well known" bus names
unique bus names are assigned randomly and start with ":". They are unique for the lifetime of the bus
well known names are two or more dot-separated strings


bus names have "objects". and object-oriented view is this imposed by dbus.
an object has an "object path", which is of the form /some/name/here. Usually done in reverse domain name notation like 
/org/freedesktop/something
every bus name (connection) has at least one default object that represents that status of the bus name

objects have interfaces which are the APIs that objects support
an interface can have one or more "methods" and "signals"
"methods" are RPC and have return messages
"signals" are one-to-many and seem just like pub/sub. applications must register to receive signals
clients sign up for signals with "match rules"

clients can sign up for copies of method messages using match rules

each message has a header and a body

