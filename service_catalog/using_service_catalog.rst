.. include:: ../GLOBAL.rst

.. _sc_using:

Self Service via the Service Catalog
====================================
|SCOPE_ENV|

Scalr provides Cloud Deployment Self Service via the Service Catalog. This capability enables simple deployment of even the most complex cloud based services and applications at the click of a button. The Service Catalog is available to all types of users of Scalr including development teams, QA and non-technical end-users. In the case of non-technical end users Scalr can be configured to provide only the Service Catalog functionality by associating end user teams with restricted :ref:`access_control`. This results in end users seeing a very limited set of menu options.

.. image:: images/sc_user_menu.png
   :scale: 40%

The Service Catalog provides a list of predefined offerings that contain all the necessary configuration details to create Applications and deploy them to the Cloud. Users can select an offering from the list and then request to create an application from it. The user will be prompted for various input according to configuration before the Application is launched.

The Service Catalog itself is accessed from the Main Menu.

.. |SC1| image:: /service_catalog/images/sc_menu_1.png
         :scale: 30%

Clicking on |SC1| itself opens the list of available offerings to allow users to request applications. "My Applications" opens the screen of already created applications.

Requesting Applications
-----------------------

.. |REQ| image:: images/request.png
   :scale: 40%

The Service Catalog selection screen will, by default, show all available offerings. Offerings can optionally be grouped into Categories by the person who sets up the Service Catalog. Users can refine the list of available offerings by selecting a category from the search bar drop down and/or by typing filter text into the search bar.

.. image:: images/sc_select.png
   :scale: 40%

Click on the |REQ| button to start the Application creation dialogue.

In the simplest case users may only be asked to provide a name for the new application before reviewing and launching. At the other extreme the user could be asked to enter a number of choices and detail. The amount of input required is governed by the configuration of the offering and any Policies that are in place for the |ENVIRONMENT|.

The following screens walk through an example where significant user input is required.

**Set the name and Project**

.. image:: images/simple_2_general.png
   :scale: 50%

**Choose the Cloud, Location and cloud specific parameters**

Note that the input parameters are tailored to the chosen cloud.

.. |M1| image:: images/multi_cloud_1.png
        :scale: 40%

.. |MAWS| image:: images/multi_cloud_aws_2.png
        :scale: 40%

|M1| |MAWS|

Note how mandatory parameters can be highlighted in red if incomplete or invalid entries are submitted.

**Review and Launch**

Review the deployment parameters and then Create and Launch.

.. image:: images/review.png
   :scale: 50%

If any amendments are required click on the appropriate "STEP" tab on the left hand side to make the changes.

Managing Applications
---------------------

After launching the application the "MY APPLICATIONS" will be displayed and will show the status of the Application request.

.. image:: images/apps_prov.png
   :scale: 40%

This screen can also be accessed from the |MENU_ENV|.

.. image:: images/sc_user_menu.png
   :scale: 40%

From here applications can be Started, Suspended, Terminated (Stop), Deleted and Locked. The Delete and Start buttons are only visible when an application is in a Stopped stated. The Lock button disables the the other available buttons to minimise the risk of accidentally changing the state of an application.

.. |ACT1| image:: images/app_actions.png
          :scale: 40%

.. |ACT2| image:: images/app_actions_2.png
          :scale: 40%

|ACT1| |ACT2|

Click on the Application to see more details including a list of the Servers that are being launched and their IP Addresses.

.. image:: images/app_svr_detail.png
   :scale: 40%
.. |DASH| image:: images/dash_button.png
          :scale: 40%

Access to the dashboard for each server is through the |DASH| button alongside each server in the list. This gives access to full details of each server, including the Health statistics.

.. image:: images/svr_dash.png
   :scale: 40%
