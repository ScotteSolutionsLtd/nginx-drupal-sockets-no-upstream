Configuration for Drupal running on nginx virtual hosts using php-fpm and unix sockets.
================================

The nginx website has very good documentation and anyone setting up nginx for the first time I suggest you go to the website and actually *read* the documentation links. It's so easy and so simple, when first learning I wondered if this was almost *too* easy to read and adapt. I'd recommend to maximize your nginx experience to take a total of half a day or two and read the entirety of the nginx documentation. There isn't a ton and it doesn't take long to learn the directives and how they work common sensically to serve a web page.

## Installation

For all the files in your nginx directory, replace any that are included in this package. This configuration has only been tested on CentOS 6, but isn't very operating-system dependent. There is the possibility that your install of nginx came with additional files or folders required for nginx to run properly on your server. Keep those, just replace those files included here.

Using this configuation the default security on Drupal files besides index.php is pretty much lock-down. To access php files other than index.php in your Drupal folder (like update.php, cron.php, etc), add a line with your IP address to ips_allowed.conf. Another option is to use HTTP Basic Authentication provided by nginx. To do so create a htpasswd.users file; in your shell type
	
	htpasswd /path/to/nginx/htpasswd.users <username>

Replace /path/to/nginx with the path to nginx on your server and <username> with the username you'd like to allow to access these files. When prompted, enter the password for this user. Then comment out line 159 in drupal7, and uncomment lines 157 and 158 to switch to using HTTP Authentication.

## Credits

I learned nginx don't really see myself going back. Code in this package is adapted, and shamelessly stolen (with some original comments) from:
# [Perusio's bleeding edge Drupal nginx config](https://github.com/perusio/drupal-with-nginx)
# [yhager's nginx Boost compatible Drupal config](https://github.com/yhager/nginx_drupal)
# assorted tutorials

## Features
While this configuration doesn't have everything in perusio's yet it is for a different setup using unix sockets. Adding virtual-host-specific features to the configuration is left as an exercise to the administrator.

	1. php-fpm unix socket support for
	2. Drupal 7 using clean URLs
	2. Multiple virtual hosts in separate small easy to manage files
	3. Basic gzip caching option(s)
	4. One file to save IP addresses of Drupal administrators allowed to visit update.php and install.php
	5. Advanced Aggregation module support [Drupal.org:](http://drupal.org/project/advagg)
	6. An HTML5 template for 404 pages with an option to use Drupal instead
	7. HTTP Basic Authentication for folders; like in Apache
	8. Image hotlinking protection
	9. Decent video and audio mp4 streaming config
	10. Support for the [Filefield Nginx Progress](http://drupal.org/project/filefield_nginx_progress) module for the upload progress bar.
	11. Non-[expensive 404s](http://drupal.org/node/76824 "Expensive 404s issue")
	12. [Advanced Help](http://drupal.org/project/advanced_help) support.
	13. Security. Among other things, there is no ability to use any _pages_ other than index.php
	14. The Drupal specific headers like `X-Drupal-Cache` provided by [pressflow](https://github.com/pressflow/6) or the `X-Generator`
		header that Drupal 7 has are both **hidden**.
		
## Conclusion
While this is a work in progress, I wanted to provide my nginx config to get feedback from ninjas so to keep improving. If I had this configuration as a starting point I probably wouldn't have read the documentation on the nginx website. Maybe you won't have to, though I still recommend it. Don't use their Drupal example config, but definitely read the docs.

As of now, this readme needs the most work. Patches, comments, and all feedback is welcome. Commit authorship respected! Mainly I just want to rock a good nginx configuration. +1 open source