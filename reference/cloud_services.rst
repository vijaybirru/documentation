.. include:: ../GLOBAL.rst

.. _cloud_services_ref:

Supported Cloud Services and Features
=====================================

|SCOPE_ENV|

This reference page provides details of the Cloud specific services and features that are configurable through Scalr. The page provides details of how Scalr works with each service and feature, including how Scalr enhances the use of services to automatically integrate them with with Servers. This page DOES NOT provide details of functionality the service or feature itself but instead provides links to the relevant page in the Cloud providers own documentation.

AWS Features and Services
-------------------------

|MENU_ENV|

.. image:: images/aws_menu.png
   :scale: 40%

S3 Buckets
^^^^^^^^^^

.. |LINK_01| raw:: html

          <a href="https://aws.amazon.com/documentation/s3/" target="_blank">Amazon S3</a>

.. csv-table::
   :header-rows: 1
   :widths: 40,40,20

   Description,Scalr Support,External Docs
   "Amazon S3 is an object storage service","Full management of S3 buckets including enabling Transfer Acceleration and linking to CloudFront",|LINK_01| |NEWWIN|


CloudFront
^^^^^^^^^^

.. |LINK_02| raw:: html

          <a href="https://aws.amazon.com/documentation/cloudfront/" target="_blank">Amazon Cloud Front</a>

.. csv-table::
   :header-rows: 1
   :widths: 40,40,20

   Description,Scalr Support,External Docs
   "Amazon CloudFront is a global content delivery network (CDN) service that securely delivers data, videos, applications, and APIs with low latency and high transfer speeds.","Full configuration of CloudFront distributions and and linking to S3 Buckets or Load Balancers",|LINK_02| |NEWWIN|

Relational Database Service (RDS)
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. |LINK_03| raw:: html

          <a href="https://aws.amazon.com/documentation/rds/" target="_blank">Amazon RDS</a>

.. csv-table::
   :header-rows: 1
   :widths: 40,40,20

   Description,Scalr Support,External Docs
   "Amazon RDS provides a low administration database service that supports multiple database engines including, PostgreSQL, MySQL, MariaDB, Oracle, and Microsoft SQL Server","Configuration of RDS Instances, Clusters, Security & Parameter Groups and Snapshots. Also provides access to the RDS Events Log",|LINK_03| |NEWWIN|

EC2 - Load Balancers
^^^^^^^^^^^^^^^^^^^^

.. |LINK_04| raw:: html

          <a href="https://aws.amazon.com/documentation/elastic-load-balancing/" target="_blank">Amazon Load Balancers</a>

.. csv-table::
   :header-rows: 1
   :widths: 40,40,20

   Description,Scalr Support,External Docs
   "Amazon Elastic Load Balancing automatically distributes incoming application traffic across multiple targets, such as Amazon EC2 instances, containers, and IP addresses.","Configuration of Application, Network and Classic Load Balancers. |BR| Configuration of Target Groups for Listeners and ALB's. |BR| Scalr also provides the capability to link ELB's to Farm Roles so that instances are automatically registered and deregistered",|LINK_04| |NEWWIN|


EC2 - Elastic IP's
^^^^^^^^^^^^^^^^^^

.. |LINK_05| raw:: html

          <a href="https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/elastic-ip-addresses-eip.html" target="_blank">Elastic IP's</a>

.. csv-table::
   :header-rows: 1
   :widths: 40,40,20

   Description,Scalr Support,External Docs
   "Amazon Elastic IP's are fixed IP addresses that can be allocated to an instance.","Elastic IP's are assigned to Farm Roles. Scalr will ensure that the IP is reassigned to a replacement server in the Farm Role if a server is terminated or fails. Thus Scalr ensures that a given Elastic IP will always point to a Server of the same Farm Role.",|LINK_05| |NEWWIN|


EC2 - Security Groups
^^^^^^^^^^^^^^^^^^^^^

.. |LINK_06| raw:: html

          <a href="https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/using-network-security.html" target="_blank">Security Groups</a>

.. csv-table::
   :header-rows: 1
   :widths: 40,40,20

   Description,Scalr Support,External Docs
   "Security Groups act as a virtual firewalls that control the traffic for one or more instances.","Full configuration of security groups and rules either through Farm Roles or through the main menu.",|LINK_06| |NEWWIN|

