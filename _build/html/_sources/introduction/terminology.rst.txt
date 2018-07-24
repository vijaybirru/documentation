.. include:: ../GLOBAL.rst


Concepts and Terminology
========================

Scalr Architecture
------------------

Scalr Scopes
------------

The Scalr application is organised into 3 levels of access that are known as "Scopes". These scopes provide a hierarchy of access, functionality and object inheritance that enables a customer to match Scalr to their organisational structure, and to manage, control and monitor their deployments of cloud based infrastructure. The 3 scopes are as follows.

.. |SS| image:: images/scalr.png
   :scale: 70%

.. |AS| image:: images/account.png
   :scale: 70%

.. |ES| image:: images/environment.png
   :scale: 70%

=============== ============================= ======================================================================================
Scope           Usage                         Description
=============== ============================= ======================================================================================
|SCALR|         Scalr Administration          - There is a single admin level in Scalr where global configuration elements and |ACCOUNTS| are managed.
                                              - Scalr Administrators can configure cloud access credentials, roles, images and much more for common usage by all |ACCOUNTS| and |ENVIRONMENTS|.
                                              - Users are also managed at the |SCALR| scope.
                                              - Cost Analytics and Cost Management are configure and analysed through the definition of Cost Centers, Projects, Budgets and Pricing.

                                              |SS|
|ACCOUNT|       Organisation Units            - Typically |ACCOUNTS| are Business Units that bring together teams working to a common purpose.
                                              - There will be multiple |ACCOUNTS| which can define common governance policies for all their environments as well as also configuring additional cloud access credentials, roles, images etc over and above those defined at the |SCALR| scope.
                                              - |Accounts| are also responsible for configuring Teams and Access Control Lists (ACLs) to control who can do what and which resources they can use.
                                              - Cost Analytics can (with permission) be further configure and analysed through the definition of additional Projects, Budgets and Pricing.

                                              |AS|
|ENVIRONMENT|   Deployment Environments       - |Environments| bring together the resources required to deploy infrastructure to the cloud.
                                              - It is at the |ENVIRONMENT| scope that deployment infrastructures, known as "Farms" are defined. Farms bring together roles, cloud services and orchestration rules to enable simple deployment of an entire application infrastructure with a single click. Orchestration rules are used to install packages, deploy custom software and much more.
                                              - There will typically be multiple |ENVIRONMENTS| per |ACCOUNT| that can also configure additional roles, images etc over and above those defined at the higher scopes.
                                              - Farms can also be published as Service Catalog offerings to allow non-technical end users to select and deploy applications in real time without the need to raise requests to the central IT department.

                                              |ES|
=============== ============================= ======================================================================================

The following diagram shows the high level hierarchical relationships between the 3 scopes.

.. image:: images/Scalr-Scopes.png
   :scale: 50%


Cloud Credentials
-----------------

|SCOPE_SCALR| |SCOPE_ACC|

To be able to manage your cloud infrastructure Scalr needs to be able to connect to the APIs of the clouds that you use. Each cloud is different in the way it authenticates API access. Some require the generation of Access Keys and configuration of permissions and policies inside the cloud, whilst others simply authenticate with username and password. Whatever the method these authentication details must be stored in Scalr as Cloud Credentials.

Cloud credentials can be configured at both the |SCALR| and |ACCOUNT| scopes and are then available to all lower scopes. Once they are configured Cloud Credentials are then linked to |Environments| so that end users can configure and manage cloud infrastructure.

See :ref:`cloud_creds` for details on configuring cloud access and Cloud Credentials.

|Accounts|
----------

|AS|

|Accounts| are the core of implementing a federated IT organisational structure in Scalr. An |ACCOUNT| brings together the configuration resources, access permissions (ACLs) and governance policies that are applicable to to an organisational unit within an enterprise, thus ensuring consistent and suitably managed use of cloud environments. |Accounts| typically map to Business Units within an enterprise and are further sub-divided into |ENVIRONMENTS| for the different teams and/or functional areas within the BU, such as Dev, QA, Sales etc.

There can be multiple |Accounts| within Scalr and these will be created by the Scalr administrator.

An |ACCOUNT| administrator will be responsible for managing and configuring the following aspects of Scalr.

* Cloud credentials
* |Environments|
* Governance Policies and Resource Quotas
* Users, Teams and Access Control Lists
* Account level Orchestration rules
* Cost Management


