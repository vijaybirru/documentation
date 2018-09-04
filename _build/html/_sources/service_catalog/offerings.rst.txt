.. include:: ../GLOBAL.rst

.. _sc_offerings:

The Service Catalog
===================

.. sc_start_label:

|SCOPE_SCALR| |SCOPE_ACC| |SCOPE_ENV|

Scalr's Service Catalog provides users with simple self service capability to launch entire application infrastructures at the click of a button. Entries in the Service Catalog are called "Offerings" and are created by exporting the configuration of a Farm (the "Farm Template"), including all of it's Farm Roles and linked Cloud Services. Users can request to create an Application from the Service Catalogue Offering and then manage (launch, terminate, delete) that application to suit their requirements.

Applications launched from the Service Catalog are subject to the :ref:`Governance Policies <policy_engine>` of the |ACCOUNT| they run under, in the same way as Farms are.

The Farm Template is a Service Catalog offerings is typically customised to give users some choices over the deployment of their applications (subject to any Policy constraints). This can include choosing instance types, networks, storage options and even choosing which Cloud to deploy in.

This page covers all aspects of creating, customising and managing Service Catalog offerings. End users who simply want to use the Service Catalog to deploy applications should refer to :ref:`sc_using`.

.. note: Service Catalog Offerings can be created at any scope, but can only be created directly from a Farm at the |ENVIRONMENT| scope.

The Service Catalog itself is accessed from the Main Menu.

.. image:: /service_catalog/images/sc_menu.png
   :scale: 40%

.. |SC1| image:: /service_catalog/images/sc_menu_1.png
         :scale: 30%

Clicking on |SC1| itself opens the list of available offerings to allow users to request applications. "My Applications" opens the screen of already created applications. "Management" gives access to the interface for editing and customising offerings and Farm Templates, and "Categories" provides the capability to manage categories for groups Service Catalog entries.

Creating Service Catalog Offerings
==================================

|SCOPE_ENV|

Typically Service Catalog Offerings are created directly from fully configured and tested Farms.

.. note:: Service Catalog Offerings can be created from the Service Catalogue --> Management screen by copying the Farm Template from another offering and pasting into the template editor. This option is available at all 3 Scopes |SCOPE_SCALR| |SCOPE_ACC| |SCOPE_ENV|.

To create an offering navigate to the Farms list and select Create Offering from the Farm |MENU| button.

.. image:: images/offer_menu.png
   :scale: 50%

Enter a name for the Service Catalog Offering and click "CREATE".

The resulting screen allows you to add descriptions for the Offering and for any Applications created from it. Optionally the offering can have a custom pricing applied to it. Ownership can be set and the Offering can be allocated specific teams.
The Farm Template is also presented for editing which is covered in `Customising Farm Templates`_.

.. image:: images/edit_offering.png
   :scale: 50%

Customising Farm Templates
==========================

A Farm Template is a JSON representation of a Farm. This includes all Farm Roles and other configuration items from the originating Farm.  Farm Templates are very flexible and provide a form of  "Infrastructure as code" to be used via the Scalr API/Scalr-CTL tool, as well as providing the configuration of Service Catalog offerings for Self Service application deployment.

Farm Templates used in the Service Catalog offerings are usually customised to provide end users with some choices over various aspects of the deployment. This section will provide some more common examples of customisation. For more advanced customisation, including use of the ``_meta`` configuration block to control options, allowed values and visibility see :ref:`adv_farm_templates`.

In simple terms the ``_meta`` section defines the rules for the parameters and their values that can be used in the rest of the template.
The other sections of the template define the components of the Application, their static values such as the role to be used, and the configurable values such as cloud location, networks etc. Where values are provided they are generally the default values or the only value allowed. This varies from field to field (See "Farm Template Parameter Reference"). The values available to chose from when requesting an application are only constrained if there are policies in place and/or if ``_meta`` has a corresponding entry.

Simple Template Example
-----------------------

This is an example of as Farm Template that contains a single Farm Role, a Global Variable, Orchestration Rules and Storage configuration.
This template is constrained to AWS via the Role parameter ``"cloudPlatform": "ec2"`` but it does allow selection of the Cloud Location as there are no restrictions in ``_meta`` and ``"cloudLocation": "us-east-1"`` only sets the default value.

Templates will cause the end user to be prompted for certain mandatory inputs under a variety of circumstances.

* There are no constraints in ``_meta`` or  more than one value option is provided.
* The parameter is empty or set to ``null``
* The parameter is entirely missing from the template.

As well as prompting for Cloud Location this template will also prompt the user for the following.

* Instance Type - Not constrained by ``_meta``
* Networking information - The ``"networking": { }"`` section is empty
* Minimum number of Instances - Null value ``"minInstances": null``

.. note:: For ease of understanding it is better to include all parameters in the template and set them to blank or null if the user is to be prompted to select a value. In the case of parameters like ``minInstances`` if a value is supplied in the template it will not automatically be visible to the user.

.. literalinclude:: ft_simple.json
   :language: json

This template will result in the user being prompted for values as shown below.

.. image:: images/simple_deploy.png
   :scale: 50%

Enabling Options for End Users
------------------------------

