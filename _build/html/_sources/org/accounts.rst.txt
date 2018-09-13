.. include:: ../GLOBAL.rst

.. _accounts:

|ACCOUNT| & |Environment| Configuration
========================================

|SCOPE_SCALR| |SCOPE_ACC|

An |Account| is a child of the |Scalr| scope as it will inherit anything that is placed or assigned to it at the |Scalr| scope and it is a parent to |Environments|, which is one of the core concepts behind Scalr that makes it a truly multi-tenant tool.  Each account has an owner.  A Scalr instance may contain as many |Accounts| as you wish. |Accounts| contain one or more |Environments|. Generally, |Accounts| correspond to Organizations, Business Units, Customers, or just a logical way to segment resources and users.

Creating |Accounts|
-------------------

|SCOPE_SCALR|

|Accounts| can only be created by :ref:`global_admin`. To create an |Account|, first ensure you are logged into the |Scalr| scope as a Global Administrator. Next, click on the main Scalr menu on the top left |MENU_SCALR|, and go down to Accounts.

.. image:: /org/images/new_account.png
   :scale: 70%

Click the New Account button, which will prompt you for a Name, Owner, and Cost Center, all mandatory fields:

.. image:: /org/images/new_account1.png
   :scale: 70%

After creating an account, you can move on to creating the environments within the account.

.. _environments:

Configuring |ENVIRONMENTS|
--------------------------

|SCOPE_ACC|

An |Environment| is a child of an |Account| and will inherit anything that is placed or assigned to it at the |Account| level. Each |Environment| is connected to one or more cloud platforms. One or more teams can be granted access to each |Environment|. |Environments| can correspond to

* An SDLC environment: Dev, QA, or Prod
* An application
* A logical group of physical resources: Non-Prod and Prod
* Or More

There isn't a "rule" for what an |Environment| can be, it is just a way to add more multi-tenancy and logical groupings to Scalr.

Creating |Environments|
-----------------------

|Environments| can only be created by |Account| administrators. To create an |Environment|, first ensure you are logged into the |Account| scope. Next, click on the main Scalr menu on the top left |MENU_ACC|, and go down to |Environments|.

.. image:: /org/images/new_env.png
   :scale: 70%

Click on New Environment, enter the Name and Cost Center, either of which can be changed at a later time, and Save.

Managing |Environments|
-----------------------

At this point you can do the following with |Environments|:

* :ref:`cloud_creds`
* :ref:`policy_link`
* :ref:`apply_quotas`
* :ref:`teams_env`

If for any reason you need to suspend the Scalr management of an Environment, click on Suspended at the top right of the Environment page:

.. image:: /org/images/env_suspend.png
   :scale: 70%

This will suspend API calls to the Cloud Providers, it will not terminate or cause any damage to the running resources.
