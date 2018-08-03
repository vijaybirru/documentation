.. include:: ../GLOBAL.rst

.. _ssh_keys:

SSH Keys in Scalr
=================

Definition and Scope
--------------------

|SCOPE_ENV|

Upon launching servers, Scalr automatically generates a new SSH Keypair and makes it available to users. These key pairs can be used to remotely log into servers. If you have different authentication methods like password auth, this can still be used, Scalr will not interfere with it. When launching a Windows server, Scalr will create an SSH key and/or a password. Some clouds require a SSH key to decrypt the Windows password.

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

Usernames
---------

To log into the servers with your keypair you will need to use the correct usernames:

.. csv-table::
   :header-rows: 1
   :file: csv/ssh_usernames.csv
   :widths: 20,80

Adding Policy for Keys
----------------------

Some organizations like to enforce policies around how users log into their servers. In this case, a policy can be created to ensure a specific key is used for ALL servers within an |ENVIRONMENT|. This key must exist in the cloud provider for it to be used by a policy. End users will *not* be able to download this key, it is up to the administrators to tell the users how to log into the servers.

To create a policy for SSH keys, go to the |ACCOUNT| scope, click on the main Scalr menu |MENU_ACC|, click on Policy Engine > Policy Groups. In here you can either add to an existing cloud Policy or create a new one, search for cloud.ssh.key_pair and enter the name of the key as it appears in the cloud provider:

.. image:: images/key_policy.png
  :scale: 70%

To learn more about the Policy Engine, please go here: :ref:`policy_engine`
