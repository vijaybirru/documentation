.. include:: ../GLOBAL.rst

.. _manual_scaling:

Manual Scaling
==============

Definition and Scope
--------------------

|SCOPE_F_ROLE|

For those use cases where you may not have an application that has a fully automated deployment or it just doesn't need to be autoscaled, Scalr has the option to allow users to initiate the provisioning of servers.

Using Manual Scaling
--------------------

To enable manual scaling in your Farm Role, find your Farm, click on the Farm Role, go to the Scaling tab and make sure it is set to Manual:

.. image:: images/manual_scaling.png
   :scale: 60%

Manually Launching Servers
--------------------------

.. |ROLE| image:: images/roles_column.png
   :scale: 100%

Once you have set the the Farm Role to manual scaling and launched your Farm, you will now have to manually launch a server. To do so, go to the Farms page, find your Farm, and click on the number in the Roles |ROLE| column (Number 3 in the example below):

.. image:: images/dashboard_roles_column.png
   :scale: 60%

.. |LAUNCH| image:: images/launch_button.png
      :scale: 100%

That will bring you to the Farm Roles pages for that specific Farm. Within this page, click on the launch |LAUNCH| button for the Farm Role that you want provision a server for on the right-hand side:

.. image:: images/farmrole_launch.png
   :scale: 60%


Manually Terminating Servers
----------------------------

Just like you have to manually launch a server when scaling is set to manual, the same applies to terminating servers. To terminate a server, go to the servers pages, find the server you want to terminate and click on the Terminate Server button:

.. image:: images/terminate_server.png
   :scale: 60%