The previous example showed some common cases for configuring a Farm to present the end user with options. This may need to taken a step further if a Service Catalog offering is to be published at |ACCOUNT| or |SCALR| scope or being offered to a wider global audience. The Project ID in the template may not be valid in other accounts and user may wish to use their own timezone. We can also remove the pre-set value for the global variable so the user is prompted to enter that as well. In this revised example the following changes were made.

* Project ID - ``"project": []``
* Timezone - ``"timezone": null`` - Causes users default TZ to be used instead
* Variables - ``"value": null``

.. literalinclude:: ft_simple_2.json
   :language: json

This template will result in the user being prompted for values as shown below.

.. image:: images/simple_2_general.png
   :scale: 50%

.. image:: images/simple_2_deploy.png
   :scale: 50%


Customising for Multi-Cloud
---------------------------

Farm Templates provide the capability to use a single Service Catalog offering across multiple clouds. When a template if created from a Farm it includes the specific configuration items for the Cloud that the Farm Roles are linked to. In this form the Service Catalog Offering can also only use the Cloud that is baked into the template.

To enable a Service Catalogue Offering to be used in multiple clouds the Farm Template can be edited in two ways.

1. Remove the configured cloudPlatform and all cloud specific configuration items. This will effectively give the end user complete choice over the cloud, location, instance types and network configuration, subject to any governance policies that may be in place in the |ACCOUNT|.
2. Use ``_meta`` to set default values or a list choices for each Cloud. This option is covered in more detail in :ref:`adv_farm_templates`.

.. note:: The Cloud(s) used in a Farm Template are configured for each (Farm) role, just as they are in the originating Farm. Thus to make a Farm Template work for multiple clouds the cloud specific elements must be removed for all Roles.

To remove the specific cloud configuration in a Role the following must be changed.

**Before**

.. code-block:: json

   "cloudPlatform": "ec2",
   "cloudLocation": "us-east-1",
   "availabilityZones": [],
   "instanceType": {
                "id": "m3.medium"

**After**

.. code-block:: json

   "cloudPlatform": "",
   "cloudLocation": "",
   "availabilityZones": [],
   "instanceType": {
                "id": ""

In addition it us necessary to remove all the details from ``networking: []`` and ``storage: []``.

.. code-block:: json
   :emphasize-lines: 19-23,56,64

   {
    "_meta": {
        "schema_version": "v1beta0-7.11.0"
    },
    "farm": {
        "name": "Single Application Server",
        "description": "",
        "project": [],
        "timezone": null,
        "launchOrder": "simultaneous",
        "variables": []
    },
    "roles": [
        {
            "alias": "base-ubuntu1404",
            "role": {
                "name": "base-ubuntu1404"
            },
            "cloudPlatform": "",
            "cloudLocation": "",
            "availabilityZones": [],
            "instanceType": {
                "id": ""
            },
            "launchIndex": 0,
            "advancedConfiguration": {
                "disableAgentIptablesManagement": false,
                "disableAgentNtpManagement": false,
                "rebootAfterHostInit": false
            },
            "scaling": {
                "considerSuspendedServers": "running",
                "enabled": true,
                "minInstances": null,
                "maxInstances": 1,
                "rules": [],
                "scalingBehavior": "launch-terminate"
            },
            "cloudFeatures": {
                "type": "AwsCloudFeatures",
                "ebsOptimized": false
            },
            "security": {
                "securityGroups": [
                    {
                        "id": "sg-2cb57444"
                    },
                    {
                        "id": "sg-6a769f7c"
                    },
                    {
                        "id": "sg-1a1cea0c"
                    }
                ]
            },
            "networking": [],
            "variables": [
                {
                    "name": "RequiredVariable",
                    "value": null
                }
            ],
            "orchestration": [],
            "storage": []
        }
    ]
    }

This Farm Template will now cause different prompts to appear for the user depending on the Cloud they select.

.. |M1| image:: images/multi_cloud_1.png
        :scale: 40%

.. |MAWS| image:: images/multi_cloud_aws.png
        :scale: 40%

.. |MGCE| image:: images/multi_cloud_gce.png
        :scale: 40%

|M1| |MAWS| |MGCE|

Publishing and Promoting Service Catalog Offerings
==================================================

.. |PUB| image:: images/publish.png
         :scale: 30%

Once the necessary details have been entered, and any customisations have been completed the Offering can be published by clicking YES |PUB| and saving the offering. Service Catalog offerings can optionally be grouped into Categories to help users with selection. Categories can be created by following the main menu "Service Catalog" --> "Categories". You can custom pricing for the service catalog offering.

.. |PROMOTE| image:: images/promote.png
         :scale: 40%

Service Catalog offerings can also be promoted to higher scopes to make them more widely available by clicking on the Promote |PROMOTE| button. When an offering is promoted to |ACCOUNT| scope it will become available to all |ENVIRONMENTS| in that |ACCOUNT|, and when prompted to |SCALR| scope it becomes available to ALL |ENVIRONMENTS|. It is therefore essential that the Farm Template is configured to work in all |ENVIRONMENTS| and that the |ENVIRONMENTS| themselves have the necessary Roles, Scripts, Cloud Crednetials etc in place to support the Service Catalog offering. If any discrepancies exist between the Farm Template and the |ENVIRONMENT| at the time a user requests an Application they will see errors and thew application will fail to create.
