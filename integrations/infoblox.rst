.. include:: ../GLOBAL.rst

.. _infoblox:

Infoblox Integration
====================

Definition and Scope
--------------------
|SCOPE_SCALR| |SCOPE_ACC| |SCOPE_ENV| |SCOPE_ROLE| |SCOPE_F_ROLE|

.. |infoblox_doc| raw:: html

   <a href="https://www.infoblox.com/" target="_blank">Infoblox Website</a>

Scalr provides a Webhook integration with Infoblox allowing you manage your IP addresses and hostnames directly in Infoblox for private clouds. Find out more about Infoblox here: |infoblox_doc| |NEWWIN|

Installation & Setup
--------------------

.. note:: This document is written for Debian distributions. Adapt as necessary for other distributions. **Prerequisite**: You will need to create a server to host your Webhook, find out more about Webhhoks here: :ref:`webhooks`.

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
-------------------------------------

When creating a Farm Role you will be prompted for Network information, at that point you should select the Infoblox Endpoint as your IP Source:

.. image:: images/ip_source.png
   :scale: 60%

Furthermore, you can set up a Policy to enforce the IP Pool Source, see more here: :ref:`policy_engine`
