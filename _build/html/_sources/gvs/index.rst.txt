.. include:: ../GLOBAL.rst

.. _gvs:

Global Variables
================

Definition and Scope
--------------------

|SCOPE_SCALR| |SCOPE_ACC| |SCOPE_ENV| |SCOPE_ROLE| |SCOPE_FARM| |SCOPE_F_ROLE|

Global Variables are multi-purpose key value store objects that can be used for input from users or admins for the following:

* Tagging
* Script Input
* Naming Conventions
* Etc

Global Variables are encrypted in the Scalr database and can also be pulled down from the Scalr server by the Scalarizr agent when needed.

Creating Global Variables
-------------------------

.. |SCALR_ICON| image:: images/scalr_icon_env.png
   :scale: 70%

Global Variables can be created, updated, edited, or deleted at the |Scalr|, |Account|, |Environment|, Farm, or Farm Role scopes. To create a Global Variable at the |Scalr|, |Account|, or |Environment| scopes you can click on the Scalr icon on the top left: |SCALR_ICON|

.. |GV| image:: images/gv.png
   :scale: 70%

Then click on Global Variables: |GV|

You have a few options when creating a Global Variable:

.. image:: images/new_gv.png
   :scale: 70%

.. |LOCK| image:: images/locked.png
   :scale: 60%

.. |MAN| image:: images/mandatory.png
   :scale: 60%

.. |HID| image:: images/hidden.png
   :scale: 60%

=============== ========    =============================================================
 Item           Type        Description
=============== ========    =============================================================
Name            Metadata      Name of the Global Variable

Category        Metadata      Category that the Global Variable falls into

Description     Metadata      Description of the Global Variable

|HID| Hidden    Flag          The value cannot be seen at a lower scope

|LOCK| Locked   Flag          The value cannot be changed at a lower scope

|MAN| Mandatory Flag          The value must be set at a specific scope

Custom          Format        A regular expression can be created for pattern validation

JSON            Format        The values must be in a JSON format

List            Format        The values will be presented in a dropdown
=============== ========    =============================================================

Once the Global Variable is created, click save and you will be able to use it in the various use cases below.

Using Global Variables in Scripts
---------------------------------

Global Variables can be passed to scripts that are executed through Scalr orchestration. The following examples are scripts executed on a server whose scope includes a Global Variable with the name "MyGlobalVariable".

Bash:

.. code-block:: shell

  #!/bin/bash
  echo $MyGlobalVariable

Powershell:

.. code-block:: Powershell

  #!powershell
  $env:MyGlobalVariable

Python:

.. code-block:: Python

  #!/usr/bin/env python
  import os
  print os.environ.get("MyGlobalVariable", "")

Ruby:

.. code-block:: Ruby

  #!/usr/bin/env ruby
  print ENV["MyGlobalVariable"]

Using Global Variables in Policies
----------------------------------

Another powerful use of Global Variables is to use them in policy. A common use case is to use them in conjunction with tagging or naming policies. To do this, go to Policy at the |Account| scope:

.. image:: images/policy_account.png
   :scale: 70%

In the example below, a tagging policy is created in the cloud provider which will have a tag name of "scalr_tag" and the tag value will be the value of a Global Variable named "MyGlobalVariable". Based on the brackets {} being around the value, Scalr knows to pull that as a Global Variable and insert that value into the cloud provider.

.. image:: images/gv_tag_policy.png
   :scale: 70%

This same concept can be used for other policies that allow for free form input, like hostname and instance name policies.

Examining Global Variables in Servers
-------------------------------------

Global Variables can also be referenced while working within the operating system by using the Scalarizr agent admin command: ``szradm``. For more information click on this link: **NEED TO ADD LINK***


Built-in Scalr Variables
------------------------

All of the variables above have been Global Variables that are provided by either an admin or user input. Scalr can also automatically define a certain amount of "built-in" Global Variables and inject them in the server Scope. These Global Variables are always available and they are prefixed with "SCALR" to avoid collisions with your own variables. Here is the list of the variables that can be accessed the same way as Global Variables:

Server Scope Built-In Variables
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

