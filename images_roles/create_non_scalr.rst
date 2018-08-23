.. include:: ../GLOBAL.rst

.. _images_from_servers:

Creating Images and Roles from Non-Scalr Servers
================================================

.. warning:: This option will suspend the cloud server whilst the snapshot for the image is taken.

The workflow for creating an Image and Role from a non-scalr server is the same for all clouds.

* Select and prepare the server to be imaged
* Install Scalarizer
* Run Scalarizer
* Confirm installation

**Step 1 : Prerequisites**

Before starting you must ensure your environment and the server meets the following prerequisites.

1. You have login access to the server with root (via sudo) access for Linux or Administrator access for Windows.
2. The install OS is supported as listed in :ref:`supported-os-start`.
3. Open inbound network ports 8008,8010 and 8013 for the server.
4. Open outbound network ports 80, 443, 5671 for the server. See :ref:`net-req-start` for more details.

**Step 2 : Prepare Server for Imaging**

Prior to imaging the Server, ensure that you complete common Image preparation steps required by your organization. (You will need to take a snapshot of the server prior to this preparation if you wish to continue using the server afterwards)

Examples of such steps include:

Linux:

* Updating all packages
* Cleaning package manager caches
* Remove SSH Public Keys (from authorized_keys files)
* Remove SSH Host Keys (from /etc/ssh)
* Clear shell history

Windows:

* Sysprep

All:

* Remove credentials found on the instance

.. warning:: DO NOT logout of the server after performing these preparatory tasks. You need to be logged in to install Scalarizr.

**Step 3 : Creating the Image/Role**

This option can be accessed from either the Images or Roles Library by clicking on either Images or Roles in the Bookmark Bar.

.. image:: images/images_cfns.png
   :scale: 50%

You will then be presented with the following screen on which you can name the new Image/Role and select the Cloud and target server to be imaged.

.. image:: images/cfns_1.png
   :scale: 50%

.. |ONLY_IMG| image:: images/only_image.png
              :scale: 50%

.. note:: Regardless of which way you navigate to this option you will be presented with the same screen under the Roles heading. The only difference is that the "Only create image..." check box is already checked when navigating from the Images list. |ONLY_IMG|

After choosing the cloud and location the Server drop down list will show all the servers. Only servers that are not already imported will show as "Available to import". Select the required server and click "START BUILDING".

You will be presented with a screen similar to this.

.. image:: images/cfns_2.png
   :scale: 50%

Proceed as follows:

1. Click on the command window under "INSTALL SCALARIZER" and copy the contents to your paste buffer.
2. Switch to the command shell for the server. Note for Windows ensure the Power Shell is running as Administrator.
3. Paste the commands in and run. When complete go back to the Scalr UI.
4. Click on the command window under "LAUNCH SCALARIZER" and copy the contents to your paste buffer.
5. Switch to the command shell for the server. Note for Windows ensure the Power Shell is running as Administrator.
6. Paste the commands in and run. On Linux ensure the commands are prefixed by ``sudo``.
7. When the Launch command shows ``2018-08-14 15:11:07+01:00 - INFO  - Service main loop (Linux)`` or similar go back to the UI and click on "CONFIRM SCALARIZR LAUNCH".

Scalr will now snapshot the server and build the Image (and Role).

.. image:: images/cfns_3.png
   :scale: 50%

.. |IMPORTING| image:: images/importing.png
               :scale: 40%

It will take Scalr a few minutes to run through all the steps required.

Whilst the build is running you will be able to continue using Scalr for other tasks. To return to the build screen to review progress you should navigate to the Servers list and click on |IMPORTING| for the relevant server.

Once the build is complete you can assign the Image to a Role and start using the Role in Farms.
