.. include:: ../GLOBAL.rst

.. _ssh_keys:

SSH Keys in Scalr
=================

Definition and Scope
--------------------

|SCOPE_ENV|

Upon launching Linux Servers, Scalr automatically generates a new SSH Keypair and makes it available to users. These key pairs can be used to remotely log into servers. If you have different authentication methods like password auth, this can still be used, Scalr will not interfere with it.

Upon launching Windows Servers, Scalr will create an SSH key and/or a password depending on the cloud.

Accessing Keys
--------------

If you do not have policy set, Scalr will automatically generate a new key per Farm. All servers within a farm will use the same key, keys can be downloaded in PEM or PPK format depending on what you need. There are two ways to access keys depending on the permissions that are set:

.. |DROPDOWN| image:: images/dropdown.png
         :scale: 80%

1. Go to the Farms or Servers page in the |ENVIRONMENT| scope, find your server or farm, click on the dropdown on the left hand side |DROPDOWN|, and click on Server Credentials.

.. image:: images/server_cred_dropdown.png
   :scale: 70%

.. image:: images/server_cred_options.png
  :scale: 70%

2. Go to the main Scalr dropdown on the top left |MENU_ENV| and click on SSH keys. Once the SSH key page shows up, find the SSH key for your Farm and download the key:

.. image:: images/ssh_keys_page.png
  :scale: 70%

Adding Policy for Keys
----------------------
