Scalr Server Maintenance
==========================

We recommend having two Scalr environments, one for development and production. It is not uncommon for the majority of our customers to upgrade development the day a new release comes out and to upgrade production a week or so after. All activities on this page should be executed on the development environment prior to production.

Upgrades
---------

Backup your database (this is an example, choose any location for the backup):

.. code-block:: shell

   /opt/scalr-server/embedded/bin/mysqldump --all-databases -u{sql_username} -p{sql_password} | gzip > /some_folder/pre_upgrade_backup.gz

Stop all scalr hosts using:

.. code-block:: shell

   scalr-server-manage stop all

Upgrade scalr across all hosts:

.. code-block:: shell

   ##For RPM based installations##
   yum upgrade scalr-server

   ##For DEB based installations##
   apt upgrade scalr-server

Once all hosts have finished running the yum upgrade, **run a reconfigure on the main database first**:

.. code-block:: shell

   scalr-server-ctl reconfigure

Once the main database is finished reconfiguring run the reconfigure across all other hosts:

.. code-block:: shell

   scalr-server-ctl reconfigure

Automated Upgrades
-------------------

As you can see, the Scalr upgrade process is fairly simple, because of this we encourage customers to automate the process using their favorite configuration management method. We have put together an example using Ansible: https://github.com/scalr-tutorials/scalr-server-upgrade-ansible

Database Backups
-----------------

It is highly recommended, if not required, to take at least a daily backup of the database. To do this, you can use any automation tool of choice or simply just run a cron job and send the database backup to a remote location:

.. code-block:: shell

   /opt/scalr-server/embedded/bin/mysqldump --all-databases -u{sql_username} -p{sql_password} | gzip > /some_folder/db_backup.gz

Monitoring Best Practices
--------------------------

**Automated Testing**

While Scalr is a very reliable, it is a good idea to perform some automated testing on the basic functionality of Scalr, like launching Farms/Servers. This will not only test Scalr, but will make sure that the following is function correctly:

* Cloud provider functionality
* Cloud credentials
* Network connections to private and public clouds
* Connections to any configuration management tools

Here is an example that we created using Ansible: https://github.com/scalr-tutorials/scalr-automated-testing-via-ansible

**Infrastructure**

Disk:

If you used the standard Scalr installation guide, you should have mounted the main disk that Scalr uses to /opt/scalr-server/ on all Scalr nodes. Reference `this FAQ page <https://scalr-labs.atlassian.net/wiki/spaces/DOCS/pages/301039670/Scalr+Server+Maintenance>`_ for installations in different directories.  The database node will grow faster than others, but none of the nodes should ever be over 80% in disk use.

.. code-block:: shell

   root@scalr:~# df -h /opt/scalr-server/
   Filesystem      Size  Used Avail Use% Mounted on
   /dev/sdb         50G  2.1G   45G   5% /opt/scalr-server

**Application**

When it comes to monitoring Scalr itself, it is fairly simple as there are only two components of note to monitor:

* Scalr Supervisor
* Scalr Services - Scalr uses a command-line tool to manage the internal services, scalr-server-manage.

Make sure the Scalr Supervisor is up:

.. code-block:: shell

   root@scalr:~# service scalr status
   scalr is running

or

.. code-block:: shell

   root@scalr:~# /etc/init.d/scalr status
   scalr is running

Using the Scalr Server command-line management tool, make sure the individual service are up (they are likely spread across multiple nodes):

.. code-block:: shell

   root@scalr:~# scalr-server-manage status
   analytics_poller                 RUNNING   pid 3031, uptime 2 days, 4:08:22
   analytics_processor              RUNNING   pid 3059, uptime 2 days, 4:08:22
   beat                             RUNNING   pid 3063, uptime 2 days, 4:08:22
   dbqueue                          RUNNING   pid 3035, uptime 2 days, 4:08:22
   license-manager                  RUNNING   pid 3049, uptime 2 days, 4:08:22
   monitor                          RUNNING   pid 3089, uptime 2 days, 4:08:22
   msgsender                        RUNNING   pid 3068, uptime 2 days, 4:08:22
   plotter                          RUNNING   pid 3062, uptime 2 days, 4:08:22
   poller                           RUNNING   pid 3075, uptime 2 days, 4:08:22
   scalr-crond                      RUNNING   pid 3036, uptime 2 days, 4:08:22
   scalr-httpd                      RUNNING   pid 3080, uptime 2 days, 4:08:22
   scalr-influxdb                   RUNNING   pid 3087, uptime 2 days, 4:08:22
   scalr-memcached                  RUNNING   pid 3039, uptime 2 days, 4:08:22
   scalr-mysql                      RUNNING   pid 2705, uptime 2 days, 4:10:10
   scalr-nginx                      RUNNING   pid 3030, uptime 2 days, 4:08:22
   scalr-rabbitmq                   RUNNING   pid 3037, uptime 2 days, 4:08:22
   scalr-rrd                        RUNNING   pid 3041, uptime 2 days, 4:08:22
   szrupdater                       RUNNING   pid 3040, uptime 2 days, 4:08:22
   workflow-engine                  RUNNING   pid 3072, uptime 2 days, 4:08:22
   zmq_service                      RUNNING   pid 3032, uptime 2 days, 4:08:22

These services should always be in a "RUNNING" state, if there is any other state returned then it should be flagged by your monitoring tool.
