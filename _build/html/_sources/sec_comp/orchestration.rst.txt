.. include:: ../GLOBAL.rst

.. _sa_orchestration:

|SCALR|/|ACCOUNT|/|ENVIRONMENT| Level Orchestration
====================================================

|SCOPE_SCALR| |SCOPE_ACC| |SCOPE_ENV|

Orchestration Rules can be defined to run :ref:'scripts' across all appicable servers within the scope at which the rule is defined.

* At |SCALR| scope script will be run on all applicable servers in all |ENVIRONMENTS| managed by this Scalr installation
* At |ACCOUNT| scope script will be run on all applicable servers in all |ENVIRONMENTS| with the |ACCOUNT|
* At |ENVIRONMENT| scope script will be run on all applicable servers within the |ENVIRONMENT|

This type of Orchestration is typically used to enforce policies, for example:

* Security toolsets that must be applied to all servers.
* Lifecycle events that must be applied to all servers, i.e. join a domain.

If an Orchestration rule is created at one of these scopes, it cannot be removed at the lower scope and ALL servers at the lower scope will have the rule applied to it.

Creating Orchestration Rules
----------------------------

.. |SCALR_ICON| image:: images/scalr_icon_env.png
   :scale: 70%

To create an orchestration rule at the |SCALR|, |ACCOUNT|, or |ENVIRONMENT| scopes, click on the Scalr icon on the top left |SCALR_ICON| and then click on Orchestration.

.. include:: /farms/orchestration_include.rst
