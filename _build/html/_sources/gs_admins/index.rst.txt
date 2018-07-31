.. include:: ../GLOBAL.rst

Getting Started for Admins
==========================

This page provides the basic information needed by |SCALR| and |ACCOUNT| admins to get Scalr up and running and configured for end users to start work.

**Prerequisite:** Scalr Server has been installed (See :ref:`install`) and you are able to login as either a |SCALR| or |ACCOUNT| admin.

Role of an Administrator
---------------------------

An Administrator's role can vary from organisation to organisation and admin tasks can be performed at various scopes within Scalr. Some tasks can only be done at one specific scope and some are available at all 3 scopes. The unique aspects of these roles can be summarised as follows.

* **Scalr Admin**

 * Set up Accounts
 * Set Cost Centers (and other aspects Cost Analytics)
 * Configuration items to be used across all |ACCOUNTS|

    * Scripts, Global Variables and Orchestration rules.
    * Images and roles

* **Account Admin**

  * Create |Environments|
  * Set up governance policies via the Policy Engine
  * Set up Users, Teams and Access Control Lists
  * Configuration items to be used across all |Environments| in the |ACCOUNT|.

     * Scripts, Global Variables and Orchestration rules.
     * Images and roles

All tasks can be performed by clicking on the appropriate on the main menu button |MENU_SCALR| |MENU_ACC|.

The table below describes the core tasks that Admins must perform in order for End Users to be able to login, configure farms and deploy cloud infrastructure.
This is NOT a comprehensive list of all features and functionality available in Scalr

.. |LS| image:: ../images/scope_scalr.png
                 :scale: 40%

.. |LA| image:: ../images/scope_acc.png
                 :scale: 40%

.. |LE| image:: ../images/scope_env.png
                 :scale: 40%

=========================================  ================ ===================== ===========
Task                                       Scopes           Menu Item             Description
=========================================  ================ ===================== ===========
Set up Cost Centers                        |LS|             Cost Analytics        | Cost Centers are critical to enabling useful sub-divisions of Cost Analytics.
                                                                                  | Each |ACCOUNT| must be associated with a Cost Center, so it is advisable to set up Cost Centers before setting up |Accounts|.
                                                                                  | More detail can be found at :ref:`cost_control`.
Create |Accounts|                          |LS|             Accounts              | |Accounts| must be created to match the desired organisational structure.
                                                                                  | |Accounts| must be allocated a Cost Center and assigned an owner to be the |ACCOUNT| administrator.
                                                                                  | More detail can be found at :ref:`accounts`.
Set Up Users                               |LS| |LA|        Users                 | If users are NOT being external authenticated via LDAP or SAML they must be created in Scalr.

                                                                                  .. note:: Users are unique throughout Scalr and can have access to multiple accounts. They can be created at |SCALR| or |ACCOUNT| scope but it is recommended that all User and Team management is done at |ACCOUNT| scope. The exception being that only the Scalr admin can assign Global and Cost Manager Admin privileges to a user.
                                                                                  
                                                                                  | See :ref:`teams_users`.
Configure ACLs                             |LA|             ACL                   | Scalr comes with 3 pre-configured ACL's. You can use these or create your own to match your requirements.
                                                                                  | See :ref:`access_control`.
Set up Teams                               |LA|             Teams                 | Access to environments is configured via Teams. Teams must be created, linked to ACL's and assigned Users as team members.
                                                                                  | Teams must be linked to each environment they require access to.
                                                                                  | If you are using LDAP for authentication the teams will automatically appear in Scalr based on the LDAP group names. You cannot set up or change LDAP based teams within Scalr, but you must still allocate an ACL.
                                                                                  | See :ref:`teams_users`.
Configure Cloud Credentials                |LS| |LA|        Cloud Credentials     | Cloud authentication details for access to the Cloud API(s) must be set and linked to |Environments|.
                                                                                  | See :ref:`cloud_creds`.
Create Environments                        |LA|             Environments          | Each |ACCOUNT| requires one or more |ENVIRONMENTS| for users to login into. These must be linked to one or more sets of Cloud Credentials and access must be granted to the appropriate Teams.
                                                                                  | Environments can also be linked to Policy Groups and Resource Quotas if they are being used.
                                                                                  | See :ref:`environments`.
Register Images                            |LS| |LA| |LE|   Images                | Images must be registered in Scalr before they can be used in Roles. This can be simple manual registration or Images can be created from existing cloud servers.
                                                                                  | See :ref:`register_images` and :ref:`images_from_servers`.
Configure Roles                            |LS| |LA| |LE|   Roles                 | Roles associated with Images must be created and configured with any required Orchestration capabilities. This can be done from scratch or it can be done by importing existing cloud servers as new Images and Roles.
                                                                                  | See :ref:`roles` and :ref:`images_from_servers`.
=========================================  ================ ===================== ===========

The table below lists some of the optional tasks admins can perform before allowing end users access to Scalr. The tasks relate to implementing enterprise and business unit wide governance.

===========================================  ================ ===================== ===========
Task                                         Scopes           Menu Item             Description
===========================================  ================ ===================== ===========
Set up Governance Policies                   |LA|             Policy Engine         | Governance policies can be implemented at |ACCOUNT| level to control many aspects of cloud deployments, e.g. to ensure compliance, adhere to standard, control cost and much more.
                                                                                    | See :ref:`policy_engine`.
Create Scripts                               |LS| |LA| |LE|   Scripts               | Scripts can be created at all scopes within Scalr. They are used perform actions on running servers and can include things like ensuring mandatory software upgrades and patches are applied, or they can simply perform local actions relevant to individual Farm Roles.
                                                                                    | Scripts should be created by administrators if they are required for |SCALR| or |ACCOUNT| scope Orchestration rules, including orchestration rules applied to Roles at these scopes.
                                                                                    | See :ref:`scripts`.
Create Global Variables                      |LS| |LA| |LE|   Global Variables      | Global Variables should be created by administrators if they are required for |SCALR| or |ACCOUNT| scope Orchestration rules, including orchestration rules applied to Roles at these scopes. Global variables can be created at all scopes.
                                                                                    | See :ref:`gvs`.
Set up Orchestration Rules                   |LS| |LA|        Orchestration         | If you require orchestration rules to be applied consistently across all |Accounts| and |Environments| these should be created by administrators.
                                                                                    | See :ref:`sa_orchestration`.
Set up Endpoints and Webhooks                |LS| |LA| |LE|   Integration Hub       | Administrators must set up Enterprise or |ACCOUNT| wide external integrations via Webhooks and associate them with appropriate events. Examples of this are for integration with an IPAM system or a CMDB.
                                                                                    | See :ref:`webhooks`.
Set up Resource Quotas                       |LA|             Resource Quotas       | |ACCOUNT| admins can apply Resource Quotas (disk, memory etc) to all their |ENVIRONMENTS| to help control cost. This is often relevant in non-production |ENVIRONMENTS| where larger resource allocations are not required.
                                                                                    | See :ref:`quotas`
===========================================  ================ ===================== ===========
