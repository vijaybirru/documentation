.. include:: ../GLOBAL.rst

.. _kubernetes:

Kubernetes Clusters
====================

Definition and Scope
--------------------

|SCOPE_ACC|

Scalr provides a built-in integration with Kubernetes to manage existing clusters and give a view into the overall health, capacity and workloads on the cluster. Currently, Scalr supports:

* Native Kuberenetes
* GKE Kubernetes

The following Kuberneters offerings will be supported soon:

* Amazon EKS
* Azure AKS

Adding a Cluster
-----------------

To add a cluster into Scalr, go to the |Account| scope and click on the Scalr menu on the top left of the screen |MENU_ACC| and then down to Kubernetes (Preview):

.. image:: images/menu_kubernetes.png
   :scale: 60%

To discover a new cluster, click on New Cluster, select your offering and enter the details:

.. image:: images/new_cluster.png
   :scale: 60%

Once it is successfully added the cluster operation dashboard will appear:

.. image:: images/ops_dashboard.png
   :scale: 60%
