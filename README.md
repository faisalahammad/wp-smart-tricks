# wp-smart-tricks
There you will found small tips and tricks to make your journey with WP smooth.

### Hide PHP Warnings
##### The solution:
If you simply set 'WP_DEBUG' to 'false' in your 'wp-config.php' file you should be fine. ** These don’t affect your site in any way. **

However, the problem is that some times the above does not work. That can happen most times on * cheap shared hosts * that force displaying PHP warnings and notices.

In that case, you can replace this line from your wp-config.php file:

'''
define('WP_DEBUG', false);
'''

with this:

'''
ini_set('log_errors','On');
ini_set('display_errors','Off');
ini_set('error_reporting', E_ALL );
define('WP_DEBUG', false);
define('WP_DEBUG_LOG', true);
define('WP_DEBUG_DISPLAY', false);
I hope that helps someone out there!
'''