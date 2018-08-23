.. include:: ../GLOBAL.rst

.. _supported-os-start:

Supported Server/Instance Operating Systems
-------------------------------------------

Scalarizr is supported on the following operatings systems and versions.

========================================    ================================
Operating System                            Supported Versions
========================================    ================================
Ubuntu                                      14.04 - 18.04 LTS
Debian                                      6.x - 7.x
RHEL / CentOS                               5.x - 7.x
Windows Server                              2008 R2, 2012(all), and 2016
========================================    ================================

.. supported-os-end

.. _net-req-start:

Scalarizr Network Requirements
------------------------------

Scalarizr needs to be able to communicate bi-directionally with the Scalr server. This table shows the ports that need to be open to enable this and also shows additional ports required to be open when Scalr is deployed on multiple hosts.

=====   ============   =========================================  =================================
Port    Protocol       Direction                                  Usage
=====   ============   =========================================  =================================
80       TCP           Cloud Instance > Scalr Server              Scalarizr Agent
443      TCP           Cloud Instance > Scalr Server              Scalarizr Agent
5671     TCP           Cloud Instance > Scalr Server              Scalarizr Agent (rabbitmq)
6275     TCP           Between Scalr Server Nodes (excluding DB)  RabbitMQ
6276     TCP           Between Scalr Server Nodes (excluding DB)  RabbitMQ
6291     TCP           Between Scalr Server Nodes (excluding DB)  InfluxDB
8008     TCP           Scalr Server > Cloud Instance              Scalarizr Agent (update service)
8010     TCP           Scalr Server > Cloud Instance              Scalarizr Agent (API)
8013     TCP           Scalr Server > Cloud Instance              Scalarizr Agent (control)
15671    TCP           Between Scalr Server Nodes (excluding DB)  RabbitMQ
=====   ============   =========================================  =================================

.. net-req-end

.. _scalarizr-func-start:

Scalarizr Functionality
-----------------------

The Scalarizr agent is optional, but without the agent the Scalr experience is limited, please see the following comparison chart:

========================================    ============   ==================
Capability                                   Agentless      Agent Installed
========================================    ============   ==================
Launch, Terminate, Suspend, Resume            Yes             Yes
Security Group management                     Yes             Yes
Tagging                                       Yes             Yes
Autoscaling                                   No              Yes
Orchestration (script execution)              No              Yes
Monitoring                                    No              Yes
Storage Volume addition	                      No              Yes
Software Firewall/ iptables management		    No              Yes
========================================    ============   ==================

.. scalarizr-func-end
