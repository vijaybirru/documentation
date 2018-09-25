.. include:: ../GLOBAL.rst

.. _chef:

Chef Integration
================

Definition and Scope
--------------------
|SCOPE_SCALR| |SCOPE_ACC| |SCOPE_ENV| |SCOPE_ROLE| |SCOPE_F_ROLE|

Scalr provides a built-in integration with Chef allowing you to add servers built by Scalr to Chef for configuration management.

.. |chef_doc| raw:: html

   <a href="https://docs.chef.io/" target="_blank">Chef Documentation</a>

Find out more about Chef here: |chef_doc| |NEWWIN|

Adding a Chef Server
--------------------

Chef servers can be added at the |Scalr|, |Account|, or |Environment| scope. To add a Chef server click on the Scalr icon on the top left |MENU_ACC| and click on Chef Servers. In the Chef Servers page, click on New Chef Server and you will be prompted for the following:

.. image:: /chef/images/new_chef_servers.png
   :scale: 40%

.. csv-table::
    :header-rows: 1
    :file: csv/chef_server.csv

Using Chef with Scalr
---------------------

|SCOPE_ROLE| |SCOPE_F_ROLE|

To use Chef with Scalr, the images that you are building from must have the Chef Client installed on them.

Chef Bootstrapping can be added in two places:

* The Role scope which would force the configuration on all servers built using that Role.
* The Farm Role scope which would force the configuration on all servers built using that Farm Role.

Role Scope
^^^^^^^^^^

.. include:: /images_roles/creating_roles.rst
   :start-after: chef_roles_start
   :end-before: chef_roles_end

Farm Role Scope
^^^^^^^^^^^^^^^^

The Bootstrap config can also be added directly into a Farm Role if the Role allows for it. To do this, go into the Farm Role and click on Bootstrap with Chef. Within here you can add Chef Roles, Runlists, Cookbooks, and more.

.. image:: /chef/images/farm_role_chef.png
   :scale: 70%

Troubleshooting
----------------

If you need to troubleshoot any issues related to your Chef Cookbooks, all logs from the Chef Client are displayed in the Orchestration Logs tab in the |Environment| scope.
