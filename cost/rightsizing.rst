.. include:: ../GLOBAL.rst

.. _rightsizing:

Rightsizing
===========
|SCOPE_ENV|

Scalr has the ability to rightsize servers based on the metrics it collects from them using the Scalarizr agent. Scalr will not automatically rightsize the servers for you, but will provide recommendations and projected savings based on changing the server size. A server needs to be up for a minimum of 48 hours with the Scalarizr agent running before a recommendation can be made.

To utilize Rightsizing, you first need to logged into the |Environment| scope. Once you are in the |Environment| scope, there are a few ways to get to the Recommendations page:

1. Go to the main Servers page and you will see those instances that have a recommendation (only 2 servers have a recommendation in this screenshot):

.. image:: images/rightsizing1.png
   :scale: 40%

2. The other option is to go to the main Scalr menu dropdown on the top left |MENU_ENV| and select Cost Manager and then Recommendations:

.. image:: images/rightsizing2.png
   :scale: 40%

Once you are in the Recommendations page, you will see the usage over the period of time selected as well as the Current/New instance type that is recommended as well as projected savings. To complete the rightsizing, verify the new instance type and select Resize on the bottom right:

.. image:: images/rightsizing3.png
   :scale: 40%
