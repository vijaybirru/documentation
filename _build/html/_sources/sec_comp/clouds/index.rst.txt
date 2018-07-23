.. include:: ../GLOBAL.rst

Scalr must be configured to connect to the Cloud API's of the clouds you wish to manage through Scalr. This configuration is called "Cloud Credentials". Cloud Credentials are linked to |LEV3s| to enable Farms to be configured to use your clouds. An |LEV3| can be linked to multiple clouds which enables DevOps to implement distributed deployments, and/or provide users with the option to choose a cloud when using Self Service deployment through the Service Catalog.

Cloud credentials in Scalr can be configured globally at the |SCALR| scope for all |Accounts| and |Environments| or at the |ACCOUNT| Scope so they are restricted to |Environments| within the |ACCOUNT|.

For details on configuring Scalr for the different cloud services, please follow the appropriate link(s) below.

.. toctree::
   :maxdepth: 1

   ../clouds/connecting_aws
   ../clouds/connecting_gcp
   ../clouds/connecting_azure
   ../clouds/connecting_openstack
   ../clouds/connecting_vmware