.. warning:: Security Group changes are applied immediately to the Servers they are linked to when the changes are saved in Scalr. This could have an immediate impact on the flow of network traffic and could disrupt production services if mistakes are made.

EC2 - EBS Volumes
^^^^^^^^^^^^^^^^^

.. |LINK_07| raw:: html

          <a href="https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/EBSVolumes.html" target="_blank">EBS Volumes</a>

.. csv-table::
   :header-rows: 1
   :widths: 40,40,20

   Description,Scalr Support,External Docs
   "Amazon's Elastic Block Store (EBS) can be used as block level storage volumes for your Amazon EC2 instances. An EBS Volume functions as a network-attached form of block level storage that persists independently from a Server's life.","Management of EBS Volumes independently of Servers. |BR| Attach and detach volumes on running servers. |BR| Access to CloudWatch stats.",|LINK_07| |NEWWIN|

EC2 - EBS Snapshots
^^^^^^^^^^^^^^^^^^^

.. |LINK_08| raw:: html

          <a href="https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/EBSSnapshots.html" target="_blank">EBS Snapshots</a>

.. csv-table::
   :header-rows: 1
   :widths: 40,40,20

   Description,Scalr Support,External Docs
   "EBS Snapshots are incremental backups of EBS Volumes stored on S3. Each snapshot contains only the changes since the volume was created or the last snapshot.","Manual creation of Snapshots. |BR| Create new Volumes from Snapshots. |BR| Configure Auto-Snapshot. |BR| Copy Snapshots to other regions.",|LINK_08| |NEWWIN|

Elastic Map Reduce (EMR)
^^^^^^^^^^^^^^^^^^^^^^^^

.. |LINK_09| raw:: html

          <a href="https://docs.aws.amazon.com/emr/latest/ManagementGuide/emr-overview.html" target="_blank">Amazon EMR</a>

.. csv-table::
   :header-rows: 1
   :widths: 40,40,20

   Description,Scalr Support,External Docs
   "Amazon Elastic MapReduce (EMR) is an AWS tool for big data processing and analysis. EMR offers the expandable low-configuration service as an easier alternative to running in-house cluster computing.","Creation and management of EMR clusters. |BR| Linking to Farms.",|LINK_09| |NEWWIN|

Elastic File System (EFS)
^^^^^^^^^^^^^^^^^^^^^^^^^

.. |LINK_10| raw:: html

             <a href="https://docs.aws.amazon.com/efs/latest/ug/whatisefs.html" target="_blank">Amazon EFS</a>

.. csv-table::
   :header-rows: 1
   :widths: 40,40,20

   Description,Scalr Support,External Docs
   "Amazon Elastic File System (Amazon EFS) provides simple, scalable file storage for use with Amazon EC2. With Amazon EFS, storage capacity is elastic, growing and shrinking automatically as you add and remove files, so your applications have the storage they need, when they need it.","Creation and management of EFS. |BR| Linking to Farms and mounting on instances.",|LINK_10| |NEWWIN|

Route53
^^^^^^^

.. |LINK_11| raw:: html

             <a href="https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/Welcome.html" target="_blank">Amazon Route 53</a>

.. csv-table::
   :header-rows: 1
   :widths: 40,40,20

   Description,Scalr Support,External Docs
   "Amazon Route 53 is a scalable and highly available Domain Name System providing domain name registration, DNS routing and automated DNS health checks","Creation and management of Route 53 zones. |BR| Creation and management of Health Checks. |BR| Automation of hostname registration with Route 53 through Webhooks.",|LINK_11| |NEWWIN|

IAM - SSL Certificates
^^^^^^^^^^^^^^^^^^^^^^

.. |LINK_12| raw:: html

             <a href="https://docs.aws.amazon.com/acm/latest/userguide/acm-overview.html" target="_blank">IAM SSL Certificates</a>

.. csv-table::
   :header-rows: 1
   :widths: 40,40,20

   Description,Scalr Support,External Docs
   "Amazon ACM handles the complexity of creating and managing public SSL/TLS certificates for your AWS based websites and applications.","Upload of SSL Certificates to ACM",|LINK_12| |NEWWIN|

VPC's and Subnets
^^^^^^^^^^^^^^^^^

.. |LINK_13| raw:: html

             <a href="https://docs.aws.amazon.com/vpc/latest/userguide/what-is-amazon-vpc.html" target="_blank">Amazon VPC's</a>

