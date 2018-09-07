.. include:: ../GLOBAL.rst

Scaling Applications
====================

Scalr support two types of scaling, Auto and Manual Scaling. Autoscaling is the best option for applications that are cloud aware, while manual scaling may be the better option for a legacy application that has not been rearchitected for the cloud.

**Autoscaling Mode**

There are two distinct but related ways to use Autoscaling Mode:

* With Simple Autoscaling, Scalr will ensure that you always have at least the minimum and no more than the maximum number of servers up at all times.

* With Dynamic Autoscaling, Scalr will additionally monitor metrics on your servers and dynamically add or remove servers depending on the specified metric threshold (load, response time, etc).

**Manual Scaling Mode**

In Manual Scaling Mode, Scalr does not automatically launch or terminate Servers. A user must launch the Farm and then manually launch a server based on a farm role.
