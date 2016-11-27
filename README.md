Fail2map
========

### Changes on this fork:

- Include all JavaScript files from http://leafletjs.com/ and https://jquery.com/ to the file system structure of fail2map
- Change from http://www.telize.com (the public API will permanently shut down) to http://ip-api.com
- Fix some problems with UTF-8 inside the fail2map.py python script
- **Shell/Bash script for MERGE various ''places.geojson'' files to one** - (`fail2map-merge.sh`)

Fail2map is a map generator for [fail2ban](http://www.fail2ban.org).
It displays banned IP on a world map. Adding IP is done automagically through a fail2ban *action*.

Fail2map is based on [backpack](https://github.com/maximeh/backpack) by Maxime Hadjinlian.

### Try the [example](http://mvonthron.github.io/fail2map).

Installing fail2map and fail2ban action
---------------------------------------

##### See following Link for an installation description (sorry, only available in german language):
- [DokuWiki - Klaus Tachtler - fail2map](http://www.dokuwiki.tachtler.net/doku.php?id=tachtler:fail2map)

##### or follow the standard installation instructions here:

1. Place fail2map in the desired path of your web server

        git clone https://github.com/mvonthron/fail2map ~/public_html/fail2map

2. Edit `fail2map-action.conf` with the correct path for fail2map.py

        fail2map-action.conf:20     fail2map = cd /home/<USER>/public_html/fail2map && python fail2map.py

3. Move/copy/link `fail2map-action.conf` to fail2ban actions folder (usually `/etc/fail2ban/action.d/`)
4. Add the action to your `jail.conf` or `jail.local`

        # The simplest action to take: ban only
        action_ = %(banaction)s[name=%(__name__)s, port="%(port)s", protocol="%(protocol)s", chain="%(chain)s"]
                  fail2map-action

5. (Optional) Change the tile provider in js/maps.js line 45:

        baseLayer = L.tileLayer.provider('Thunderforest.Landscape', ...
                                            ^= select any provider listed at http://leaflet-extras.github.io/leaflet-providers/preview/ 
                                            
Notes
-----
* OpenStreetMap tiles providers list by https://github.com/leaflet-extras/leaflet-providers
* Map API from [leaflet](http://www.leafletjs.com)
* IP geolocation is provided by [Telize](http://http://www.telize.com/). It's free, but not very accurate. If you want to achieve high precision, you may want a paid account at maxmind.com and change `GEOIP_API` in `fail2map.py`.



----
2015, Manuel Vonthron <manuel.vonthron@acadis.org>

2016, Klaus Tachtler <klaus@tachtler.net>