+---------------------------+---------------------------------------------------------------------------------------------------------------+-----------------------------------------+
| Environment Variable      | Description                                                                                                   | Sample Value                            |
+===========================+===============================================================================================================+=========================================+
| SCALR_IMAGE_ID            | Cloud Image Identifier                                                                                        | ami-43935d2a                            |
+---------------------------+---------------------------------------------------------------------------------------------------------------+-----------------------------------------+
| SCALR_EXTERNAL_IP         | External IP Address of the Server (only provided if the IP exists)                                            | 107.108.109.110                         |
+---------------------------+---------------------------------------------------------------------------------------------------------------+-----------------------------------------+
| SCALR_INTERNAL_IP         | Internal IP Address of the Server (only provided if the IP exists)                                            | 10.11.12.13                             |
+---------------------------+---------------------------------------------------------------------------------------------------------------+-----------------------------------------+
| SCALR_ROLE_NAME           | Name of the Scalr Role this Server belongs to. This is not the Farm Role Alias.                               | app-apache-ubuntu-ebs                   |
+---------------------------+---------------------------------------------------------------------------------------------------------------+-----------------------------------------+
| SCALR_ROLE_OS             | Operating System of the Role                                                                                  | Ubuntu, etc                             |
+---------------------------+---------------------------------------------------------------------------------------------------------------+-----------------------------------------+
| SCALR_ISDBMASTER          | Whether this Instance is a Role Master (only provided).                                                       | 1                                       |
+---------------------------+---------------------------------------------------------------------------------------------------------------+-----------------------------------------+
| SCALR_INSTANCE_INDEX      | Index of this Instance within its Farm Role                                                                   | 2                                       |
+---------------------------+---------------------------------------------------------------------------------------------------------------+-----------------------------------------+
| SCALR_INSTANCE_FARM_INDEX | Index of this instance within its Farm                                                                        | 1                                       |
+---------------------------+---------------------------------------------------------------------------------------------------------------+-----------------------------------------+
| SCALR_SERVER_TYPE         | Instance type                                                                                                 | c3.large                                |
+---------------------------+---------------------------------------------------------------------------------------------------------------+-----------------------------------------+
| SCALR_SERVER_HOSTNAME     | The hostname for this Server                                                                                  | app-1.example.com                       |
+---------------------------+---------------------------------------------------------------------------------------------------------------+-----------------------------------------+
| SCALR_LAUNCHED_BY_EMAIL   | The system email of the user who launched the instance                                                        | someone@company.com                     |
+---------------------------+---------------------------------------------------------------------------------------------------------------+-----------------------------------------+
| SCALR_LAUNCHED_BY_ID      | The system ID of the user who launched the instance                                                           | 1                                       |
+---------------------------+---------------------------------------------------------------------------------------------------------------+-----------------------------------------+
| SCALR_SERVER_ID           | The Server ID for this Server. This is an internal Scalr record key.                                          | 0abb9535-9d1a-4dc4-a38c-7b7b26db7bb0    |
+---------------------------+---------------------------------------------------------------------------------------------------------------+-----------------------------------------+
| SCALR_FARM_ID             | The Farm ID of the Farm this Server belongs to. This is an internal Scalr record key.                         | 5334                                    |
+---------------------------+---------------------------------------------------------------------------------------------------------------+-----------------------------------------+
| SCALR_FARM_ROLE_ID        | The Farm Role ID of the Farm Role this Server belongs to. This is an internal Scalr record key.               | 4                                       |
+---------------------------+---------------------------------------------------------------------------------------------------------------+-----------------------------------------+
| SCALR_FARM_ROLE_ALIAS     | The Farm Role Alias of the Farm Role this Server belongs to.                                                  | myrole                                  |
+---------------------------+---------------------------------------------------------------------------------------------------------------+-----------------------------------------+
| SCALR_FARM_NAME           | The Name of the Farm this Server belongs to.                                                                  | My App Production                       |
+---------------------------+---------------------------------------------------------------------------------------------------------------+-----------------------------------------+
| SCALR_FARM_HASH           | The Farm Hash of the Farm this Server belongs to. This is an internal Scalr record key.                       | cc55739bfdf844                          |
+---------------------------+---------------------------------------------------------------------------------------------------------------+-----------------------------------------+
| SCALR_FARM_OWNER_EMAIL    | The email address of the owner of the Farm this Server belongs to.                                            | user@scalr.com                          |
+---------------------------+---------------------------------------------------------------------------------------------------------------+-----------------------------------------+
| SCALR_BEHAVIORS           | A comma-separated list of the Scalr built-in automations that are active for this Server.                     | apache,nginx                            |
+---------------------------+---------------------------------------------------------------------------------------------------------------+-----------------------------------------+
| SCALR_ENV_ID              | The ID of the Environment this Server belongs to. This is an internal Scalr record key.                       | 1                                       |
+---------------------------+---------------------------------------------------------------------------------------------------------------+-----------------------------------------+
| SCALR_ENV_NAME            | The Name of the Environment this Server belongs to.                                                           | Staging                                 |
+---------------------------+---------------------------------------------------------------------------------------------------------------+-----------------------------------------+
| SCALR_CLOUD_LOCATION      | The Location where this Server is. This value is provided by your Cloud Platform.                             | us-east-1                               |
+---------------------------+---------------------------------------------------------------------------------------------------------------+-----------------------------------------+
| SCALR_CLOUD_SERVER_ID     | The Cloud ID for this Server. This value is provided by your Cloud Platform.                                  | i-866f40a8                              |
+---------------------------+---------------------------------------------------------------------------------------------------------------+-----------------------------------------+
| SCALR_CLOUD_LOCATION_ZONE | A more precise location for this Server, if available. This value is provided by your Cloud Platform.         | us-east-1a                              |
+---------------------------+---------------------------------------------------------------------------------------------------------------+-----------------------------------------+
| SCALR_CLOUD_PLATFORM      | A description of the Cloud Platform.  Available in Scalr  >=7.5.2.                                            | openstack, ec2, etc                     |
+---------------------------+---------------------------------------------------------------------------------------------------------------+-----------------------------------------+
| SCALR_ACCOUNT_ID          | The Scalr Account ID.  This is an internal Scalr record key. Available in Scalr  >=7.5.2.                     | 1, 5, etc                               |
+---------------------------+---------------------------------------------------------------------------------------------------------------+-----------------------------------------+
| SCALR_ACCOUNT_NAME        | The Scalr Account Name.  This is an internal Scalr record key. Available in Scalr  >=7.5.2.                   | Account1, Oil and Gas, Healthcare, etc. |
+---------------------------+---------------------------------------------------------------------------------------------------------------+-----------------------------------------+
| SCALR_INSTANCE_ID         | Equivalent to SCALR_CLOUD_SERVER_ID . This Global Variable is a legacy AWS specific variable.                 | i-866f40a8                              |
+---------------------------+---------------------------------------------------------------------------------------------------------------+-----------------------------------------+
| SCALR_AMI_ID              | Equivalent to SCALR_IMAGE_ID . This Global Variable is a legacy AWS specific variable.                        | ami-43935d2a                            |
+---------------------------+---------------------------------------------------------------------------------------------------------------+-----------------------------------------+
| SCALR_REGION              | Equivalent to SCALR_CLOUD_LOCATION . This Global Variable is a legacy AWS specific variable.                  | us-east-1                               |
+---------------------------+---------------------------------------------------------------------------------------------------------------+-----------------------------------------+
| SCALR_AVAIL_ZONE          | Equivalent to SCALR_CLOUD_LOCATION_ZONE . This Global Variable is a legacy AWS specific variable.             | us-east-1a                              |
+---------------------------+---------------------------------------------------------------------------------------------------------------+-----------------------------------------+

