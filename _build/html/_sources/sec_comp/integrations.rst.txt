.. include:: ../GLOBAL.rst

.. _webhooks:

Webhooks and Endpoints
======================

Definition and Scope
--------------------

|SCOPE_SCALR| |SCOPE_ACC| |SCOPE_ENV|

Webhooks are very simple, yet very powerful to integrate with external tools like a CMDB, IPAM, ITSM or Monitoring tools. Using Webhooks, Scalr delivers HTTP notifications (API calls) to external services of your choosing when lifecycle events occur on your infrastructure, such as server being provisioned or decommissioned. While Scalr Orchestration could be used to integration with external tools, there are a few constraints with orchestration as a script runs on the server you are provisioning rather than a central location:

* Those external tools may be firewalled off, and not accessible from your instances. This is commonplace for CMDBs.
* Those external tools may require credentials that you wouldn’t feel comfortable distributing to all your instances.
* Those external tools may need to be notified when instances go down or crash, in which case there may not be an instance to run the action on. This is typical for an alerting system.

Unlike Orchestration, Webhook Notifications are delivered by Scalr itself to those external tools, which effectively lifts those limitations.

.. image:: images/webhook_diagram.png
   :scale: 70%



Configuring Endpoints
---------------------

Before creating a Webhook, an endpoint in which the webhook will contact is needed. The endpoint is the URL of the application that is running the webhook, to create an endpoint at the |ACCOUNT| scope, click on the Scalr icon on the top left |MENU_ACC| and then click on Integration Hub > Endpoints.

.. image:: images/new_endpoint.png
   :scale: 70%

+--------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------+
| Field                                      | Description                                                                                                                                                   |
+============================================+===============================================================================================================================================================+
| Name                                       | The name of the endpoint.                                                                                                                                     |
+--------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------+
| URL                                        | The URL the endpoint can be reached at.                                                                                                                       |
+--------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------+
| Status                                     | A radio button to turn make the endpoint active/ inactive within Scalr.                                                                                       |
+--------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------+
| Shared                                     | Determines if the endpoint can be used at a lower level. This is only seen at the |Account| and |Scalr| scopes.                                               |
+--------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------+


Configuring Webhooks
--------------------

The next step is to configure the Webhook, to do this at the |ACCOUNT| scope, click on the Scalr icon on the top left |MENU_ACC| and then click on Integration Hub > Webhooks.

.. image:: images/new_webhook.png
   :scale: 70%

.. csv-table::
   :header-rows: 1
   :file: csv/new_webhook.csv


Webhook Payloads
----------------

A Webhook payload will dump all data it knows about a server built in Scalr to the endpoint application. This includes the Built-In Variables and Global Variables, which you can find out more about here: :ref:`gvs`. The application that is running on the endpoint should be configured in a way that is parses for the relevant data.

Webhook Payloads are dispatched as an HTTP POST request to your Endpoint. Notable features of the request include:

* A JSON body containing the Webhook Notification
* A Date HTTP Header, containing the timestamp when the Webhook Notification was dispatched
* A X-Signature HTTP Header, containing a cryptographic signature of the Webhook Notification
* A X-Scalr-Webhook-Id HTTP Header, containing the ID of the Webhook Notification

The JSON body contains the following keys:

.. csv-table::
   :header-rows: 1
   :file: csv/payload_json.csv

Sample Payload:

