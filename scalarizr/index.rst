.. include:: ../GLOBAL.rst

Scalarizr
==========

.. include:: /install_guide/scalarizr_installation.rst
   :start-after: Term-Scalarizr-About-Start
   :end-before: Term-Scalarizr-About-End

This page will focus on how to monitor, update, and use Scalarizr once it is deployed. If you do not have Scalarizr installed yet or want to learn more about it, please go to the Scalarizr administration section: :ref:`admin_scalarizr`

Monitoring Scalarizr
--------------------

After you have provisioned a server it is important to ensure Scalarizr is up to date and running at all times. If Scalarizr is not running you will not be able to autoscale based on metrics, run scripts, or collect statistics about the server. The two main services that are needed to ensure Scalarizr is functioning correctly are:

* scalarizr
* scalr-upd-client

The Scalarizr agent is what communicates back and forth from Scalr. The scalr-upd-client queries the Scalarizr repo to ensure Scalarizr is always up to date.

The following is a list of ways to check if Scalarizr is functioning properly.

Servers Dashboard:
^^^^^^^^^^^^^^^^^^

If the agent is install and running correctly you will see a green check mark with the agent version:

.. image:: images/server_dashboard.png
   :scale: 70%

If the agent is not running correctly you will see the server row highlighted in red as well as error messages when hovering over the exclamation point:

.. image:: images/broken_agent.png
   :scale: 70%

Server General Details:
^^^^^^^^^^^^^^^^^^^^^^^

To get to the Server Details, click on the Servers page, then click on the ID of the server you want to take a look at. If the agent is installed and running correctly you will see "Running" for the Scalarizr Status:

.. image:: images/server_general_details.png
   :scale: 70%

If the agent is not running correctly you will see an error in the Scalarizr Status as well as an Alert in Active Alerts:

.. image:: images/active_alerts.png
   :scale: 70%

Farm Dashboard:
^^^^^^^^^^^^^^^

If the agent is not running correctly you will also see an alert in the Farm dashboard, you can click on that alert to get directed to the alerts page:

.. image:: images/farm_alert_flag.png
   :scale: 70%

.. _updating_scalarizr:

Updating the Scalarizr Agent
----------------------------

It is important to keep the Scalarizr agent updated to within a month or two of the latest release. The Scalr admin should maintain their own Scalarizr repo and ensure the agents are updated: :ref:`scalarizr_repo`

As a Farm owner, you also have the ability to pick what Scalarizr version is on your server as well as how frequent it gets updated, by default it checks for an update once every hour.

Farm:
^^^^^

.. |WRENCH| image:: images/wrench.png
         :scale: 80%

To update these setting for the entire farm, go to the Farms page, find your farm, click on the |WRENCH| and then go to Advanced Settings:

.. image:: images/farm_advanced_settings.png
   :scale: 70%

In the Repository section you can select which repository you want all of the servers to point to, there may only be one depending on how the Scalr admin has setup your Scalr Server Repo.

You can also schedule the time that Scalarizr should check for updates, this follows standard crontab notation.

Farm Role:
^^^^^^^^^^

To update these setting for a single Farm Role, go to the Farms page, find your farm, click on the |WRENCH| , click on the Farm Role you want to update, and then go to the bottom of the Advanced tab:

.. image:: images/farm_role_advanced_settings.png
   :scale: 70%

In the Repository section you can select which repository you want all of the servers to point to, there may only be one depending on how the Scalr admin has setup your Scalr Server Repo.

You can also schedule the time that Scalarizr should check for updates, this follows standard crontab notation.

Forcing an Update:
^^^^^^^^^^^^^^^^^^

If there is a need to update Scalarizr without waiting for the scheduled update, the option is given in the General details page for any server:

.. image:: images/update_scalarizr.png
   :scale: 70%

Scalarizr Logs
--------------

.. Term-Scalr-Logs-Start

The following are the Scalarizr log locations:

.. csv-table::
   :header-rows: 1
   :file: csv/log_location.csv
   :widths: 20,80

