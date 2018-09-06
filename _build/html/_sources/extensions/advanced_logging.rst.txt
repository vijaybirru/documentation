.. include:: ../GLOBAL.rst

.. _advanced_logging:

Enable Advanced Logging
========================

Advanced logging can be turned on for administrators to gather more information for the following type of logs:

* Agent Logs - This log will contain all events related to Orchestration. It will contain the same events as found under Orchestration Log in the Scalr UI.
* API Logs - This log contains failed API requests and responses.
* Audit Logs - This log contains different events that happened in Scalr and who triggered them.  It is designed to collect all user initiated actions which should be audited.
* User Logs - This log cotains the system logs that you can see in the UI under System Logs.

Scalr supports real time logging to a fluentd backend which can be configured to act as a funnel before getting stored on any storage backend, such as Plain Text Files, ElasticSearch, MongoDB, or Splunk.

.. |fluentd_link| raw:: html

   <a href="https://www.fluentd.org/download" target="_blank">Fluentd Information</a>

A running Fluentd installation with a configured storage backend is required.. More on installing fluentd here: |fluentd_link| |NEWWIN|.

Fluentd Configuration
----------------------

Once you have installed Fluentd, you'll want to update the config file located in ``/etc/td-agent/td-agent.conf``

.. code-block:: shell

    ####
    ## Output descriptions:
    ##

    # Treasure Data (http://www.treasure-data.com/) provides cloud based data
    # analytics platform, which easily stores and processes data from td-agent.
    # FREE plan is also provided.
    # @see http://docs.fluentd.org/articles/http-to-td
    #
    # This section matches events whose tag is td.DATABASE.TABLE
    <match td.*.*>
      type tdlog
      apikey YOUR_API_KEY

      auto_create_table
      buffer_type file
      buffer_path /var/log/td-agent/buffer/td

      <secondary>
      type file
      path /var/log/td-agent/failed_records
      </secondary>
      </match>

      ## match tag=debug.** and dump to console
      <match *>
      type stdout
      </match>

      ####
      ## Source descriptions:
      ##

      ## built-in TCP input
      ## @see http://docs.fluentd.org/articles/in_forward
      <source>
      type forward
      </source>

      ## built-in UNIX socket input
      #<source>
      #  type unix
      #</source>

      # HTTP input
      # POST http://localhost:8888/<tag>?json=<json>
      # POST http://localhost:8888/td.myapp.login?json={"user"%3A"me"}
      # @see http://docs.fluentd.org/articles/in_http
      <source>
      type http
      bind 0.0.0.0
      port 8888
      </source>

      ## live debugging agent
      <source>
      type debug_agent
      bind 0.0.0.0
      port 24230
      </source>

      ###Tagging for Scalr###
      <match user.***>
      type stdout
      </match>
      <match audit.***>
      type stdout
      </match>
      <match api.***>
      type stdout
      </match>
      <match agent.***>
      type stdout
      </match>

Once you have updated the configuration, restart the td-agent service.

Scalr Configuration
-------------------

To enable the advanced logging, add the following to the scalr-server.rb file:

.. code-block:: ruby

  app[:configuration] = {
    "scalr" => {
      "logger" => {
        "agent" => {
          "enabled" => true,
          "proto" => "http",
          "path" => "hostname of the server hosting fluentD",
          "port" => 8888
        },
        "audit" => {
          "enabled" => true,
          "proto" => "http",
          "path" => "localhost or hostname of the server hosting fluentD",
          "port" => 8888
        },
        "api" => {
          "enabled" => true,
          "proto" => "http",
          "path" => "localhost or hostname of the server hosting fluentD",
          "port" => 8888
        },
        "user" => {
          "enabled" => true,
          "proto" => "http",
          "path" => "localhost or hostname of the server hosting fluentD",
          "port" => 8888
        }
      }
    }
  }

In most cases, the settings above should be fine for your setup. If you do need to change the settings, the full list of fields can be found in the :ref:`logging` section of our advanced configurations page.

.. note::

  The agent log settings must have the hostname of the FluentD server as this information is passed to the agent residing on the server provisioned by Scalr. The logs go directly from the agent to FluentD server.

.. note:: |SCALR_SERVER_RB|

If everything is configured correctly, you will see the logs in ``/var/log/td-agent/td-agent.log``. You can then forward these logs off to your logging solution of choice.

Log Examples
------------

Agent
^^^^^^

