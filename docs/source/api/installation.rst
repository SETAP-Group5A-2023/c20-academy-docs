Installation
============

Prerequisites
-------------

* A server with a publicly accessible IP address, preferably running either Fedora 39 or Ubuntu 22.04 LTS, as these are the platforms we test against
* A domain to point at the API instance
* A compiled copy of the code, as instructed in `Compilation <compilation.html>`_

.. note::

   If wanting to host with HTTPS (you should for anything other than testing), you need to use NGINX with a reverse proxy. This is beyond the scope of these instructions, but you just need to point it at the port number you specify in :code:`config.yaml`

Installing
----------

#. Install PostgreSQL, e.g. `Fedora Docs <https://docs.fedoraproject.org/en-US/quick-docs/postgresql/>`_
#. Set a user name and password for the API to access the database
#. Use the :code:`database/db_create.sql` file to set up the database and tables in Postgres (Upload the file to the server, then use :code:`\\i <filename>` in Postgres to run the file)
#. If you are installing for testing purposes, also run the :code:`database/db_populate.sql` file to add some dummy data to the database, using the same steps as above
#. Upload the compiled binary to the server's :code:`/usr/bin/` folder
#. Create the :code:`/etc/c20-academy-api/` folder
#. Run :code:`c20-academy-api` inside the folder to create a blank :code:`config.yaml`, and edit as required
#. Copy :code:`api/c20-academy-api.service` into :code:`/etc/systemd/system/`
#. Start the systemd service (Using :code:`# systemctl start c20-academy-api` or :code:`# systemctl enable --now c20-academy-api`)
