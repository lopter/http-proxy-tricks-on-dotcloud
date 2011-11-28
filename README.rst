HTTP Proxy Tricks on DotCloud
-----------------------------

This repository shows how to setup a HTTP reverse proxy in a DotCloud
application.

You can deploy it on DotCloud with::

    git clone git://github.com/lopter/proxytricks-on-dotcloud proxytricks
    dotcloud push proxytricks proxytricks-on-dotcloud

This trick can be used when you want to point different parts of your URI space
to different DotCloud services.

In this example all URIs that starts with /blog/ are redirected to a blog
service. Everything else is redirected to the app service

.. code-block::

                   +-------+          o-----o
                   |       |          |     |
   HTTP Requests --> proxy ---+- /* --> app |
                   |       |   \      |     |
                   +-------+    \     o-----o o------o
                                 \            |      |
                                  `- /blog/* -> blog |
                                              |      |
                                              o------o

However this solution is not really advised on the DotCloud platform for three
reasons:
#. It adds a service only to route HTTP traffic (expensive);
#. It's difficult to set up;
#. It further adds latency (on DotCloud HTTP traffic goes already at least
   through one reverse proxy and two in the case of SSL).

That's why, whenever possible, your are advised to use sub domains, e.g:
blog.dotcloud.com.
