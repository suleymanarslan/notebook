# Printers

Required packages:

* CUPS
* Avahi

Install:

* [Find New Printer](http://localhost:631/admin/)
* Search its hostname in Avahi. E.g `sudo avahi-browse -alr | grep -i "Printer-name"`
* Resolve the hostname. E.g `avahi-resolve-host-name 'Example.local'`
* Update connection to HTTP and given IP