.. Term-Scalr-Logs-Stop

.. _szradm:

Scalarizr Administrative Interface
==================================

Scalarizr provides a command line interface (szradm) allowing users to perform a variety of tasks inluding:

* Firing events
* Querying environments information about the server or farm.

To access the szradm interface go to the following locations:

Linux:

.. code-block:: shell

  /usr/bin/szradm

Windows:

.. code-block:: shell

  C:\opt\scalarizr\szradm.bat

Firing Custom Events
--------------------

Szradm can be used to fire Custom Events, see more information on Custom Events here: :ref:`custom_events`

Here is an example of firing a custom event from Scalarizr:

.. code-block:: shell

  # Fire the "Hello" Custom Event
  $ szradm fire-event Hello

You can call this Custom Event from within a server and trigger an event on all servers that the Custom Event is linked to.

Querying Environments
----------------------

queryenv list-roles
^^^^^^^^^^^^^^^^^^^

The ListRoles QueryEnv call returns a list of the Farm Roles and associated server(s) that make up the Farm the calling Server belongs to.

The list retuned by ListRoles may be filtered using the following parameters:

.. csv-table::
   :header-rows: 1
   :file: csv/query_env_listroles.csv
   :widths: 20,80

Example Output:

.. code-block:: sh

      root@haproxy-1:~# szradm queryenv --format=json list-roles

.. code-block:: json

          {
              "roles": [
                  {
                      "alias": "app",
                      "behaviour": "app,chef",
                      "hosts": [
                          {
                              "cloud-location": "us-east-1",
                              "cloud-location-zone": "us-east-1d",
                              "external-ip": "54.80.254.121",
                              "index": "1",
                              "internal-ip": "10.231.56.83",
                              "status": "Running"
                          }
                      ],
                      "id": "70824",
                      "name": "app-apache64-ubuntu1204",
                      "role-id": "38356"
                  },
                  {
                      "alias": "lb",
                      "behaviour": "haproxy,chef",
                      "hosts": [
                          {
                              "cloud-location": "us-east-1",
                              "cloud-location-zone": "us-east-1d",
                              "external-ip": "54.237.243.48",
                              "index": "1",
                              "internal-ip": "10.140.13.96",
                              "status": "Running"
                          }
                      ],
                      "id": "70825",
                      "name": "haproxy14-ubuntu1204",
                      "role-id": "55435"
                  },
                  {
                      "alias": "lb2",
                      "behaviour": "www,chef",
                      "hosts": [
                          {
                              "cloud-location": "us-east-1",
                              "cloud-location-zone": "us-east-1d",
                              "external-ip": "54.237.159.84",
                              "index": "1",
                              "internal-ip": "10.239.60.22",
                              "status": "Running"
                          }
                      ],
                      "id": "70826",
                      "name": "lb-nginx64-ubuntu1204",
                      "role-id": "38354"
                  },
                  {
                      "alias": "cache",
                      "behaviour": "memcached,chef",
                      "hosts": [
                          {
                              "cloud-location": "us-east-1",
                              "cloud-location-zone": "us-east-1d",
                              "external-ip": "23.20.164.51",
                              "index": "1",
                              "internal-ip": "10.238.245.237",
                              "status": "Running"
                          }
                      ],
                      "id": "70827",
                      "name": "memcached-ubuntu1204",
                      "role-id": "53475"
                  },
                  {
                      "alias": "db",
                      "behaviour": "chef,mysql2",
                      "hosts": [
                          {
                              "cloud-location": "us-east-1",
                              "cloud-location-zone": "us-east-1d",
                              "external-ip": "54.196.199.10",
                              "index": "1",
                              "internal-ip": "10.236.218.208",
                              "replication-master": "1",
                              "status": "Running"
                          }
                      ],
                      "id": "76050",
                      "name": "mysql-ubuntu1404",
                      "role-id": "64082"
                  },
                  {
                      "alias": "db2",
                      "behaviour": "chef,postgresql",
                      "hosts": [
                          {
                              "cloud-location": "us-east-1",
                              "cloud-location-zone": "us-east-1c",
                              "external-ip": "54.90.253.70",
                              "index": "1",
                              "internal-ip": "10.65.176.134",
                              "replication-master": "1",
                              "status": "Running"
                          }
                      ],
                      "id": "76051",
                      "name": "postgresql93-ubuntu1404",
                      "role-id": "64083"
                  },
                  {
                      "alias": "db3",
                      "behaviour": "chef,redis",
                      "hosts": [
                          {
                              "cloud-location": "us-east-1",
                              "cloud-location-zone": "us-east-1d",
                              "external-ip": "54.235.7.39",
                              "index": "1",
                              "internal-ip": "10.71.128.244",
                              "replication-master": "1",
                              "status": "Running"
                          }
                      ],
                      "id": "76052",
                      "name": "redis26-ubuntu1404",
                      "role-id": "64084"
                  },
                  {
                      "alias": "queue",
                      "behaviour": "chef,rabbitmq",
                      "hosts": [
                          {
                              "cloud-location": "us-east-1",
                              "cloud-location-zone": "us-east-1c",
                              "external-ip": "54.234.29.43",
                              "index": "1",
                              "internal-ip": "10.183.188.183",
                              "status": "Running"
                          }
                      ],
                      "id": "76053",
                      "name": "rabbitmq33-ubuntu1404",
                      "role-id": "64089"
                  }
              ]
          }

