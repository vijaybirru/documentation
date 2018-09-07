.. include:: ../GLOBAL.rst

Cloud Service Gateway
=====================

In order to ensure a consistent multi-cloud experience for cross-cloud automation, policy enforcement, cost visibility, and access control, typically Cloud Management Platforms will enforce limitations on what services are available for consumption by developers.  This can create issues when developers need access to services that are not otherwise available to them, and may result in undesired actions being taken by those users that are contrary to your goals and policies.  Scalr's solution to this conundrum is the Scalr Cloud Service Gateway, or CSG.  By utilizing the CSG, you’ll gain the benefits of cloud management for these services without the previous limitations.

The Scalr CSG acts as a transparent proxy between your applications and cloud provider services   By maintaining this gateway within Scalr, you receive the benefits of complete compatibility with tools, documentation, etc. Developers just point to the CSG endpoint configured and hosted in your Scalr infrastructure and everything works the same as it does for other natively supported cloud service, but you’ll now receive visibility into and control over service consumption.

Configuring Cloud Service Gateway
---------------------------------

To enable the CSG on your deployment, add the following to your scalr-server.rb:

.. code-block:: shell

  # Enable the CSG service
  csg[:enable] = true

  # Root CA. Users must configure their clients to trust csg[:cert] SSL certificate. This must be a SELF SIGNED cert.
  csg[:cert] = '/etc/scalr-server/csg.crt'
  csg[:key] = '/etc/scalr-server/csg.key'

  # Set port CSG will listen on. Default is 3128, like in most HTTP(S) proxies.
  csg[:bind_port] = 3128
  # csg[:bind_host] should be this host's public domain name.
  # If you have a single node deployment, this will be simply routing[:endpoint_host]
  # For a multi node deployment, this will be the host that CSG resides on.  Be sure to update your scalr-server-local.rb
  csg[:bind_host] = routing[:endpoint_host]

  # Logger (optional)
  #app[:configuration] = {
  #  :scalr => {
  #    "logger" => {
  #      "csg" => {
  #        "backend" => "logstash",
  #        "proto" => "tcp",
  #        "path" => "logstash.local",
  #        "port" => 8888,
  #        "enabled" => true
  #      }
  #    }
  #  }
  #}

.. note:: If you have a multi server Scalr deployment, the ``csg[:enable] = true`` section must be added to the scalr-server-local.rb of the server that it will run on, not the scalr-server.rb

.. note:: |SCALR_SERVER_RB|

Using the Cloud Service Gateway
-------------------------------

The overall flow of the CSG is as follows:

1. Developers request access to AWS services that aren’t accessible through Farms: Lambda, Elastic Container Services (ECS), Route53, Glacier, API Gateway, Simple Notification Service (SNS), Simple Email Service (SES), Redshift, and DynamoDB
2. Users with permission Account Management > Cloud Service Access Requests can view who has requested which services, and approve or deny access

3. Developers whose request is approved get access to the endpoint, key, and secret they need to access the services. These keys and secrets work on the Scalr hosted endpoint which acts as an HTTP proxy, and Scalr handles the authentication to the cloud service.

4. Applications use the service, and Scalr provides access via the CSG.

An end user interested in using the Cloud Service Gateway will need to begin by accessing their environment of choice and selecting the user drop down in the upper right corner of your display.  Next, select Cloud Services.

.. image:: images/cloud_services.png
   :scale: 50%

Once you are on the Cloud Services page, click Request Access and select the cloud and service(s) that you want access to:

.. image:: images/cloud_services_request.png
   :scale: 50%

After you request the services, they must be approved or denied by the account administrator. Within the Cloud Services page you can manage the services you have requested.

Once a request has been approved, select the Details icon to view additional details. Access details will be presented in a new pop-up.  Use the information presented here to configure and leverage access to your approved Cloud Services:

.. image:: images/secret_key.jpg
   :scale: 60%

.. image:: images/access_details1.jpg
    :scale: 60%

.. image:: images/access_details2.jpg
    :scale: 60%

.. note:: Upon initial Approval and access of the Details menu, a one time Secret Key will be provided to the end user.  This key MUST be saved as it will never be presented again.

Client Configuration Details
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

API client / CLI must support SNI in order to establish a proper TLS connection with Cloud Service Gateway. If you don't have SNI support you'll get the following error client side:

.. code-block:: shell

  [SSL: CERTIFICATE_VERIFY_FAILED] certificate verify failed (_ssl.c:600)

The server side error in the cloud-service-gateway.log would look like the following:

.. code-block:: shell

  << Cannot establish TLS with queue.amazonaws.com:443 (sni: None): TlsException('Cannot validate certificate hostname without SNI',)

AWS-CLI / AWS-SDK / Boto - Python 2.7.9+ and Python3 works without any need for additional configuration.

.. note:: Regardless of AWS CLI version, you would still need Python 2.7.9+ due to the requirement for SNI support in Python.

Managing approvals for Cloud Service Gateway
--------------------------------------------

|Account| Admins, or users with the appropriate ACLs, will have the ability to manage Cloud Service Access Requests from the |Account| Scope.

Begin by selecting the Cloud Service Access Request item from the Main Menu:

.. image:: images/csg_approval.png
    :scale: 50%

And approve or deny the request:

.. image:: images/csg_approval_page.png
    :scale: 90%

You must select the cloud credentials that will be used when making a call via the CSG:

.. image:: images/csg_approval_cloud_creds.png
    :scale: 50%

From this page you can also revoke, archive, and manage existing requests.