.. code-block:: JSON

  {
    "configurationId": "d6e3a602-4a86-4871-9c02-931b543c6df8",
    "data": {
      "SCALR_ACCOUNT_ID": "1",
      "SCALR_ACCOUNT_NAME": "ACME Operations",
      "SCALR_BEHAVIORS": "base",
      "SCALR_CLOUD_LOCATION": "europe-west1-b",
      "SCALR_CLOUD_LOCATION_ZONE": "europe-west1-b",
      "SCALR_CLOUD_PLATFORM": "gce",
      "SCALR_CLOUD_SERVER_ID": "bdc02d5b-613f-4c34-b4fc-04f01db4f118",
      "SCALR_COST_CENTER_BC": "CC-01",
      "SCALR_COST_CENTER_ID": "3f54770e-bf1a-11e3-92c5-000feae9c516",
      "SCALR_COST_CENTER_NAME": "ACME Operations",
      "SCALR_ENV_ID": "2",
      "SCALR_ENV_NAME": "IT Labs US",
      "SCALR_EVENT_ACCOUNT_ID": "1",
      "SCALR_EVENT_ACCOUNT_NAME": "ACME Operations",
      "SCALR_EVENT_BEHAVIORS": "base",
      "SCALR_EVENT_CLOUD_LOCATION": "europe-west1-b",
      "SCALR_EVENT_CLOUD_LOCATION_ZONE": "europe-west1-b",
      "SCALR_EVENT_CLOUD_PLATFORM": "gce",
      "SCALR_EVENT_CLOUD_SERVER_ID": "bdc02d5b-613f-4c34-b4fc-04f01db4f118",
      "SCALR_EVENT_COST_CENTER_BC": "CC-01",
      "SCALR_EVENT_COST_CENTER_ID": "3f54770e-bf1a-11e3-92c5-000feae9c516",
      "SCALR_EVENT_COST_CENTER_NAME": "ACME Operations",
      "SCALR_EVENT_ENV_ID": "2",
      "SCALR_EVENT_ENV_NAME": "IT Labs US",
      "SCALR_EVENT_EXTERNAL_IP": "104.155.70.102",
      "SCALR_EVENT_FARM_HASH": "501a9f8cab6b5f",
      "SCALR_EVENT_FARM_ID": "1824",
      "SCALR_EVENT_FARM_NAME": "Temp Scalr sandbox",
      "SCALR_EVENT_FARM_OWNER_EMAIL": "aloys@scalr.com",
      "SCALR_EVENT_FARM_ROLE_ALIAS": "base-ubuntu1604",
      "SCALR_EVENT_FARM_ROLE_ID": "2682",
      "SCALR_EVENT_FARM_TEAM": "",
      "SCALR_EVENT_ID": "333d5bfa",
      "SCALR_EVENT_IMAGE_ID": "scalr-demo/images/ubuntu1604-gce-scalr-1497530014",
      "SCALR_EVENT_INSTANCE_FARM_INDEX": "1",
      "SCALR_EVENT_INSTANCE_INDEX": "1",
      "SCALR_EVENT_INTERNAL_IP": "10.132.0.3",
      "SCALR_EVENT_ISDBMASTER": "0",
      "SCALR_EVENT_LAUNCHED_BY_EMAIL": "aloys@scalr.com",
      "SCALR_EVENT_LAUNCHED_BY_ID": "80",
      "SCALR_EVENT_NAME": "HostUp",
      "SCALR_EVENT_PROJECT_BC": "PR-01",
      "SCALR_EVENT_PROJECT_ID": "30c59dba-fc9b-4d0f-83ec-4b5043b12f72",
      "SCALR_EVENT_PROJECT_NAME": "IT Lab",
      "SCALR_EVENT_ROLE_NAME": "base-ubuntu1604",
      "SCALR_EVENT_SERVER_HOSTNAME": "scalrserver01",
      "SCALR_EVENT_SERVER_ID": "bdc02d5b-613f-4c34-b4fc-04f01db4f118",
      "SCALR_EVENT_SERVER_TYPE": "n1-standard-4",
      "SCALR_EXTERNAL_IP": "104.155.70.102",
      "SCALR_FARM_HASH": "501a9f8cab6b5f",
      "SCALR_FARM_ID": "1824",
      "SCALR_FARM_NAME": "Temp Scalr sandbox",
      "SCALR_FARM_OWNER_EMAIL": "aloys@scalr.com",
      "SCALR_FARM_ROLE_ALIAS": "base-ubuntu1604",
      "SCALR_FARM_ROLE_ID": "2682",
      "SCALR_FARM_TEAM": "",
      "SCALR_ID": "333d5bfa",
      "SCALR_IMAGE_ID": "scalr-demo/images/ubuntu1604-gce-scalr-1497530014",
      "SCALR_INSTANCE_FARM_INDEX": "1",
      "SCALR_INSTANCE_INDEX": "1",
      "SCALR_INTERNAL_IP": "10.132.0.3",
      "SCALR_ISDBMASTER": "0",
      "SCALR_LAUNCHED_BY_EMAIL": "aloys@scalr.com",
      "SCALR_LAUNCHED_BY_ID": "80",
      "SCALR_PROJECT_BC": "PR-01",
      "SCALR_PROJECT_ID": "30c59dba-fc9b-4d0f-83ec-4b5043b12f72",
      "SCALR_PROJECT_NAME": "IT Lab",
      "SCALR_ROLE_NAME": "base-ubuntu1604",
      "SCALR_SERVER_HOSTNAME": "scalrserver01",
      "SCALR_SERVER_ID": "bdc02d5b-613f-4c34-b4fc-04f01db4f118",
      "SCALR_SERVER_TYPE": "n1-standard-4",
      },
      "endpointId": "4dd66e35-9955-45cc-a6fb-f24e945bf16a",
      "eventId": "417692b9-2f1e-4d08-a7a5-fbb8954a288d",
      "eventName": "HostUp",
      "timestamp": "Wed 06 Sep 2017 12:21:17 UTC",
      "userData": ""
      }

