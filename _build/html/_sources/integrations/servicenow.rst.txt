.. include:: ../GLOBAL.rst

.. _servicenow:

ServiceNow Integration
=======================

Overview
--------

|SCOPE_SCALR| |SCOPE_ACC| |SCOPE_ENV|

Scalr provides out-of-the-box integration with ServiceNow to enable mutual customers to leverage ServiceNow for ITSM workflows including problem management, incident management, change management, asset management, and others. The Scalr ServiceNow integration allows users to maintain a single source of truth for all on premise and cloud-based infrastructure resources and services,  and leverage existing workflows, while taking advantage of Scalr for cloud infrastructure management.

CMDB Integration
----------------
Scalr integrates with the ServiceNow CMDB to record cloud-based assets, resources and configurations in ServiceNow, and maintain a single source of truth across the customer's entire IT ecosystem.

CMDB Integration Setup
^^^^^^^^^^^^^^^^^^^^^^

.. note:: You will need to create a server to host your Webhook, find out more about Webhhoks here: :ref:`webhooks`.

On the server that will be hosting the Webhook, create the directory and pull down the Webhook code from Git:

.. code-block:: shell

  apt update apt install python-pip -y

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

The Endpoint in the screenshot above will be the Endpoint that you created in the previous step. In terms of the Events, you can select as many Events as you wish, every time this event is triggered a payload will be sent to ServiceNow.

Next, log into the server that is hosting the Webhook and go to the /opt/snow-webhook directory. Copy the uwsgi.ini file:

.. code-block:: shell

  cd /opt/snow-webhook
  cp uwsgi.ini.example uwsgi.ini
  vi uwsgi.in

Edit uwsgi.ini to set the configuration variables:

* env = SCALR_SIGNING_KEY=Signing key that was generated after creating the Webhook Endpoint.
* env = SNOW_URL=The ServiceNow URL
* env = SNOW_USER=The user accessing ServiceNow
* env = SNOW_PASS=The password for accessing ServiceNow

Next, run the webhook with Docker:

.. code-block:: shell

  ./relaunch.sh

You’re ServiceNow Webhook should now be running, you can check the logs by using the following command:

.. code-block:: shell

  docker logs -f infoblox-webhook
