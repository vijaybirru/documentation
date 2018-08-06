.. Generic Include file to cover Orchestration rules
.. To be included in /farms/index.rst and /images_roles/creating_roles.rst
.. It assumes these files contain an appropriate heading and relevant instructions on how to navigate to Orchestration in the UI
.. Screenshots will come from Farm Role Orchestration.

Orchestration Rules are made up of three main elements.

.. csv-table::
   :widths: 15,60

   **Trigger Event**,The lifecycle event of the a server that will cause the Orchestration Rule Script to execute such as OnHostUp or BeforeHostTerminate
   **Target**,Criteria for identifying the server on which to run the Script which need not be the triggering server and can be multiple servers
   **Action**,The script to be run or the Ansible Tower job to be run if Ansible Tower is configured for the Role.

.. image:: /farms/images/orch_rule_new.png
   :scale: 50%

You must create the :ref:`Script <scripts>` and any :ref:`gvs` that are required before creating the Rule.

First select the Trigger Event for this rule. The following table describes each event and the state of the Server when the event fires.

.. csv-table:: Orchestration Events
   :header-rows: 1
   :widths: 20,60
   :file: event_reference.csv


After an Instance finishes booting the OS, the Scalarizer Agent starts configuring your Environment in a certain order as follows.

* All EBS / Disk Routines are executed.
* Deployment Routines are executed.
* Server Configuration (including vhosts) Routines are executed. If you wish to work with Virtual Hosts, you can assign a Script to the BeforeHostUp Event.

You must define the target for executing the script. The default is to execute only on the instance that triggered the event. The other options are as follows. Note that availability of targets depends on the scope at which the rule is being defined.

.. csv-table::
   :header-rows: 1
   :widths: 25,15,50

   Target,Scopes,Description
   Triggering Server,|SCOPE_ROLE| |SCOPE_F_ROLE|,The script will only be executed on the server that triggered the event.
   Triggering Server with <specified OS>,|SCOPE_SCALR| |SCOPE_ACC|,The script will only be executed on the server that triggered the event providing it is the specified Operating System.
   All Servers in the Farm,|SCOPE_ROLE| |SCOPE_F_ROLE|,The script will be executed on all running servers.
   All Servers of the Farm Role,|SCOPE_ROLE|,Script will execute for all servers running from the same Farm Role as the triggering server.
   All Roles with Selected Tags,|SCOPE_SCALR| |SCOPE_ACC| |SCOPE_F_ROLE|,Script will execute for all servers running from Roles with the specified tag at or below the scope at which the rule is defined.
   All Roles with Selected OS,|SCOPE_F_ROLE|,Script will execute for all servers in the Farm with the specified OS.
   Selected Farm Roles,|SCOPE_F_ROLE|,Script will execute for all servers in the given Farm Role(s).
