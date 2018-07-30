Scalr Server HA Replication
===========================

If you are deploying Scalr on premise we recommend setting up high availability for the database. The steps below will automate the HA replication for you. If you are using a cloud based solution like AWS RDS for your database, the service has replication automatically built in if chosen.

Setting up Replication for the Scalr Database
---------------------------------------------

If you are using the built-in MySQL server that comes with Scalr, you can use the kickstart-replication script to setup replication to your slave database.

Scalr should already be installed, if you have not installed Scalr yet, click `here <https://scalr-docs.readthedocs-hosted.com/en/update/install_guide/scalr_server_installation.html>`_ . Make all necessary changes to scalr-server.rb and make sure to specify that master server is configured to be used as database server.

On the master database, make sure your scalr-server-local.rb has the following set:

.. code-block:: shell

   # Enable the MySQL component
   mysql[:enable] = true

   # Set unique ID of this MySQL server
   mysql[:server_id] = 1

   # Enable binary log needed for replication
   mysql[:binlog] = true

   # Allow remote root access is required by the kickstart-replication script
   mysql[:allow_remote_root] = true

   # Specify which IP the slave will connect from to grant the correct privileges to the replication user
   mysql[:repl_allow_connections_from] = 'SLAVE-IP'

On the slave database, make sure your scalr-server-local.rb has the following set:

.. code-block:: shell

   # Enable the MySQL component
   mysql[:enable] = true

   # Set unique ID of this MySQL server
   mysql[:server_id] = 2

   # Enable binary log needed for replication
   mysql[:binlog] = true

   # Allow remote root access is required by the kickstart-replication script
   mysql[:allow_remote_root] = true

Run a reconfigure on server 1.:

.. code-block:: shell

   scalr-server-ctl reconfigure

Run a reconfigure on server 1.:

.. code-block:: shell

      scalr-server-ctl reconfigure

Start replication by executing:

.. code-block:: shell

   /opt/scalr-server/bin/kickstart-replication IP-OF-MASTER:3306 IP-OF-SLAVE:3306
