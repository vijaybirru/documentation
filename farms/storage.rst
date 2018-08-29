.. include:: ../GLOBAL.rst

.. _storage:

Configuring Storage
===================

|SCOPE_ENV|

Storage is configured at the Farm Role and includes options for configuring the mandatory root storage volume and optional additional storage. The additional storage can be shared on some clouds and marked as reusable. Reusable storage is automatically preserved by a snapshot and added to new servers when they are launched. In AWS this includes copying snapshots to other Availability Zones when a Farm Role is re-launched in a different AZ.

.. note:: Storage configuration changes do not apply to running Servers. They only take effect when new servers are launched.

Below is an example of a Storage configuration for a root volume. The actual options available are specific to the Cloud allocated to the Farm Role but are typically limited to the volume size and type.

.. image:: images/storage_root.png
           :scale: 50%

For additional storage there are many more options available which are again specific to the Cloud allocated to the Farm Role. This example for AWS shows the full set of options when auto-mount is enabled.

.. image:: images/storage_add.png
           :scale: 50%

The common parameters for additional storage are as follows.

.. csv-table::
   :header-rows: 1
   :widths: 25,100
   :file: csv/storage_add_gen.csv

AWS Storage Configuration
-------------------------

Additional AWS EBS Volumes can be configured on a Farm Role to be added to every server. The additional EBS options are as follows.

.. |EBS| raw:: html

   <a href="https://aws.amazon.com/ebs/details/" target="_blank">Amazon EBS Product Details</a>

.. csv-table::
   :header-rows: 1
   :widths: 25,100

   Option,Description
   EBS Type,The full range of EBS types can be selected. See |EBS| |NEWWIN| for more details
   Snapshot,The Snapshot to create the volume from. If blank a new Volume is created
   Enable EBS encryption,Turn on encryption and specify the KMS key

.. image:: images/storage_aws.png
   :scale: 50%

Google Cloud Platform Storage Configuration
-------------------------------------------

GCP based Farm Roles can have additional storage added using either "Persistent Disk" or "Local SSD (ephemeral)".

**Persistent Disk** : Options are Standard or SSD disk |BR|
**Local SSD** : Only option is the name.

.. |GCP1| image:: images/storage_gcp_1.png
          :scale: 50%

.. |GCP2| image:: images/storage_gcp_2.png
          :scale: 50%

|GCP1| |GCP2|

Azure Storage Configuration
---------------------------

Azure based Farm Roles can have additional managed data disks added. The only option is the size.

.. image:: images/storage_azure.png
   :scale: 50%


OpenStack Storage Configuration
-------------------------------

OpenStack based Farm Roles can have additional persistent disks added. The only option is the size.

.. image:: images/storage_openstack.png
   :scale: 50%

VMWare Storage Configuration
----------------------------

VMware based Farm Roles can have additional virtual disks added. The Volume Settings available are as follows.

.. csv-table::
   :header-rows: 1
   :widths: 25,100

   Option,Description
   Provisioning,Defines how to initialise the volume using zeroing
   Shared Disk,Allows the disk to be shared across all servers in the Farm Role. Only available for "Eager Zeroed" provisioning

.. image:: images/storage_vmware.png
   :scale: 50%
