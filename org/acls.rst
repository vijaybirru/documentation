.. include:: ../GLOBAL.rst

.. _access_control:

Access Control Lists
====================

|SCOPE_ACC|

Access Control Lists allows you restrict the permissions for users and/or teams, so that they only have access to Scalr features their work requires.

.. note::

  Scalr Access Control Lists apply to both the Scalr UI and the Scalr API

Understanding Access Control
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

There are two types of Access Control in Scalr:

* Access to Environments (e.g. ability to view the Production Environment).
* Permission to use a given feature within a specific Environment (e.g. ability to create Farms in the Production Environment).

Note that access to an Environment alone doesn't let a user do anything unless they also have permissions within that Environment. To learn more about giving users and teams access to an environment, please go to the :ref:`teams_users` page.

Permissions are granted through Teams and Access Control Lists (ACLs). ACLs are sets of permissions. Permissions are scoped, which means a user may have different permissions across different Environments within Scalr.

To determine whether a user has a given permission within a given Environment, Scalr checks whether any team that grants that user access to that Environment is associated with an ACL that grants that permission. Note that this means ACLs are cumulative (multiple ACLs that give access to the same Environment result in the permissions from all these ACLs being granted).

For permissions that are relevant in the Account Scope, all teams the user is a member of (and all associated ACLs) are taken into account.

Here's an example:

* User John Doe is a member of the teams Developers and Testers
* Team Developers is associated with the ACL Development
* Team Testers is associated with the ACL Test
* Team Developers grants access to the Development Environment.
* Team Testers grants access to the Development and Staging Environments.
* The Development ACL grants the permission to Manage Roles
* The Test ACL grants the permission to Manage Environment-Scope Scripts and the permission to Manage Account-Scope Webhooks.

Then,

* John Doe has access to the Development and Staging Environments, but he does not have access to a hypothetical Production Environment.
* John Doe has permission to Manage Roles and Environment-Scope Scripts in the Development Environment.
* John Doe has permission to Manage Environment-Scope Scripts in the Staging Environment.
* John Doe has permission to Manage Account-Scope Webhooks.

Creating an ACL
^^^^^^^^^^^^^^^

To create an ACL in Scalr, log into the |Account| scope, click on the main Scalr menu on the top left |MENU_ACC|, and go down to ACL.

Click on New ACL, set the ACL Name and then select the Default Permissions to start out with. The default gives a starting point, you can start configuring the ACL from there:

.. image:: /org/images/new_acl.png
   :scale: 70%

A few of the ACLs, like Farms, have an extra level of granularity to account for users and teams:

* Farms you Own - You will only see your farms, and these permissions will only apply to your farm.
* Farms Your Teams Own - You will only see your teams farms, and these permissions will only apply to your teams farms.
* All Farms - You will see all farms within an environment, and these permissions will apply to all farms.

Now that the ACL is created, go to the :ref:`teams_users` to learn how to assign the ACL to a team.
