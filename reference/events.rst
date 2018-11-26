.. include:: ../GLOBAL.rst

.. _events:

Event Descriptions
==================

Events are automatically fired by Scalr over the lifecycle of your Farms and Servers (Instances). For Servers these events can be used to trigger :ref:`Scope level <sa_orchestration>`, :ref:`Role <role_orchestration>` and :ref:`Farm Role <farm_role_orchestration>` orchestration rules. For Farms events can be linked to :ref:`webhooks` to trigger integration actions with external systems.

You will find the list of events built in to Scalr below along with details of how each event occurs and their uses. Scalr also supports :ref:`custom_events`.

Farm Life Cycle Events
----------------------

Farm Events can only currently be used with :ref:`webhooks` and :ref:`approvals`

**BeforeFarmLaunch**

* Farm launch has been requested. In this stage a Farm is in the "Pending launch" state and waiting for "approval" (if one is required).
* Any Farm's cloud resources cannot be launched in this state considering that previous state was Terminated.
* Event is triggered as soon as Farm is launched.

**FarmLaunched**

* Farm has successfully been launched. Farm status is Running.
* When "approval" is not required this event is triggered immediately after BeforeFarmLaunch event independently from the statuses of the Farm's Servers. If approval is required the event is triggered as soon the "approval" is received.

**FarmSuspended**

* Farm has been suspended.
* Triggered as soon as Farm is suspended by the initiator (User, Lease manager / lights out functionality)

**FarmResumed**

* Farm has been resumed.
* Triggered as soon as Farm has resumed by the initiator (User, Lease manager / lights out functionality)

**BeforeFarmTerminate**

* Termination of Farm has been requested. The Farm will be in "Pending terminate" state and waiting for the "approval" if required.
* All cloud resources remain in their current state.

**FarmTerminated**

* Farm has been terminated.
* All Farm's servers are put in the Pending terminate state at this point.
* Triggered immediately after BeforeFarmTerminate event if the "approval" is not required, or as soon as it is received otherwise.

Server Life Cycle Events
------------------------

.. note:: The ONLY guaranteed sequence for events occurs when a server is booting up and the events are being processed on the triggering server. |BR| This sequence is HostInit -> BeforeHostUp -> HostUp.

.. warning:: The sequence/order that events are received when the target is NOT the triggering server or the target is a Webhook ARE NOT guaranteed and may vary from case to case due to the multithreaded processing of events in Scalr.

----

BeforeInstanceLaunch Event
~~~~~~~~~~~~~~~~~~~~~~~~~~

.. csv-table::
   :widths: 20,100
   :file: csv/BeforeInstanceLaunch.csv

----

HostInit Event
~~~~~~~~~~~~~~

.. warning:: The HostInit Event does not fire on reboots! To fire Orchestration Rules on reboot, use the `RebootComplete Event`_.

.. csv-table::
   :widths: 30,100
   :file: csv/HostInit.csv

----

HostInitFailed Event
~~~~~~~~~~~~~~~~~~~~

.. csv-table::
   :widths: 30,100
   :file: csv/HostInitFailed.csv

----

BeforeHostUp Event
~~~~~~~~~~~~~~~~~~

.. warning:: The BeforeHostUp Event does not fire on reboots! To fire Orchestration Rules on reboot, use the `RebootComplete Event`_.

.. csv-table::
   :widths: 30,100
   :file: csv/BeforeHostUp.csv

----

HostUp Event
~~~~~~~~~~~~

.. warning:: The HostUp Event does not fire on reboots! To fire Orchestration Rules on reboot, use the `RebootComplete Event`_.

.. csv-table::
   :widths: 30,100
   :file: csv/HostUp.csv

----

IPAddressChanged Event
~~~~~~~~~~~~~~~~~~~~~~

.. csv-table::
   :widths: 20,100
   :file: csv/IPAddressChanged.csv

.. note:: IPAddressChanged event fires when a Server is Resumed. The \*OLD\* variables will show the old IP Address as "N/A"

----

EBSVolumeAttached Event
~~~~~~~~~~~~~~~~~~~~~~~

.. warning:: * This event fires for block devices on all clouds, not just EBS block devices.
             * This event **does not** fire on Windows Servers.

.. csv-table::
   :widths: 20,100
   :file: csv/EBSVolumeAttached.csv

----

.. _EBSVolumeMounted:

EBSVolumeMounted Event
~~~~~~~~~~~~~~~~~~~~~~

.. warning:: * This event fires for block devices on all clouds, not just EBS block devices.

.. csv-table::
   :widths: 20,100
   :file: csv/EBSVolumeMounted.csv

----

BeforeHostTerminate Event
~~~~~~~~~~~~~~~~~~~~~~~~~

.. csv-table::
   :widths: 20,100
   :file: csv/BeforeHostTerminate.csv

.. note:: By default Scalr will make the API call to the Cloud service to terminate the server 3 minutes after the termination request is made in Scalr. However Scalr can be configured to wait until all orchestration scripts run by the BeforeHostTerminate Event have completed before terminating the server. The config parameter ``scalr.system.server_terminate_timeout`` can be set to ``auto`` to enable this. When set to ``auto`` if there are no orchestration scripts on BeforeHostTerminate, Scalr will terminate the server immediately. However, if there are scripts on BeforeHostTerminate, Scalr will terminate the server only when Scalr receives confirmation that the scripts have completed.

----

HostDown Event
~~~~~~~~~~~~~~

.. csv-table::
   :widths: 20,100
   :file: csv/HostDown.csv

.. warning:: * Scalr makes no guarantees as to how long it will take for HostDown to fire after a Server has been terminated.
             * In some cases, the HostDown Event may fire multiple times for a server going offline. Your Orchestration Rules should be ready to handle this condition.

----

RebootComplete Event
~~~~~~~~~~~~~~~~~~~~

.. csv-table::
   :widths: 20,100
   :file: csv/RebootComplete.csv

----

ResumeComplete Event
~~~~~~~~~~~~~~~~~~~~

.. csv-table::
   :widths: 20,100
   :file: csv/ResumeComplete.csv
