.. include:: ../GLOBAL.rst

.. _multicloud_roles:

Multi-cloud Roles
=================

This pages is an overview of multi-cloud roles. More details on using multi-cloud roles can be found in :ref:`farms` and :ref:`service_catalog`.

Roles can be associated with Images from different clouds in order to provide flexibility in choosing where to provision servers from :ref:`farm_roles`. This example shows a Role associated with Images from multiple clouds.

.. image:: images/multi-cloud-01.png
   :scale: 50%

All Images associated with a Role should be fundamentally the same. They MUST be the same base operating system and version and should also have the same pre-installed patches and software packages. Variations specific to each cloud are allowed for cloud specific items such as pre-installing VMware Tools on VMware images.

Choosing which cloud to use initially occurs when configuring a Farm Role and cannot be changed in the Farm Role once set.

.. image:: images/multi-cloud-02.png
   :scale: 50%

The choice of Cloud (and location and other cloud parameters) can be restricted by :ref:`Policy <policy_engine>` |POLICY|.

When a Farm is used to create a :ref:`Service Catalog Offering <service_catalog>` the template will contain the settings of the Cloud(s) that were chosen at the time the Farm Role(s) was created. The Farm Template can be edited to remove these Cloud settings so that an End User launching applications via the Service Catalog will be given the choice of Cloud at the point at which they make the request, subject to policy restrictions. Note these parameters are not just the cloud name and location, but may also include cloud specific details such as instance type, network settings and so on. Below is a simple example.

**Farm Template after Creating Offering**

.. code-block:: json
   :emphasize-lines: 8,9,12

       },
    "roles": [
        {
            "alias": "base-ubuntu1604",
            "role": {
                "name": "base-ubuntu1604"
            },
            "cloudPlatform": "ec2",
            "cloudLocation": "eu-west-2",
            "availabilityZones": [],
            "instanceType": {
                "id": "t2.nano"
            },

**Farm Template with Cloud Parameters Removed**

.. code-block:: json
   :emphasize-lines: 8,9,12

       },
    "roles": [
        {
            "alias": "base-ubuntu1604",
            "role": {
                "name": "base-ubuntu1604"
            },
            "cloudPlatform": "",
            "cloudLocation": "",
            "availabilityZones": [],
            "instanceType": {
                "id": ""
            },

A change like this results in the Service Catalog user being prompted for Cloud Specific details. In this example AWS has been chosen and so a number of AWS specific parameters are also required. The parameters are only shown if there are choices to be made. If :ref:`Policies <policy_engine>` are in place to enforce the use of one specific setting the end user will not be prompted to choose.

.. image:: images/multi-cloud-05.png
   :scale: 50%

Please see the main :ref:`service_catalog` page for full details on configuring Farm Templates for use with Multi-Cloud Roles.
