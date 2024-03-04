Installation
============

The recommended platform for the API is Fedora 39, as this is what it is tested against

#. Install PostgreSQL, e.g. `Fedora Docs <https://docs.fedoraproject.org/en-US/quick-docs/postgresql/>`_
#. Setup SSL encryption within Postgres
#. Set a username and password for the API to access the database
#. Use the :code:`database/db_create.sql` file to setup the database and tables in Postgres (Upload the file to the server, then use :code:`\i <filename>` in Postgres to run the file)
#. Upload the compiled binary to the server
#. Run the binary once manually to generate a blank config file, edit as necessary
#. Copy :code:`api/c20-academy-api.service` into :code:`/etc/systemd/system/`
#. Start the systemd service (With :code:`$ systemctl start c20-academy-api` or :code:`$ systemctl enable --now c20-academy-api`)