Webhook Security and Authentication
------------------------------------

Scalr adds a cryptographic signature to Webhook Notifications in order for you to be able to validate that they were indeed generated by Scalr.

To validate Webhook Notifications, follow this procedure:

* Obtain the Webhook Endpoint Signing Key for your Endpoint, this is shown as soon as the Webhook is created. Note that the Signing Key is unique to an Endpoint.
* When receiving a Webhook message, compute its signature using the following algorithm (see below for code samples)

  * Concatenate the JSON message payload and the Date header
  * Compute a HMAC digest of the concatenated message, using the SHA-1 algorithm
  * Retrieve the hexadecimal value of the HMAC digest (this is the signature)

* Compare the signature you computed to the one that is found in the X-Signature HTTP Header. For maximum security, ensure you perform a constant-time comparison.

  * If the signatures match, the message is authentic, and was indeed sent by Scalr
  * If the signatures do not match, the message is a forgery, and was not sent by Scalr


To compute a Webhook Notification signature in PHP, use the following algorithm. We assume that the $payload variable contains the request JSON payload, and that timestamp contains the Date Header.

.. code-block:: shell

  $canonical_string = $payload . $timestamp;
  $signature = hash_hmac('SHA1', $canonical_string, $endpoint->securityKey);

Webhook History
---------------

To track Webhook calls as well as troubleshoot if you suspect an integration is failing, there is a Webhook History section that will provide this information. It shows if the call was completed/failed as well as exit codes:

Highly Available Webhooks
--------------------------

Highly-available Webhooks can be simply deployed using DNS-based high availability. To achieve this, you should ensure that:

* A DNS name is assigned to the webhook service (e.g. webhook.scalr.corp.com).
* The Webhook Endpoint is Scalr is configured with this DNS name.
* The Webhook server itself can be replicated to make it highly available. Since most webhook handlers are stateless, this should not be an issue.
* Several instances of the webhook server are deployed.
* The DNS server returns several A records for the webhook service, one for each webhook server instance.

.. code-block:: shell

  ; <<>> DiG 9.10.6 <<>> webhook.scalr.corp.com
  ;; global options: +cmd
  ;; Got answer:
  ;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 60289
  ;; flags: qr rd ra ad; QUERY: 1, ANSWER: 2, AUTHORITY: 0, ADDITIONAL: 1

  ;; OPT PSEUDOSECTION:
  ; EDNS: version: 0, flags:; udp: 4096
  ;; QUESTION SECTION:
  ;webhook.scalr.corp.com. IN A

  ;; ANSWER SECTION:
  webhook.scalr.corp.com. 3600 IN A 35.187.188.42
  webhook.scalr.corp.com. 3600 IN A 35.195.169.152

  ;; Query time: 15 msec
  ;; SERVER: 192.168.5.1#53(192.168.5.1)
  ;; WHEN: Mon Jun 25 20:17:15 CEST 2018
  ;; MSG SIZE rcvd: 90

If your webhook server is deployed from Scalr, and your Scalr installation is integrated with your DNS system, steps 4 and 5 can be as simple as scaling up the Farm Role of the webhook.

If all these conditions are met, Scalr will correctly and quickly retry webhook requests if one of the servers becomes unavailable, making the webhook integration highly available. As long as one server is reachable, you will not see any errors in the Scalr webhook log.

Naturally, this should be coupled with a monitoring and alerting system to ensure that this doesn't just hide failures.

Example Webhooks
----------------

To see examples of Webhooks please visit our Github site: |scalr_github_link| |NEWWIN|
