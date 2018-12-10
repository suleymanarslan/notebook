# Printers

Install:

* CUPS
* Avahi

Allow your user to modify:

* vim /etc/cups/cupsd.conf
* Locate the line which says "<Limit CUPS-Add-Modify-Printer...".
* On the following line, immediately after the text "Require user @SYSTEM" 
* Add your username: `Require user @SYSTEM azer`

Find & install the printer:

* [Find New Printer](http://localhost:631/admin/)
* Search its hostname in Avahi. E.g `sudo avahi-browse -alr | grep -i "Printer-name"`
* Resolve the hostname. E.g `avahi-resolve-host-name 'Example.local'`
* Update connection to HTTP and given IP (adding `:631/ipp` at the end of the hostname)
