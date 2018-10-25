.. _one_server_install:

Scalr Server Install - One Server
=================================

.. note:: This guide should only be used for POCs or Development environments. To see a production install guide, please visit the following page: :ref:`install`

Prerequisites
^^^^^^^^^^^^^^
* Scalr download token
* Scalr license file

Installation
^^^^^^^^^^^^^
Get the scalr-server package:

.. code-block:: shell

   # For Debian:
   curl -s https://<token>:@packagecloud.io/install/repositories/scalr/scalr-server-ee/script.deb.sh | sudo bash
   # For RPM:
   curl -s https://<token>:@packagecloud.io/install/repositories/scalr/scalr-server-ee/script.rpm.sh | sudo bash

Install the package:

.. code-block:: shell

   # For Debian:
   apt-get install scalr-server
   # For RPM:
   yum install scalr-server


Run the following when prompted:

.. code-block:: shell

   scalr-server-wizard

The step above did two things, created the /etc/scalr-server directory and the scalr-server-secrets.json file.

Please add the license file to the /etc/scalr-server directory

.. code-block:: shell

    ##Paste the license.json file in the following location on each server:##
    vi /etc/scalr-server/license.json

Reconfigure the Scalr server:

.. code-block:: shell

    /opt/scalr-server/bin/scalr-server-ctl reconfigure

You can now log into Scalr by putting the hostname or IP address that is listed as your endpoint in the scalr-server.rb into a browser. To log in the first time, please find the admin password in the /etc/scalr-server/scalr-server-secrets.json file.

.. code-block:: shell

  "app": {
    "admin_password": "password123",

The default username is admin:

.. image:: images/admin_login.png
   :scale: 70%

Shared Roles
^^^^^^^^^^^^^

.. note:: We recommend using Shared Roles for POC or Development environments, not Production. The best practice for Production is to maintain in-house images to ensure it follows your security standards.

Syncing shared roles lets you use pre-built Images that are provided by Scalr for use on Public Clouds including AWS, Azure, and GCE. To access them, you must execute the following command:

.. code-block:: shell

  scalr-server-manage sync-shared-roles
