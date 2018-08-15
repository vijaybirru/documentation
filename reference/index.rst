.. include:: ../GLOBAL.rst

.. _supported-os-start:

Supported Server/Instance Operating Systems
-------------------------------------------

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