queryenv list-global-variables
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The ListGlobalVariables Queryenv call returns a list of Global Variables that are in scope for the Server that is making the call.

.. note::

  Private Global Variables are flagged to ensure you don't misuse them.

.. code-block:: bash

   user@server:~# szradm queryenv --format=json list-global-variables

.. code-block:: json

    {
      "variables": {
          "private_values": {},
          "values": {
              "Purpose": "scalarizr screenshots for docs",
              "SCALR_ACCOUNT_ID": "1",
              "SCALR_ACCOUNT_NAME": "Customer Success",
              "SCALR_AMI_ID": "ami-63866d19",
              "SCALR_AVAIL_ZONE": "us-east-1e",
              "SCALR_BEHAVIORS": "base",
              "SCALR_CLOUD_LOCATION": "us-east-1",
              "SCALR_CLOUD_LOCATION_ZONE": "us-east-1e",
              "SCALR_CLOUD_PLATFORM": "ec2",
              "SCALR_CLOUD_SERVER_ID": "i-09ea238e2b70ba0c6",
              "SCALR_COST_CENTER_BC": "CS",
              "SCALR_COST_CENTER_ID": "ddbbe790-d3d8-48be-8ee7-b42f78234736",
              "SCALR_COST_CENTER_NAME": "Customer Success",
              "SCALR_ENV_ID": "6",
              "SCALR_ENV_NAME": "Solution Architecture",
              "SCALR_EXTERNAL_IP": "54.209.94.192",
              "SCALR_FARM_HASH": "408ea3b05e7b9e",
              "SCALR_FARM_ID": "515",
              "SCALR_FARM_NAME": "Server 1",
              "SCALR_FARM_OWNER_EMAIL": "ryan@scalrdemo.demo.scalr.com",
              "SCALR_FARM_ROLE_ALIAS": "base-ubuntu1604",
              "SCALR_FARM_ROLE_ID": "805",
              "SCALR_FARM_TEAM": null,
              "SCALR_ID": "6d341467",
              "SCALR_IMAGE_ID": "ami-63866d19",
              "SCALR_INSTANCE_FARM_INDEX": "1",
              "SCALR_INSTANCE_ID": "i-09ea238e2b70ba0c6",
              "SCALR_INSTANCE_INDEX": "1",
              "SCALR_INTERNAL_IP": "10.0.40.18",
              "SCALR_ISDBMASTER": "0",
              "SCALR_LAUNCHED_BY_EMAIL": "ryan@scalrdemo.demo.scalr.com",
              "SCALR_LAUNCHED_BY_ID": "23",
              "SCALR_PROJECT_BC": "CS-01",
              "SCALR_PROJECT_ID": "1682b63d-6d28-4b5f-8438-3cf058f89a6c",
              "SCALR_PROJECT_NAME": "Solution Architects",
              "SCALR_REGION": "us-east-1",
              "SCALR_ROLE_ID": "1",
              "SCALR_ROLE_NAME": "base-ubuntu1604",
              "SCALR_ROLE_OS": "ubuntu-16-04",
              "SCALR_SERVER_HOSTNAME": "ec2-54-174-97-210.compute-1.amazonaws.com",
              "SCALR_SERVER_ID": "7eaeb765-2037-46f2-ada8-033ef2915c75",
              "SCALR_SERVER_TYPE": "t2.nano"
          }
      }
    }


