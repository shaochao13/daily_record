Docroot is: /usr/local/var/www

The default port has been set in /usr/local/etc/lighttpd/lighttpd.conf to 8080 so that
lighttpd can run without sudo.

To have launchd start lighttpd now and restart at login:
  brew services start lighttpd
Or, if you don't want/need a background service you can just run:
  lighttpd -f /usr/local/etc/lighttpd/lighttpd.conf