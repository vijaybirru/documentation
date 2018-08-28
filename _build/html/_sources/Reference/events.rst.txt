.. include:: ../GLOBAL.rst

.. _events:

Event Descriptions
==================

Events are automatically fired by Scalr over the lifecycle of your Servers (Instances) and can be used to trigger :ref:`Scope level <sa_orchestration>`, :ref:`Role <role_orchestration>` and :ref:`Farm Role <farm_role_orchestration>` orchestration rules.

You will find the list of events built in to Scalr below along with details of how each event occurs and their uses. Scalr also supports :ref:`custom_events`.

BeforeInstanceLaunch Event
--------------------------

.. csv-table::
   :header-rows: 1

   Prior Event(s),Event,Following Event(s)
   *None*,**BeforeInstanceLaunch**,HostInit

.. csv-table::
   :widths: 20,100
   :file: csv/BeforeInstanceLaunch.csv

HostInit Event
--------------

.. csv-table::
   :header-rows: 1

   Prior Event(s),Event,Following Event(s)
   BeforeInstanceLaunch,**HostInit**,BeforeHostUp
   ,,HostInitFailed

.. warning:: The HostInit Event does not fire on reboots! To fire Orchestration Rules on reboot, use the `RebootComplete Event`_.

.. csv-table::
   :widths: 30,100
   :file: csv/HostInit.csv

HostInitFailed Event
--------------------

.. csv-table::
   :header-rows: 1

   Prior Event(s),Event,Following Event(s)
   HostInit,**HostInitFailed**,*None*

.. csv-table::
   :widths: 30,100
   :file: csv/HostInitFailed.csv

BeforeHostUp Event
------------------

.. csv-table::
   :header-rows: 1

   Prior Event(s),Event,Following Event(s)
   HostInit,**BeforeHostUp**,HostUp

.. warning:: The BeforeHostUp Event does not fire on reboots! To fire Orchestration Rules on reboot, use the `RebootComplete Event`_.

.. csv-table::
   :widths: 30,100
   :file: csv/BeforeHostUp.csv

HostUp Event
------------

.. csv-table::
   :header-rows: 1

   Prior Event(s),Event,Following Event(s)
   BeforeHostUp,**HostUp**,(EBSVolumeAttached)

.. warning:: The HostUp Event does not fire on reboots! To fire Orchestration Rules on reboot, use the `RebootComplete Event`_.

.. csv-table::
   :widths: 30,100
   :file: csv/HostUp.csv

IPAddressChanged Event
----------------------

.. csv-table::
   :header-rows: 1

   Prior Event(s),Event,Following Event(s)
   HostInit,**IPAddressChanged**,HostUp

.. csv-table::
   :widths: 20,100
   :file: csv/IPAddressChanged.csv

EBSVolumeAttached Event
-----------------------

.. csv-table::
   :header-rows: 1

   Prior Event(s),Event,Following Event(s)
   HostInit,**EBSVolumeAttached**,HostUp

.. warning:: * This event fires for block devices on all clouds, not just EBS block devices.
             * This event **does not** fire on Windows Servers.

.. csv-table::
   :widths: 20,100
   :file: csv/EBSVolumeAttached.csv

EBSVolumeMounted Event
----------------------

.. csv-table::
   :header-rows: 1

   Prior Event(s),Event,Following Event(s)
   HostInit,**EBSVolumeMounted**,HostUp

.. warning:: * This event fires for block devices on all clouds, not just EBS block devices.

.. csv-table::
   :widths: 20,100
   :file: csv/EBSVolumeMounted.csv

BeforeHostTerminate Event
-------------------------

.. csv-table::
   :header-rows: 1

   Prior Event(s),Event,Following Event(s)
   *[Suspend or Terminate]*,**BeforeHostTerminate**,HostDown

.. csv-table::
   :widths: 20,100
   :file: csv/BeforeHostTerminate.csv

.. note:: By default Scalr will make the API call to the Cloud service to terminate the server 3 minutes after the termination request is made in Scalr. However Scalr can be configured to wait until all orchestration scripts run by the BeforeHostTerminate Event have completed before terminating the server. The config parameter ``scalr.system.server_terminate_timeout`` can be set to ``auto`` to enable this. When set to ``auto`` if there are no orchestration scripts on BeforeHostTerminate, Scalr will terminate the server immediately. However, if there are scripts on BeforeHostTerminate, Scalr will terminate the server only when Scalr receives confirmation that the scripts have completed.

HostDown Event
--------------

.. csv-table::
   :header-rows: 1

   Prior Event(s),Event,Following Event(s)
   BeforeHostTerminate,**HostDown**,*None*

.. csv-table::
   :widths: 20,100
   :file: csv/HostDown.csv

.. warning:: * Scalr makes no guarantees as to how long it will take for HostDown to fire after a Server has been terminated.
             * In some cases, the HostDown Event may fire multiple times for a server going offline. Your Orchestration Rules should be ready to handle this condition.

RebootComplete Event
--------------------

.. csv-table::
   :header-rows: 1

   Prior Event(s),Event,Following Event(s)
   RebootBegin,**RebootComplete**,*None*

.. csv-table::
   :widths: 20,100
   :file: csv/RebootComplete.csv

ResumeComplete Event
--------------------

.. csv-table::
   :header-rows: 1

   Prior Event(s),Event,Following Event(s)
   BeforeInstanceLaunch,**ResumeComplete**,*None*

.. csv-table::
   :widths: 20,100
   :file: csv/ResumeComplete.csv
