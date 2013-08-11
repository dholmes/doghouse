# Questions to Answer

- What could be better than Apache + mod_php?
- What does php-fpm look like?
- How can it help Apache be better?
- What kind of extra features are in php-fpm?
- Does it work with APM for "Opcode caching"?
- What is Nginix?

# Apache mod_php
- (Image of Browser + Apache w/ mod_php + scripts ) 
- (Drill into Apache and show list of processes w/php loaded in )
- Apache needs to be running in "pre-fork" mode with mod_php.  This means each httpd process can only handle one http request at a time, and must have php loaded in memory even if it's not going to do anything

# php-fpm
- "What if you could pull out the php so apache didn't have to worry about it?"
- ("Same" image as before of httpd but replacing with php process)
- (Now pull back out to "same" image with Browser + Apache + php-fpm )
   Now Apache can be changed to use it's threaded MPM worker.

Why is this better?

* Apache gets to do what Apache knows best--serving web content
* PHP becomes a service of flexible, restart-able, pools
* No worries about "thread safety" no matter what PHP modules you run
* php-fpm can create php-specific logging, customized environments and resource allocation per pool, different user/groups per pool, etc.
* Available memory can be more precisely controlled to your traffic / resources available

Look at a php-fpm configuration
Things to show:
    # ps -ef of a couple of different pools running as different users
    # diving into the config of a pool showing:
        * name
        * listen
        * permissions
        * user/group
        * resource limits
        * php environment settings


Connecting Apache to your php-fpm pools with mod_fastcgi


Adding APM into the mix


Replacing Apache with Nginx

   

   
