.. include:: ../GLOBAL.rst

Security and Compliance Overview
================================

Scalr provides the capability to rigorously implement policies and rules that ensure security rules, compliance requirements and standards are fully and consistently implemented across all cloud infrastructure, regardless of which and how many cloud service(s) are being used. This "Governance" can be implemented through several different features Scalr and this section of our documentation describes the purpose of each governance related feature and how to implement the policies and rules.

Policy Engine
-------------

The Scalr Policy Engine is a powerful platform that can be used to create, manage and enforce Governance Policies, allowing your users to continue to take advantage of the speed and flexibility enabled by Cloud services, without increasing risk for your organization.  Scalr lets you enforce policies for an entire Environment, such as restricting instance types, restricting networks or mandating security requirements.  Each policy is defined by its type, which describes the goal of the policy, optional conditions that limit the scope this policy will apply to, and for some policy types that need it, additional configuration settings.

Scalr policy engine sits between the user and Scalr, as well as between Scalr and clouds.  When you provision a new Policy Group, all user interaction with Scalr will be validated by the Policy Engine.  Scalr also validates all actions from Scalr to clouds via the policy engine as well.  New Policies do not automatically apply to running farms. They will only be fully taken into account for Farms launched after the enforcement of the policy.  For previously Running Farms, Scalr will not terminate existing instances that violate newly enforced Policies, but will not allow for violation of the policy in the future.

For more details see :ref:`policy_engine`

Resource Quotas
---------------

Resource Quotas in Scalr provide a simple mechanism to limit consumption of resources in clouds and thereby control cost. Resource quotas can be set for Memory (RAM), number of servers and vCPU's on a cloud by cloud basis and applied selectively to different |Environments|. Thus a development team working in AWS could have different quotas to the Production system also running in AWS or anywhere else.

For more details see :ref:`quotas`

Orchestration Rules
-------------------

Orchestration Rules are a mechanism that enables scripts to be on servers under a variety of circumstances. The circumstances include built-in server life cycle events, custom events and scheduled tasks. Orchestration rules can be defined at many levels through out Scalr, including Farms and Farm Roles. But in the context of governance Scalr allows for event based Orchestration Rules to be defined at the |SCALR| scope (Enterprise) and |ACCOUNT| scope (Business Unit) so that the rules are applied to all |Environments| below these scopes.

Examples of using Orchestration Rules for governance are as follows.

* Ensuring mandatory security upgrades/patches are applied
* Ensuring Virus checkers are installed and activated
* Configuring external authentication at server level

For more details see :ref:`sa_orchestration`

Role Based Access Control
-------------------------

The Policy Engine and Resource Quotas control how you use the cloud. Role Based Access Control (RBAC) is all about controlling who does what with the cloud (and Scalr). Scalr provides fine grained control of Scalr and Cloud functionality through Access Control Lists (ACLs) and Teams. Teams are assigned and ACL which then applies to all members of the team. The ACLs will alter the appearance of the Scalr UI, causing buttons and fields to be hidden, filtering of lists limitation to read only access if required. Thus an Enterprise or Business Unit can define functional roles and implement these through the ACL's and Teams in Scalr. From a governance perspective this ensures only duly authorised staff are carrying out specific actions in the context of provisioning and managing cloud infrastructure.

For more details see :ref:`access_control`

Governance Through External Integrations
----------------------------------------

Enterprises often already have systems in place to implement governance policies. This can include things like

* IPAM systems
* CMDB systems for tracking infrastructure
* Approval systems

Scalr can be configured to directly authenticate against external LDAP and SAML bases systems and also includes the capability to define Webhooks and Endpoints for integration to 3rd party configuration management and approval systems, such as ServiceNow.

For more details see :ref:`webhooks`