szradm queryenv get-server-user-data
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The GetServerUserData Queryenv call returns information about the Server (Instance) making the call.

.. note::

  Most of the useful information returned by this call is also found in szradm queryenv list-global-variables, which you might want to use instead.

.. code-block:: bash

   root@ec2-54-174-97-210:~# szradm queryenv --format=json get-server-user-data

.. code-block:: json

     {
         "user-data": {
             "values": {
                 "behaviors": "base",
                 "cloud_location_zone": "us-east-1e",
                 "cloud_storage_path": "s3://",
                 "env_id": "6",
                 "farm_roleid": "805",
                 "farmid": "515",
                 "hash": "408ea3b05e7b9e",
                 "httpproto": "https",
                 "message_format": "json",
                 "owner_email": "user@scalr.com",
                 "p2p_producer_endpoint": "https://scalr.server.com/messaging",
                 "platform": "ec2",
                 "queryenv_url": "https://scalr.server.com/query-env",
                 "realrolename": "base-ubuntu1604",
                 "region": "us-east-1",
                 "role": "base",
                 "roleid": "1",
                 "s3bucket": null,
                 "scalr_version": "7.10.1",
                 "server_index": "1",
                 "serverid": "7eaeb765-2037-46f2-ada8-033ef2915c75",
                 "szr_key": "qrD1uXdCyw8uDG9S0T31Ta7Z8N/fOv5YwnFgu30SeMtaiLU8n9BXgQ=="
             }
         }
     }

szradm queryenv set-global-variable
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The SetGlobalVariable Queryenv call allows you to set:

* Server-Scope Global Variables for the Server that is making the call.
* Farm-Role-Scope Global Variables for the Farm Role that the Server making the call is an instance of.

You must pass the following options when calling the SetGlobalVariable Queryenv call:

.. csv-table::
   :header-rows: 1
   :file: csv/query_env_set_gv.csv
   :widths: 20,80

.. code-block:: bash

     # Set a Global variable on the Server Scop
     root@haproxy-1:~# szradm queryenv set-global-variable scope=server param-name=ServerVar param-value=ServerValue

.. code-block:: xml

     <?xml version="1.0" encoding="utf-8"?>
     <response>
         <variables>
             <variable name="ServerVar">ServerValue</variable>
         </variables>
     </response>

.. code-block:: bash

     # Set a Global Variable on the Farm-Role Scope
     root@haproxy-1:~# szradm queryenv set-global-variable scope=farmrole param-name=FarmRoleVar param-value=FarmRoleValue

.. code-block:: xml

     <?xml version="1.0" encoding="utf-8"?>
     <response>
         <variables>
             <variable name="FarmRoleVar">FarmRoleValue</variable>
         </variables>
     </response>

.. code-block:: bash

     # List the variables that were set
     root@haproxy-1:~# szradm queryenv list-global-variables

.. code-block:: xml

     <?xml version="1.0" encoding="utf-8"?>
     <response>
         <variables>
             <variable name="FarmRoleVar" private="0">FarmRoleValue</variable>
             <variable name="ServerVar" private="0">ServerValue</variable>
             <!-- More Global Variables -->
         </variables>
     </response>
