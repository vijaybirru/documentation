.. include:: ../GLOBAL.rst

External Integrations
=====================

.. _infoblox:

Infoblox Integration
--------------------

Definition and Scope
^^^^^^^^^^^^^^^^^^^^
|SCOPE_SCALR| |SCOPE_ACC| |SCOPE_ENV| |SCOPE_ROLE| |SCOPE_F_ROLE|

.. |infoblox_doc| raw:: html

   <a href="https://www.infoblox.com/" target="_blank">Infoblox Website</a>

Scalr provides a Webhook integration with Infoblox allowing you manage your IP addresses and hostnames directly in Infoblox for private clouds. Find out more about Infoblox here: |infoblox_doc| |NEWWIN|

Installation & Setup
^^^^^^^^^^^^^^^^^^^^

.. note:: This document is written for Debian distributions. Adapt as necessary for other distributions. **Prerequisite**: You will need to create a server to host your Webhook, find out more about Webhooks here: :ref:`webhooks`.

First, you will need to create a server to host your Webhook, find out more about Webhhoks here: :ref:`webhooks` . Once you have the server, please follow these directions:

On the server that will be hosting the Webhook, create the directory and pull down the Webhook code from Git:

.. code-block:: shell

  apt update
  apt install python-pip -y
  pip install docker-compose

  curl -fsSL https://get.docker.com/ | sh
  service docker start || systemctl start docker

  git clone https://github.com/scalr-tutorials/scalr-infoblox-webhook.git /opt/infoblox-webhook

.. include:: /sec_comp/integrations.rst
    :start-after: endpoint_start:
    :end-before: endpoint_end

The URL above will point to the server you are hosting the Infoblox Webhook on (``http://<webhook server IP or hostname>:5020/infoblox/``). Make sure to copy down the Signing Key that is generated as it will be used later on.

Next, you will want to setup an IP Pool. To create a IP Pool at the |SCALR| or |ACCOUNT| scope, click on the Scalr icon on the top left |MENU_ACC| and then click on IP Pools. After you click on New IP Pool the following page will show up:

.. image:: images/new_ip_pool.png
   :scale: 70%

In this screen you must enter the following information:

* Both IPAM TYPE and IP ALLOCATION are External.
* Select the Integration Endpoint that was created earlier.
* Enter the Subnet Mask for the network you will be pulling information for.
* Enter the Default Gateway for the network you will be pulling information for.
* In the Allocate IP User Data field, enter the subnet range that should be used.

Next, log into the server that is hosting the Webhook and go to the ``/opt/infoblox-webhook`` directory. Copy the uwsgi.ini file:

.. code-block:: shell

  cd /opt/infoblox-webhook
  cp uwsgi.ini.example uwsgi.ini
  vi uwsgi.ini

Edit uwsgi.ini to set the configuration variables:

* ``SCALR_SIGNING_KEY``: Signing key that was generated after creating the Webhook Endpoint.
* ``BACKEND_USER``: The user accessing Infoblox
* ``BACKEND_PASS``: The password for accessing Infoblox
* ``BACKEND_VERIFY``: Set to true/false if you want the Infoblox certificate to be checked (if invalid, the webhook will refuse to communicate with Infoblox)

Next, run the webhook with Docker:

.. code-block:: shell

  ./relaunch.sh

You're Infoblox Webhook should now be running, you can check the logs by using the following command:

.. code-block:: shell

  docker logs -f infoblox-webhook

Configure Farm Roles to Use Infoblox
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

When creating a Farm Role you will be prompted for Network information, at that point you should select the Infoblox Endpoint as your IP Source:

.. image:: images/ip_source.png
   :scale: 60%

Furthermore, you can set up a Policy to enforce the IP Pool Source, see more here: :ref:`policy_engine`


.. _servicenow:

ServiceNow Integration
----------------------

Overview
^^^^^^^^

|SCOPE_SCALR| |SCOPE_ACC| |SCOPE_ENV|

Scalr provides out-of-the-box integration with ServiceNow to enable mutual customers to leverage ServiceNow for ITSM workflows including problem management, incident management, change management, asset management, and others. The Scalr ServiceNow integration allows users to maintain a single source of truth for all on premise and cloud-based infrastructure resources and services,  and leverage existing workflows, while taking advantage of Scalr for cloud infrastructure management.

CMDB Integration
^^^^^^^^^^^^^^^^
Scalr integrates with the ServiceNow CMDB to record cloud-based assets, resources and configurations in ServiceNow, and maintain a single source of truth across the customer's entire IT ecosystem.

CMDB Integration Setup
^^^^^^^^^^^^^^^^^^^^^^

.. note:: You will need to create a server to host your Webhook, this can be a small Linux server as the load should be minimal. Find out more about Webhooks here: :ref:`webhooks`.

.. |snow_doc| raw:: html

   <a href="https://docs.servicenow.com/bundle/helsinki-platform-administration/page/build/applications/task/t_CreateATable.html/" target="_blank">ServiceNow Table Creation</a>

First, you will need to create a table in ServiceNow if it doesn't already exist. Please follow these instructions to do so: |snow_doc| |NEWWIN|

Next, on the server that will be hosting the Webhook, pull down the Webhook code from Git:

.. code-block:: shell

  apt update
  apt install python-pip -y

  pip install docker-compose

  curl -fsSL https://get.docker.com/ | sh
  service docker start || systemctl start docker

  git clone https://github.com/scalr-tutorials/scalr-servicenow-webhook.git /opt/snow-webhook

.. include:: /sec_comp/integrations.rst
    :start-after: endpoint_start:
    :end-before: endpoint_end

The URL above will point to the server you are hosting the ServiceNow Webhook on (http://<webhook server IP or hostname>:5018/servicenow/). Make sure to copy down the Signing Key that is generated as it will be used later on.

.. include:: /sec_comp/integrations.rst
    :start-after: webhook_start:
    :end-before: webhook_end

The Endpoint in the screenshot above will be the Endpoint that you created in the previous step. In terms of the Events, you can select as many Events as you wish, every time this event is triggered a payload will be sent to ServiceNow. By Default, the Webhook will trigger on the following events:

* BeforeInstanceLaunch
* HostInit
* BeforeHostUp
* HostUp
* BeforeHostTerminate
* HostDown
* IPAddressChanged
* ResumeComplete
* HostInitFailed

This is configurable, by updating the following line in webhook.py which is located in /opt/snow-webhook :

https://github.com/scalr-tutorials/scalr-servicenow-webhook/blob/master/webhook.py#L48

Next, log into the server that is hosting the Webhook and go to the /opt/snow-webhook directory. Copy the uwsgi.ini file:

.. code-block:: shell

  cd /opt/snow-webhook
  vi uwsgi.in

Next, edit the uwsgi.ini file to set the configuration variables:

* env = SCALR_SIGNING_KEY=Signing key that was generated after creating the Webhook Endpoint.
* env = SNOW_URL=The ServiceNow URL
* env = SNOW_USER=The user accessing ServiceNow
* env = SNOW_PASS=The password for accessing ServiceNow
* env = SCALR_TABLE=The table name that should receive data from the Webhook

Next, run the Webhook with Docker:

.. code-block:: shell

  ./relaunch.sh

You’re ServiceNow Webhook should now be running, you can check the logs by using the following command:

.. code-block:: shell

  docker logs -f snow-webhook

To test, build and launch a Farm, once the server reaches the Event specified in the Webhook section above, the payload will be sent to the Webhook and forwarded to ServiceNow.