.. csv-table::
   :header-rows: 1
   :widths: 40,40,20

   Description,Scalr Support,External Docs
   "Amazon Virtual Private Clouds (VPC) provides isolated private networking functionality for applications.","Full Management of VPC's and Subnets",|LINK_13| |NEWWIN|

Azure Features and Services
---------------------------

|MENU_ENV|

.. image:: images/azure_menu.png
   :scale: 40%

Public IP's
^^^^^^^^^^^

.. |LINK_14| raw:: html

             <a href="https://docs.microsoft.com/en-us/azure/virtual-network/virtual-networks-instance-level-public-ip" target="_blank">Azure Public IP's</a>

.. csv-table::
   :header-rows: 1
   :widths: 40,40,20

   Description,Scalr Support,External Docs
   "Public Ip's for Instances","Interface to view and delete Public IP's that are assigned to Scalr managed Instances.",|LINK_14| |NEWWIN|


Resource Groups
^^^^^^^^^^^^^^^

.. |LINK_15| raw:: html

             <a href="https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-overview" target="_blank">Azure Resource Groups</a>

.. csv-table::
   :header-rows: 1
   :widths: 40,40,20

   Description,Scalr Support,External Docs
   "A container that holds related resources for an Azure solution. The resource group can include all the resources for the solution, or only those resources that are to be managed as a group.","Interface for directly managing Resource Groups. |BR| Linking resource Groups to Farm Roles and therefore the Servers launched from a Farm Role.",|LINK_15| |NEWWIN|

Virtual Networks
^^^^^^^^^^^^^^^^

.. |LINK_16| raw:: html

             <a href="https://docs.microsoft.com/en-us/azure/virtual-network/virtual-networks-overview" target="_blank">Azure Virtual Networks</a>

.. csv-table::
   :header-rows: 1
   :widths: 40,40,20

   Description,Scalr Support,External Docs
   "Azure Virtual Network enables many types of Azure resources, such as Azure Virtual Machines (VM), to securely communicate with each other, the internet, and on-premises networks.","Interface for directly managing Virtual Networks and Subnets. |BR| Linking Virtual Networks and Subnets to Farm Roles and therefore the Servers launched from a Farm Role.",|LINK_16| |NEWWIN|

Security Groups
^^^^^^^^^^^^^^^

.. |LINK_17| raw:: html

             <a href="https://docs.microsoft.com/en-us/azure/virtual-network/security-overview" target="_blank">Azure Security Groups</a>

.. csv-table::
   :header-rows: 1
   :widths: 40,40,20

   Description,Scalr Support,External Docs
   "Security Groups act as a virtual firewalls that control the traffic for one or more instances.","Full configuration of security groups and rules either through Farm Roles or through the main menu.",|LINK_17| |NEWWIN|


Managed Disks
^^^^^^^^^^^^^

.. |LINK_18| raw:: html

             <a href="https://docs.microsoft.com/en-us/azure/virtual-machines/windows/managed-disks-overview" target="_blank">Azure Managed Disks</a>

.. csv-table::
   :header-rows: 1
   :widths: 40,40,20

   Description,Scalr Support,External Docs
   "Azure Managed Disks simplifies disk management for Azure IaaS VMs by managing the storage accounts associated with the VM disks. You only have to specify the type (Standard HDD, Standard SSD, or Premium SSD) and the size of disk you need, and Azure creates and manages the disk for you.","Full configuration of Managed Disks. |BR| Allocation of managed disks to Farm Roles as additional Storage.",|LINK_18| |NEWWIN|

Google Cloud Platform Features and Services
-------------------------------------------

|MENU_ENV|

.. image:: images/gce_menu.png
   :scale: 40%

Persistent Disks
^^^^^^^^^^^^^^^^

.. |LINK_24| raw:: html

             <a href="https://cloud.google.com/compute/docs/disks/" target="_blank">GCE Persistent Disks</a>

.. csv-table::
   :header-rows: 1
   :widths: 40,40,20

   Description,Scalr Support,External Docs
   "Persistent Storage for instances. ","From main menu view and resize. Can be created and flagged for mounting in Farm Roles",|LINK_24| |NEWWIN|

Snapshots
^^^^^^^^^

.. |LINK_25| raw:: html

             <a href="https://cloud.google.com/compute/docs/disks/create-snapshots" target="_blank">GCE Snapshots</a>

