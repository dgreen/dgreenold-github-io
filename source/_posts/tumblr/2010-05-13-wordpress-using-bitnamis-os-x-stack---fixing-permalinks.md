---
layout: post
title: WordPress using Bitnami's OS X Stack - fixing permalinks
tags: 
---
Looking at Wordpress for a variety of reasons since IEEE's EWH effort has
decided to go with it.

[Bitnami has a Wordpress application][1] for installing OS X that I chose for
easy evaluation (or so I thought).

Things initially worked fine but switching to "friendly permalinks" brought up
404 error messages for all content. After some googling, and reading the
Apache error log, changed

/Applications/wordpress-2.9.2-0/apps/wordpress/conf/wordpress.conf to contain

    Alias /wordpress/ "/Applications/wordpress-2.9.2-0/apps/wordpress/htdocs/"
    Alias /wordpress "/Applications/wordpress-2.9.2-0/apps/wordpress/htdocs"

    <Directory "/Applications/wordpress-2.9.2-0/apps/wordpress/htdocs">
        Options Indexes MultiViews FollowSymLinks
        AllowOverride all
        Order allow,deny
        Allow from all
    </Directory>

Now things are working although it appears that the Bitnami Stack is a single
blog version of WordPress. I suspect I will gain additional insight as my
evaluation continues.

[1]: http://bitnami.org/stack/wordpress

