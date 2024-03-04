Installation
============

Prerequisites
-------------

* A server with a publically accessible IP address, preferably running Fedora 39 as this is the platform we test against.
* A domain to point at the API instance
* Have a compiled copy of the code, as instructed in `Compilation <compilation>`_

.. note::

   If wanting to host with HTTPS (you should for anything other than testing), you need to use NGINX with a reverse proxy. This is beyond the scope of these instructions, but you just need to point it at the port number you specify in :code:`config.yaml`

Installing
----------

#. Install PostgreSQL, e.g. `Fedora Docs <https://docs.fedoraproject.org/en-US/quick-docs/postgresql/>`_
#. Setup SSL encryption within Postgres
#. Set a username and password for the API to access the database
#. Use the :code:`database/db_create.sql` file to setup the database and tables in Postgres (Upload the file to the server, then use :code:`\\i <filename>` in Postgres to run the file)
#. Upload the compiled binary to the server
#. Run the binary once manually to generate a blank :code:`config.yaml`. Edit this to reflect the username, password and address of your Postgres server, as well as the IP address and port number of your server
#. Copy :code:`api/c20-academy-api.service` into :code:`/etc/systemd/system/`
#. Start the systemd service (With :code:`$ systemctl start c20-academy-api` or :code:`$ systemctl enable --now c20-academy-api`)