.. csv-table::
   :header-rows: 1
   :widths: 40,40,20

   Description,Scalr Support,External Docs
   "Snapshots are incremental compressed backups of Persistent Disks. Each snapshot contains only the changes since the disk was created or the last snapshot","View only.",|LINK_25| |NEWWIN|

External IP's
^^^^^^^^^^^^^

.. |LINK_26| raw:: html

             <a href="https://cloud.google.com/compute/docs/ip-addresses/reserve-static-external-ip-address" target="_blank">GCE External IP's</a>

.. csv-table::
   :header-rows: 1
   :widths: 40,40,20

   Description,Scalr Support,External Docs
   "A static external IP address is an external IP address that is reserved for your project until you decide to release it. ","View and delete only.",|LINK_26| |NEWWIN|

Cloud SQL
^^^^^^^^^

.. |LINK_27| raw:: html

             <a href="https://cloud.google.com/sql/docs/" target="_blank">GCE Cloud SQL</a>

.. csv-table::
   :header-rows: 1
   :widths: 40,40,20

   Description,Scalr Support,External Docs
   "Cloud SQL is a fully-managed database service that makes it easy to set up, maintain, manage, and administer your relational databases on Google Cloud Platform.","Full management of Cloud SQL Instances including linking to Farms for automatic deployment when a Farm is launched.",|LINK_26| |NEWWIN|


Openstack Features and Services
-------------------------------

|MENU_ENV|

.. image:: images/openstack_menu.png
   :scale: 40%

Volumes
^^^^^^^

.. |LINK_19| raw:: html

             <a href="https://docs.openstack.org/cinder/rocky/admin/blockstorage-manage-volumes.html" target="_blank">Openstack Volumes</a>

.. csv-table::
   :header-rows: 1
   :widths: 40,40,20

   Description,Scalr Support,External Docs
   "OpenStack Volumes are block storage devices that may be attached to instances in order to enable persistent storage.","Management of Volumes independently of Servers. |BR| Attach and detach volumes on running servers.",|LINK_19| |NEWWIN|

Snapshots
^^^^^^^^^

.. |LINK_20| raw:: html

          <a href="https://docs.openstack.org/cinder/rocky/admin/blockstorage-backup-disks.html" target="_blank">Openstack Snapshots</a>

.. csv-table::
   :header-rows: 1
   :widths: 40,40,20

   Description,Scalr Support,External Docs
   "Snapshots are full backups of Volumes.","Manual creation of Snapshots. |BR| Create new Volumes from Snapshots. |BR| Configure Auto-Snapshot.",|LINK_20| |NEWWIN|


Security Groups
^^^^^^^^^^^^^^^

.. |LINK_21| raw:: html

          <a href="https://docs.openstack.org/nova/queens/admin/security-groups.html" target="_blank">Openstack Security Groups</a>

.. csv-table::
   :header-rows: 1
   :widths: 40,40,20

   Description,Scalr Support,External Docs
   "Security groups are sets of IP filter rules that are applied to all project instances, which define networking access to the instance. ","Creation and management of Security Groups and assignment to Farm Roles",|LINK_21| |NEWWIN|


Server Groups
^^^^^^^^^^^^^

.. |LINK_22| raw:: html

          <a href="https://docs.openstack.org/python-openstackclient/latest/cli/man/openstack.html" target="_blank">Openstack Server Groups</a>

.. csv-table::
   :header-rows: 1
   :widths: 40,40,20

   Description,Scalr Support,External Docs
   "Server groups provide a mechanism to group servers on to hosts according to defined policies.","Creation and management of Server Groups and assignment to Farm Roles",|LINK_22| |NEWWIN|

VMware VSphere Features
-----------------------

|MENU_ENV|

.. image:: images/vmware_menu.png
   :scale: 40%

.. |LINK_23| raw:: html

          <a href="https://docs.vmware.com/" target="_blank">VMWare Documentation</a>

For VMWare Scalr provides access to view resources and some management capabilities as shown in the table below. Full documentation on VMware features can be found at |LINK_23| |NEWWIN|.

.. csv-table::
   :header-rows: 1
   :widths: 20,20

   Description,Scalr Support
   Networks,View only
   Resource Pools,View only
   Data Stores,View only
   Compute Resources,View only (Consumption)
   Folders,"View, Create, Delete"
   Storage Pods,View only
   Virtual Disks,View and Create
   Snapshots,View only
   Alarms,View only
