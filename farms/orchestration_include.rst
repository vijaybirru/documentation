.. Generic Include file to cover Orchestration rules
.. To be included in /farms/index.rst and /images_roles/creating_roles.rst
.. It assumes these files contain an appropriate heading and relevant instructions on how to navigate to Orchestration in the UI
.. Screenshots will come from Farm Role Orchestration.

.. note:: Orchestration rules can be defined in many places in Scalr. What follows covers all aspects of rule configuration regardless of where they are configured.

Orchestration Rules are made up of three main elements.

.. csv-table::
   :widths: 15,60

   **Trigger Event**,The lifecycle event of the a server that will cause the Orchestration Rule Script to execute such as OnHostUp or BeforeHostTerminate
   **Target**,Criteria for identifying the server on which to run the Script which need not be the triggering server and can be multiple servers
   **Action**,"The script, Chef Cookbook or Ansible Tower job to be run."

.. image:: /farms/images/orch_rule_new.png
   :scale: 50%

You must create the :ref:`Script <scripts>` and any :ref:`gvs` that are required before creating the Rule.

Trigger Event
*************

First select the Trigger Event for this rule. The following table describes each event and the state of the Server when the event fires.

.. csv-table:: Orchestration Events
   :header-rows: 1
   :widths: 20,60
   :file: csv/event_reference.csv


After an Instance finishes booting the OS, the Scalr Agent starts configuring your Environment in a certain order as follows.

* All EBS / Disk Routines are executed.
* Deployment Routines are executed.
* Server Configuration (including vhosts) Routines are executed. If you wish to work with Virtual Hosts, you can assign a Script to the BeforeHostUp Event.

Target
******

You must define the target for executing the script. The default is to execute only on the instance that triggered the event. The other options are as follows. Note that availability of targets depends on the scope at which the rule is being defined.

.. csv-table::
   :header-rows: 1
   :widths: 25,15,50

   Target,Scopes,Description
   Triggering Server,|SCOPE_ROLE| |SCOPE_F_ROLE|,The script will only be executed on the server that triggered the event.
   Triggering Server with <specified OS>,|SCOPE_SCALR| |SCOPE_ACC| |SCOPE_ENV|,The script will only be executed on the server that triggered the event providing it is the specified Operating System.
   All Servers in the Farm,|SCOPE_ROLE| |SCOPE_F_ROLE|,The script will be executed on all running servers in the Farm.
   All Servers of the Farm Role,|SCOPE_ROLE|,Script will execute for all servers running from the same Farm Role as the triggering server in the Farm.
   All Roles with Selected Tags,|SCOPE_SCALR| |SCOPE_ACC| |SCOPE_ENV| |SCOPE_F_ROLE|,Script will execute for all servers running from Roles with the specified tag in the Farm.
   All Roles with Selected OS,|SCOPE_F_ROLE|,Script will execute for all servers in the Farm with the specified OS.
   Selected Farm Roles,|SCOPE_F_ROLE|,Script will execute for all servers in the given Farm Role(s) in the Farm.

Action
******

There are three choices for the Action for a rule.

.. |SHARED| image:: /farms/images/shared.png
            :scale: 40%

.. csv-table::
   :header-rows: 1
   :widths: 7,20,15,58
   :file: csv/actions.csv

Advanced Configuration
**********************

The advanced configuration section allows you to control various aspects of how the Action is executed.

.. csv-table::
   :header-rows: 1
   :widths: 20,80

   Parameter,Description
   Execution Mode,Blocking: Scalarizr will wait for your Script to finish executing before firing and processing further events
                 ,Non-Blocking: Scalarizr will not wait for your Script to finish executing before firing and processing further events
   Timeout       ,"Length in seconds before the script should timeout. This should be increased for complex actions, especially those that download from the internet."
   Order         ,Sequence in which rules must be executed. This defaults to the order in which the rules are created.
   Run As        ,For Scripts and Chef only defines the user to execute the script as on the server.