Server Scope Built-In Cost Variables
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

+------------------------+---------------------------------------------------------------------------------------------------------------------------+-------------------------------------------------+
| Environment Variable   | Description                                                                                                               | Sample Value                                    |
+========================+===========================================================================================================================+=================================================+
| SCALR_COST_CENTER_ID   | The ID of the Cost Center this Server is associated with (through the Project the Farm it belongs to is associated with). | c3146a74-3135-451e-b09e-d9882965d57f            |
+------------------------+---------------------------------------------------------------------------------------------------------------------------+-------------------------------------------------+
| SCALR_COST_CENTER_BC   | The Billing Code of the Cost Center this Server is associated with.                                                       | CLOUD-EUROPE                                    |
+------------------------+---------------------------------------------------------------------------------------------------------------------------+-------------------------------------------------+
| SCALR_COST_CENTER_NAME | The Name of the Cost Center this Server is associated with.                                                               | Europe Cloud Infrastructure                     |
+------------------------+---------------------------------------------------------------------------------------------------------------------------+-------------------------------------------------+
| SCALR_PROJECT_ID       | The ID of the Project this Server is associated with (through the Farm it belongs to ).                                   | 05650aa6-e472-4bae-8532-c57503eb5bb4            |
+------------------------+---------------------------------------------------------------------------------------------------------------------------+-------------------------------------------------+
| SCALR_PROJECT_BC       | The Billing Code of the Project this Server is associated with (through the Farm it belongs to).                          | CLOUD-EUROPE-IDENTITY                           |
+------------------------+---------------------------------------------------------------------------------------------------------------------------+-------------------------------------------------+
| SCALR_PROJECT_NAME     | The Name of the Project this Server is associated with (through the Farm it belongs to ).                                 | Europe Cloud Identity Management Infrastructure |
+------------------------+---------------------------------------------------------------------------------------------------------------------------+-------------------------------------------------+
