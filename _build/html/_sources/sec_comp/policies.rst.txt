.. include:: ../GLOBAL.rst

.. _policy_engine:

Policy Engine
=============

|SCOPE_ACC|

The Policy Engine is part of the |ACCOUNT| Scope, thus enabling business units to implement consistent governance policies across all their cloud environments.

.. image:: images/policy_menu.png
   :scale: 50%

There are three steps to defining and enabling policies.

1. Create a Policy Group.
2. Add Policies and policy conditions to the Policy Group.
3. Link the Policy group to the required |ENVIRONMENTS|.

Policy conditions provide fine grained control over the application of a policy, allowing for policy variations across different clouds, locations cloud accounts and more.
Scalr also provide the ability to implement policies based on :ref:`policy_tags`.

Creating Policy Groups
----------------------

Policies are defined by clicking on Policy Engine -> Policy Groups -> NEW POLICY GROUP which will display this screen.

.. image:: images/pg_blank.png
   :scale: 100%

Policy Groups require a Name and Type. The Type determines the options available for Policy Rules and includes types related to all clouds and cloud specific types. Cloud specific types will only appear in the drop down if there are Cloud Credentials configured for that cloud at either the |SCALR| scope or in the currently active |ACCOUNT|.

.. image:: images/pg_types.png
   :scale: 40%

The Policy Reference below explains the policy types and their associated rules.

Creating Policies
-----------------

Click on "New Policy" to add a policy rule. Policies available to the chosen Policy Group type will be displayed. This example show "Configuration" policies.

.. image:: images/cfg_policies.png
   :scale: 40%

.. |REC| image:: images/reclamation.png
         :scale: 30%

.. note:: For type type "Reclamation" there are no further options and you will be taken straight to the screen to configure the reclamation policy. |REC|

Click a policy and you will be presented with a screen specific to that policy on which you can set policy conditions and details of the policy itself. This is an example of ``scalr.server.hostname.template`` policy.

.. image:: images/policy_example.png
   :scale: 40%

All Conditions are optional.

Make sure the status is set to "ENFORCED" to enable the policy.

.. |SAVE| image:: images/save.png
         :scale: 30%

After defining the policy you can add further policies to the policy group. Remember to click "Save" |SAVE|.

Using Global Variable in Policies
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Global Variables in Policies make it possible to vary the details of the Policy at any level where Global Variables can be set. A good example of this is a policy that enforces tagging on servers. The ``cloud.tags`` policy is available for all cloud types and provides a list of tags that must be applied to servers from every Farm Role the policy applies to. In this example the policy effectively applies to all Farm Roles in all environments the Policy Group is linked to.

.. image:: images/gv_tag_policy.png
   :scale: 50%

By using a Global Variable name (in this example. `{MyGlobalVariable}`) rather than an actual value, the value applied to the tag will be determined from the Global Variable at the time the server is launched, based on the value of the variable at that time. Depending on where the variable is defined and it's permissions the value could be set as low down as the Farm Role scope.

For more details see :ref:`gvs`.

.. _policy_tags:

Policy Tags
-----------

|SCOPE_SCALR| |SCOPE_ACC|

Policy Tags provide fine grained control over which Roles a policy will apply to. Policy Tags are defined by the Scalr Administrator at |SCALR| scope and can be applied to Policies and Roles to determine which Roles a Policy applies to. Policy Tags must be defined at the |SCALR| scope BEFORE they can be used in Policies at the |ACCOUNT| scope.

.. note:: Policy Tags are entirely separate for role tags. Although Policy Tags are applied to Roles in the same way as normal role tags it is NOT possible to use existing role tags as Policy Tags. You must define new Policy Tags for this purpose.

To create Policy Tags login as the Scalr Admin at |SCALR| Scope and navigate to **Policy Engine -> Policy Tags**. Click on NEW POLICY TAG and enter a name for the tag.

.. |PT| image:: images/policy_tag_menu.png
        :scale: 40%

.. |NPT| image:: images/new_policy_tag.png
         :scale: 70%
         :align: top

|PT| |NPT|

To apply Policies Tags to a Policy include these in the conditions of the policy.

.. image:: images/apply_pol_tag.png
           :scale: 40%

Back at |SCALR| scope under **Policy Engine -> Policy Tags** you will be able to see which accounts are using each Policy Tag.

.. image:: images/tag_usage.png
           :scale: 70%

Linking Policy Groups to |Environments|
---------------------------------------

Policy Groups will only take effect when they are linked to |Environments|. You can only link one Policy Group of each type to an |ENVIRONMENT|.

Click on ENVIRONMENTS in the Bookmarks Bar or Main menu and select the environment you wish to link Policy Groups to.

.. image:: images/link_1.png

Click on the link icon on the right-hand side, link the required Policy Group to the environment, and save.

.. image:: images/link_2.png


Policy Reference
================

.. |BR| raw:: html

   <br>


Configuration Policies
----------------------

.. csv-table::
   :header-rows: 1
   :file: config_policies.csv

Container Policies
------------------

.. csv-table::
   :header-rows: 1
   :file: container_policies.csv

Reclamation Policies
--------------------

Reclamation policies enforce automatic termination of Farms after specified periods. This helps to ensure unwanted servers are not running up costs after they are no longer required. Admins can set Reclamation policies on typically fixed duration |ENVIRONMENTS| such as QA testing, short term projects etc. Reclamation polices define 3 things.

1. The duration of a Farms running lifetime.
2. Notifications to be sent prior to automatic termination.
3. Maximum number and duration of lease extension requests a Farm owner can make (Standard Requests).

.. note:: Farm owners can make Non-Standard Lease Extension requests. Standard requests are considered pre-approved and will come into effect immediately. Non-standard requests must be approved by the |ACCOUNT| Admin before they will come into effect.

.. image:: images/reclamation.png
   :scale: 50%

Cloud Service Gateway Policies
------------------------------

.. csv-table::
   :header-rows: 1
   :file: csg_policies.csv

Cloud Generic Policies
----------------------

.. csv-table::
   :header-rows: 1
   :widths: 20,6,6,6,6,6,25,25
   :file: generic_policies.csv

AWS Policies
------------

.. csv-table::
   :header-rows: 1
   :file: aws_policies.csv

Azure Policies
--------------

.. csv-table::
   :header-rows: 1
   :file: azure_policies.csv

Google Compute Engine Policies
------------------------------

.. csv-table::
   :header-rows: 1
   :file: gce_policies.csv

Openstack Policies
------------------

.. csv-table::
   :header-rows: 1
   :file: openstack_policies.csv

VMware Policies
------------------

.. csv-table::
   :header-rows: 1
   :file: vmware_policies.csv
