=====   ============   =========================================  =================================
Port    Protocol       Direction                                  Usage
=====   ============   =========================================  =================================
80       TCP           Cloud Instance > Scalr Server              Scalarizr Agent
443      TCP           Cloud Instance > Scalr Server              Scalarizr Agent
5671     TCP           Cloud Instance > Scalr Server              Scalarizr Agent (rabbitmq)
6275     TCP           Between Scalr Server Nodes (excluding DB)  RabbitMQ
6276     TCP           Between Scalr Server Nodes (excluding DB)  RabbitMQ
6291     TCP           Between Scalr Server Nodes (excluding DB)  InfluxDB
8008     TCP           Scalr Host > Cloud Instance                Scalarizr Agent (update service)
8010     TCP           Scalr Host > Cloud Instance                Scalarizr Agent (API)
8013     TCP           Scalr Host > Cloud Instance                Scalarizr Agent (control)
15671    TCP           Between Scalr Server Nodes (excluding DB)  RabbitMQ
=====   ============   =========================================  =================================