.. code-block:: shell

   {
       # Common tags are here
       ...
       # Event specific
       "orchestration.result.event.id": "69dd4b5a-402c-4506-8650-becd9cf683d8",  #
       "orchestration.result.event.name": "HostUp",  # The name of the event
       "orchestration.result.event.triggered_by": "d7c42fd5-9aa6-48c7-88e9-1abd34248e06", # Identifier of the Scalr server that caused this event
       "orchestration.result.execution_id": "9ab98d17-4440-4fbc-a75d-acecea71b2de",  # Identifier of this execution on Scalr.
       "orchestration.result.return_code": 0,  # OS process exit code.
       "orchestration.result.script.name": "Linux_ping_pong",   # The name of the Script
       "orchestration.result.stderr": "",  # Base64 encoded OS process stderr
       "orchestration.result.stdout": "cG9uZwo=\n",  # Base64 encoded OS process stdout
       "orchestration.result.target.env_id": "5",  # Identifier of the Environment the target Server corresponds to
       "orchestration.result.target.farm_id": "9800016",  # Identifier of the Farm the target Server corresponds to
       "orchestration.result.target.farm_role_id": "70",  # Identifier of the Farm Role the target Server corresponds to
       "orchestration.result.target.server_id": "d7c42fd5-9aa6-48c7-88e9-1abd34248e06",  # Identifier of the Server the script executed on
       "orchestration.result.time_elapsed": 0.012,  # Execution time in seconds
       "tags": [
         "agent",
         "orchestration.result"
         ]
      }

API
^^^

.. code-block:: shell

   {
     # common tags are here
     ...

     # API error specific
     "api.error.request.method": "POST" # Request method
     "api.error.request.url": "https://my.scalr.net/api/v1beta0/user/5/images", # Request URL like "<schema>://<user>@<host>:<port>/<path>?<query>"
     "api.error.request.headers": [ # The key-value array of the request headers
       "Content-Type": "application/json; charset=utf-8",
       "X-Scalr-Key-Id": "APIK5D9MNIFPBASMXMLJ",
       ...
       ],
       "api.error.request.body": "{'name': 'foobar', 'cloudImageId': 'i-100500', 'cloudPlatform': 'ec2', 'architecture': 'x86', 'os': 'ubuntu'}", # String representation of the request body
       "api.error.response.status": 400, # Response status code
       "api.error.response.headers": [ # The key-value array of the response headers
       "Status": "InvalidStructure",
       ...
       ],
       "api.error.response.body": "{...}" # String representation of the response body
       "tags": ["api", "api.error"] # The list of tags
     }

Audit
^^^^^

Below is an example of the audit log for a server launch, the following events are also supported:

* User Login
* User Logout
* Farm Launch
* Farm Terminate
* Farm Ownership Change
* Script Execute
* Server Launch
* Server Terminate
* Server Suspend
* Server Resume
* Cloud Resource Remove

.. code-block:: shell

   server.launch {
       # common tags are here
       ...
       # Event specific
       "server.launch.server_id": "2f928baa-4c81-43cb-a280-7c514012bf26", # Identifier of the Server being launched
       "server.launch.farm.id": 12000, # Identifier of the Farm that the Server belongs to
       "server.launch.farm_role.id": 130000, # Identifier of the Farm Role that the Server belongs to
       "server.launch.platform": "ec2", # The platform name where the Server is located
       "server.launch.type": "m1.small", # The name of the instance type of the Server
       "server.launch.cloud_location": "us-east-1", # The region where the Server is located
       "server.launch.os.id": "centos-6-x", # The Identifier of the Os that corresponds to the Server
       "server.launch.environment.id": 1234, # Identifier of the Environment that the Server belongs to
       "server.launch.account.id": 123, # Identifier of the Account that the Server belongs to
       "server.launch.reason.code": 2, # The reason code that caused the Server to be launched
       "server.launch.reason.text": "Scaling up", # The verbose message of the launch reason
       "tags": ["audit", "server.launch"]
       }

User
^^^^

.. code-block:: shell

   {
     # common tags are here
     "timestamp": "2015-10-13T08:31:15-05:00", # RFC-3339 Timestamp when the event happened in server timezone (date --rfc-3339=seconds)

     # Event specific (for server terminate for example)
     "user.log.severity": "warn", # Severity of the event. info | warn | error | ... etc in the lowercase
     "user.log.message": "Terminating server '45ea21c9-4a80-4597-8393-19070f47fd44' (Platform: ec2) (ServerTerminate)."
     "user.log.farm_id": 3454, # Identifier of the Farm
     "user.log.env_id": 12, # Identifier of the Environment
     "user.log.farm_role_id": 48349, # Identifier of the Farm Role (if exists)
     "user.log.server_id": "45ea21c9-4a80-4597-8393-19070f47fd44", # UUID of the Scalr Server (if exists)
     "tags": ["event", "user.log"]
     }
