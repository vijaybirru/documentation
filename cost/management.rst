.. include:: ../GLOBAL.rst

.. _cost_management:

Cost Management
===============

Overview
^^^^^^^^
Scalr Cost Manager is Scalr’s next general cost management product module. Scalr Cost Manager is being built to provide enhanced capabilities to help customers with cost tracking, budgeting, show-back/charge-back and cost optimization.

Scalr Cost Manager reflects all costs associated within a cloud account, including services provisioned by Scalr, as well as services provisioned outside of Scalr.


Feature Preview
^^^^^^^^^^^^^^^
Scalr Cost Manager is currently in Feature Preview and requires a new license file to enable.  Please feel free to contact Scalr Support for additional questions regarding the license file.

Upon receipt of the new license file, replace the existing file (/etc/scalr-server/license.json) on the Scalr Server (either singularly on a single node install, or on every node in the Scalr deployment in a multi-node installation)  and then run `scalr-server-ctl reconfigure` on each node.

No additional configuration should be required.


Currently Supported Cloud Service Providers
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
Cost Manager currently supports the following Cloud Service Providers:

	* Amazon Web Services - standard and Detailed Billing
	* Microsoft Azure - Azure standard billing and Azure Enterprise Agreements Billing
	* Google Cloud Platform - Google Cloud Billing
	* VMWare - Custom Price Lists


Cost Manager Dashboard
^^^^^^^^^^^^^^^^^^^^^^
The new Cost Manager Dashboard is currently accessible through the |SCALR| scope only.

The data populated within the dashboard is summarized from all cloud account numbers entered as Cloud Credentials in either |ACCOUNT| Scope or |SCALR| Scope.

**Enabling Tags**
In order to view cost data by desired Tags, the Tags need to be enabled. You can enable Tags for each cloud account, in Cloud Credentials.
