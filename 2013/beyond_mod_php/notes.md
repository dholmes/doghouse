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

# Why is this better?

- Apache gets to do what Apache knows best--serving web content
- PHP becomes a service of flexible, restart-able, pools
- No worries about "thread safety" no matter what PHP modules you run
- a php-fpm pool can have completly seperate
  - logging
  - customized environments
  - resource allocation
  - user/groups
- Available memory can be more precisely controlled to your traffic / resources available
- One php pool could be restricted from updating php scripts or even reading other directories

# Look at a php-fpm configuration
  Things to show:
  - ps -ef of a couple of different pools running as different users
  - diving into the config of a pool showing:
    - name
    - listen
    - permissions
    - user/group
    - resource limits
    - php environment settings


# "The missing Link" FastCGI
- FastCGI is the interface php-fpm expects to use with the Web Server
- For Apache, these are mainly
  - mod_fcgi
    - newer bigger brother, but duplicates a LOT of the functionality in php-fpm
    - good choice if you are running different versions of PHP (including 4)
    - can be used with mod_suexec to spawn non-php-fpm instances of PHP
    - Comes with most Package Managers
  - mod_fastcgi
    - Much simplier to configure
    - Doesn't manage it's own pool--perfect for php-fpm
    - May not come in your Package Manager (Centos/REL) but easy to build
    - is simply a FastCGI interface
    - We will focus on this one for today

# Connecting Apache to your php-fpm pools with mod_fastcgi
- (Maybe the diagram but with mod_fastcgi added?)
- Show a simple mod_php style virtual host file
- Add the directives for processing php
- Make sure to show how it demonstrates ONLY .php files will be run as PHP
- (Show diagram again and stop for questions


# Kicking up the heat
- Adding an Opcode Cache
- Logging Slow PHP requests
- Replacing Apache?

## Adding an Opcode Cache
- Full stack frameworks are big
- Wordpress is big
- Drupal is big
- 100+ php scripts need to be compiled per requests
- php's compiler is FREAKY FAST
- But still, that's a lot of compiling
## Opcode Caching Options
- Zend's Opcache - Recently Open Sourced, built into PHP 5.5
- APC - 
- 
# Zend's Opcache in PHP 5.5
  Looking at [Chris Jones' post](https://blogs.oracle.com/opal/entry/using_php_5_5_s), in 5.5 is should be as easy as :
  ```ini
   ; Adding the extension ...
   zend_extension=opcache.so
   ; and turning it on...
   opcache.enable=On
  ```



Replacing Apache with Nginx

   

   
