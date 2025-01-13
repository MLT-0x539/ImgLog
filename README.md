### ImgLog:
PHP dynamic image IP logger utilizing htaccess mod_rewrite. Allows you to log IP addresses via a JPG file without direct user interaction required. Can also be used for bypassing cloudflare and other similar DNS-Based WAF or DDoS protection products by revealing the real backend IP address.


### Requirements:
- Web-server (specifically Apache) with PHP installed
- .htaccess file correctly configured with a mod_rewrite rule


### Setup:
- Copy the .htaccess file found within this repo and have it stored in your webroot directory (/var/www/html)
- Add a valid JPG image to your webroot directory
- Either name the JPG image as "lol.jpg" or modify the .htaccess file to replace "lol.jpg" with whatever image name you chose
- Link or embed the JPG to log IP addresses


### How this works:
This will trick platforms into thinking a valid image has been served, when in reality it's a dynamic image outputted by PHP's imagecreate(); function which executes some malicious code alongside the dynamic image output. Take the following scenario as an example:

- Forum board has option to specify an avatar image from a remote URL
- Link to valid JPG image on the hackers' webserver is supplied
- Forum board attempts to fetch the image, gets redirected to a PHP script
- PHP script outputs image, forum board is then tricked into thinking they've fetched a valid JPG
- Dynamic image is included as avatar, and any other PHP code runs alongside it silently.
