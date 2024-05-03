Installation
============

Prerequisites
-------------

.. warning::

   This documentation is by no means comprehensive, and assumes you know how to set up an NGINX server

* A server with a publicly accessible IP address
* A domain to point at the webserver
* A compiled copy of the web app, as instructed in `Compilation <compilation.html>`_

.. note::

   If you want to use HTTPS (you should for anything other than testing) you will also need to set up `Certbot <https://certbot.eff.org/>`_ and get an SSL certificate for your domain

Installing
----------

#. Set up `NGINX <https://www.nginx.com/>`_
#. Create a new virtual host, with a new webroot
#. Copy the built HTML & JavaScript to the webroot
#. Restart NGINX
#. (If wanting to use HTTPS, set up `Certbot <https://certbot.eff.org/>`_ and get an SSL certificate)