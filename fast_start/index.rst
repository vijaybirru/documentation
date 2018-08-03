.. include:: ../GLOBAL.rst

.. _simple_farm:

Building a Simple Farm
======================

Keen to get started?

Just want to build a Farm and learn the details later?

This page does exactly that. No frills rapid farm building to create a simple web site.

**Prerequisites**

1. You have a login to Scalr and access to the Farm menu, in |ENVIRONMENT| Scope
2. You can see a list of base roles as shown below, or there is an Ubuntu base role of some sort available. (If you cant see these roles ask your Admin to run `scalr-server-manage sync_shared_roles`)

.. image:: images/roles.png

Overview
--------

We will be doing the following using an Ubuntu Role. Don't worry if Linux or Ubuntu isn't your thing, you wont even need to login to Linux to get this working.

* Create a Farm
* Add a Farm Role
* Configure it to install Apache on boot up
* Configure web page on boot up
* Launch and test

Fast Farm Build
---------------

1. Login to Scalr and navigate to a suitable |ENVIRONMENT| scope via the |ENVIRONMENT| menu.

.. image:: images/env_menu.png
   :scale: 50%

2. On the Dashboard enter a Farm name and Project in the "CREATE NEW FARM" widget and click "CREATE NEW FARM"

.. image:: images/farm_widg.png
   :scale: 50%

3. Click on "ADD FARM ROLE", the click on "Base". Select a small Instance Type and adjust the network settings as required. Your Admin can advise you on which network to use. When ready click on "ADD TO FARM".

.. image:: images/farm_3.png

.. |SAVL| image:: images/save_launch.png
          :scale: 50%

Now Click on the arrow next |SAVL| and then click "SAVE FARM". The farm will be saved and you will be shown a list of Farms. We will comeback to the Farm in a moment.

We now need to create scripts to configure the servers in the Farm.

Script 1 - Install Apache

4. Click on the Main Menu and then on Scripts -> ADD NEW

.. image:: images/scripts_new.png

5. Create a script as shown in the screen shot below. The code is below that for easy copy/paste. Be sure to set the timeout to 1800.

.. image:: images/script_apache.png

.. code-block:: shell

   #!/bin/bash
   apt-get install -y apache2; service apache2 start

6. Now create a second script to create the web site. Call this one "Install Web" and set the timeout to 1800. The code for the script is as follows.

.. code-block:: shell

   #!/bin/bash
   echo "$CUSTOM_MESSAGE" > /var/www/html/index.html

We now need to add the Orchestration to the Farm Role and set up the CUSTOM_MESSAGE variable for the script.

.. |CONF| image:: images/farm_conf.png

5. Click on Farms, find your farm in the list and click on |CONF|. The Farm Role will shown in the left hand side panel. Click on it.

.. image:: images/farm_4.png

6. Click on "ORCHESTRATION", then "NEW RULE" and select the TRIGGER EVENT = "BeforeHostUp", Set the Scalr Script to "Apache Install".

.. image:: images/rule_apache.png

7. Now click on "NEW RULE" again and add a rule for the with the "Install Web" script for the same event (BeforeHostUp).

.. image:: images/rule_web.png

8. Now click on "GLOBAL VARIABLES" and create a new variable called CUSTOM_MESSAGE with the value "Hello World".
.. image:: images/gv.png

9. Finally we need to make sure you can access the web site via port 80. Click on Security -> ADD SECURITY GROUPS -> NEW SECURITY GROUPS and create a new group with a rule that allows TCP Port 80. Be sure to Add the group. **Now SAVE the farm**.

.. image:: images/port80.png

Ok, lets launch...!

.. |LAUNCH| image:: images/launch.png

.. |SVRL| image:: images/servers_link.png

9. In the farm list click the launch |LAUNCH| and confirm by clicking "LAUNCH". Then click on the Server link |SVRL| in the farm list to watch your server launch.

After a while the Server will transition through "Initializing" to "Running". When it is running grab the Public IP and browse to it in your browser of choice. You should see this.

.. image:: images/web.png

**What Next?**

* Go and edit the value of the Global Variable and stop and relaunch the Farm.
* Move on to read more about Scalr infrastructure management, staring with :ref:`images_roles`.
