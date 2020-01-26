# Serial Connections on macOS

To make a serial connection on macOS, it can be as simple as

`screen /dev/tty[device] [baudspeed]`

For example, when I plug my usb->serial adapter into my Mac, a new device appears called `tty.usbserial-40110` and I know that my pfSense config uses `115200` baud speed, so the command I'd use is `screen /dev/tty.usbserial-40110 115200` and I magically get console output from the device!

I assume the same/similar method would work on linux.