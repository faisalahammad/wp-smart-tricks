# WP-SMART-TRICKS
There you will found small tips and tricks to make your journey with WP smooth.

### HIDE PHP WARNINGS
##### THE SOLUTION:
If you simply set `WP_DEBUG` to `false` in your `wp-config.php` file you should be fine. __These don’t affect your site in any way.__

However, the problem is that some times the above does not work. That can happen most times on *cheap shared hosts* that force displaying PHP warnings and notices.

In that case, you can replace this line from your wp-config.php file:

```php
define('WP_DEBUG', false);
```
with this:

```php
ini_set('log_errors','On');
ini_set('display_errors','Off');
ini_set('error_reporting', E_ALL );
define('WP_DEBUG', false);
define('WP_DEBUG_LOG', true);
define('WP_DEBUG_DISPLAY', false);
// OR
@ini_set('display_errors', 0);
```
I hope that helps someone out there!

---

### FORCE REWRITE HTTP TO HTTPS
Add those 3 lines of code in `<IfModule mod_rewrite.c>` and save changes.
```
RewriteEngine On
RewriteCond %{HTTPS} !=on
RewriteRule .* https://domain.com/%{REQUEST_URI} [R,L]
```
Replace **https://domain.com/** with your domain name.

---

### INCREASE PHP MEMORY LIMIT IN WORDPRESS
First you need to edit the `wp-config.php` file on your WordPress site and add those code then **SAVE CHANGES**.
```php
define( 'WP_MEMORY_LIMIT', '256M' );
```
Setup memory limit as you need.

---

### Force HTTP to HTTPS
```
RewriteCond %{HTTPS} !on           
RewriteRule ^(.*) https://%{SERVER_NAME}/$1 [R,L]
```

---

### FORCE REDIRECT HTTP MEDIA FILE INTO HTTPS
```php
function have_https_for_media( $url ) {

    if ( is_ssl() )
        $url = str_replace( 'http://', 'https://', $url );
    return $url;

}
add_filter( 'wp_get_attachment_url', 'have_https_for_media' );
```
Add those code into Parent/Child Theme's function.php file

---

### PHPMYADMIN login page
```
http://www.yourdomainname.com:2083/3rdparty/phpMyAdmin/index.php
```