|Environments|
--------------

|ES|

|Environments| are the scope at which cloud infrastructure is configured and run. An |ACCOUNT| can have multiple |Environments| that correspond to functional areas, different cloud providers or whatever structure makes sense for your business. Typically |Environments| are set up in line with application life cycles for specific applications and also possibly by geographical region. Each environment is linked to one or more sets of cloud credentials and one or more end user teams will be granted access at various levels to the |ENVIRONMENT|.

Application developers, architects etc work within |Environments| to configure, develop and test applications. These applications are configured in "Farms" which combine Roles, cloud services and orchestration rules together to create easily transportable application infrastructure that can be shared with other |Environments|, can be deployed across different clouds and set up to scale automatically based on the varying demands of each different deployment. Once a Farm has completed development and testing it can be published as a Service Catalog application for self service consumption by other |Accounts| and |Environments|.

Multiple teams can login to each |ENVIRONMENT| and the users functional capability can range from IT sophisticated DevOps users that build applications, through to minimal access Service Catalog users who simply login to launch applications (with one click) that they wish to use.

Menu for a full access |ENVIRONMENT| user:

.. image:: images/environment-full.png
   :scale: 70%

Menu for a Service Catalog |ENVIRONMENT| user:

.. image:: images/environment-sc.png
   :scale: 70%


Images and Roles
----------------
|SCOPE_SCALR| |SCOPE_ACC| |SCOPE_ENV|

Images (aka, AMI, template etc) are the main building blocks for building cloud infrastructure in all clouds. Images are used to create instances/servers in a cloud. Scalr also indirectly makes use of Images stored in the clouds, but in order to do this it requires a record within it's own internal meta data of every image that can be used. Thus an image in Scalr is simply a unique registration of an image that exists in a cloud. Images are used indirectly through Roles and Farm Roles within Scalr. There are three broad types of image.

* Images provided by Scalr that include Scalr's agent called Scalarizer. These Scalr images are ready made to provide the full functionality of Scalr as the agent enables control and monitoring functions. Scalr images are currently available in AWS, GCP and Azure.
* Base images provided by the cloud provider, such as AWS's AMI's
* Images users have created from customized instances with additional pre-installed software and configurations.

Base and user created images can easily be imported into Scalr and converted to scalarized images through the Scalr UI.

Roles provide an abstraction layer over the top of the images and within Scalr a Role is the reusable building block for servers deployed through Scalr. A Role can be associated with multiple similar images from multiple clouds. Similar images will have the same base operating system and version, and the same pre-installed software and configuration. This may or may not include Scalarizer, but all images in a role must be the same in this respect. The effect of this abstraction is that any user can potentially chose which cloud to use when launching a farm/application and they will get exactly the same features and behaviour. A role can also include a set of orchestration rules and global variables which ensures consistent configuration of an instance regardless of which Farm it is used in and which cloud it is deployed in.

Images and Roles can be configured at all three scopes within Scalr and are inherited by the lower scopes. They can only be edited at the scope where they were created, but they can be cloned at lower scopes and the can be promoted from lower scopes to higher scopes.

[Picture needed]

Farms and Farm Roles
--------------------

A Farm is the collection of Roles, Orchestration rules, network configuration, cloud services and much more that defines the desired deployment state of a cloud based system. A Farm can include any number of Roles that work together to provide a service, such as a basic 3-tier app that includes a load balancer, a web app layer and a database layer. The Farm can include all the required automation to bootstrap instances with the required software and auto discover the related services being provided by other roles, e.g. registering web app instances with the load balancer.

When a Role is added to a Farm this is known as a "Farm Role". It inherits all the attributes of the Role itself but extends the configuration to include selection of clouds, locations, network, security groups etc. In other words it turns a role into something that can actually be deployed as a function instance/server in the cloud. The Farm Role can also be parameterised through the use of Global Variables to enable end users to make choices about certain aspects of the deployment at the time it is launched

Desired State Engine
^^^^^^^^^^^^^^^^^^^^



Cost Analytics/Management
-------------------------

Policy Engine
-------------

Users, Teams and Access Control
-------------------------------

Orchestration
-------------

Scripts
-------

Webhooks and External integrations
----------------------------------

Storage
-------

Kubernetes
----------

Service Catalog and Applications
--------------------------------

Scalarizer Agent
----------------

External Integrations
---------------------
