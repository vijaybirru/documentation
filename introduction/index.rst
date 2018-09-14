.. include:: ../GLOBAL.rst

Overview of Scalr
=================

Scalr is a Cloud Management Platform that provides the capability to manage cloud infrastructure across all the major cloud platforms. Scalr's core capabilities are as follows.

* Cloud agnostic definition of infrastructure enabling single application configurations to be used across multiple cloud platforms. Configure once, Deploy Many.
* Capability to centralise and delegate policy administration through Software Defined Cloud Governance to ensure consistent implementation of Security and Compliance policies across all cloud deployments.
* Cost visibility and control through a single pane of glass.

All of this is provided whilst retaining the the flexibility and productivity that organisations require by putting the control and governance in the hands of managers and administrators, but leaving the development and configuration of cloud deployments in the hands of developers, testers and project teams.

Multi-Cloud Support
-------------------

Scalr provides a single UI, API, and CLI to manage resources across any Cloud Platform, public or private.

Scalr strives to expose a common set of features across all clouds, but does not limit the feature set available to users (e.g. IAM Instance Profiles are available through Scalr for AWS, even if they have no equivalent in other clouds). In addition Scalr provides robust support for the different Cloud Services provided by the individual Cloud Providers, including, but not limited to, services like S3 and RDS on AWS, and SQL in GCE

High-Level Declarative Primitives vs Low-Level Imperative Instructions
----------------------------------------------------------------------

Unlike a Cloud Platform's UI or API, Scalr intentionally does not expose the ability to imperatively provision resources  (e.g. there is no API Call to "provision an instance").

Instead, Scalr enables its end-users to declare the infrastructure they'd like to deploy through high-level primitives such as Farms, Roles, and Farm Roles.

.. pull-quote:: *"I'd like this application tier to be deployed in this cloud across 12 hosts, each with one data volume"*

In turn Scalr maintains that state by making the appropriate imperative API Calls to the underlying Cloud Platforms. When unexpected conditions arise (e.g. a Server crashes and gets terminated), then Scalr automatically reconciles existing infrastructure with the specification provided by the user (e.g. by provisioning and configuring a replacement instance).

We believe (and so do Scalr users) that this encourages end-users to adopt cloud architecture best practices that work at scale — i.e. not to focus on individual resources, but rather on the overall state of their infrastructure (a design practice epitomized by the "cattle, not pets" saying).

Usable by Both Developers and IT
--------------------------------

Scalr reconciles the needs of both DevOps and IT. At a high-level, developers needs self-service, and IT needs control. While the two might seem incompatible they usually aren't, and developers are usually OK with complying with IT policies provided they don't slow them down.

To support this use case, Scalr seeks to provide IT with the ability to transparently enforce policies that automatically ensure that every piece of infrastructure that developers provision is automatically made compliant with the organization's policies, whether that is achieved through the enforcement of a specific cloud configuration (Governance), user-level restrictions (Role-Based Access Control), enforcing host-level compliance policies (Account-Scope Orchestration), or integrating with external systems (Webhooks).

Scalr Architecture
==================

Scalr is comprised of two main software components.

1. **Scalr Server**. This is installed on one or hosts and provides the user interface, API's, meta data storage and all necessary processes to interface with the API's of clouds and manage the instances/servers running in the cloud. Scalr Server is sometimes referred to as Scalr Core.
2. **Scalarizer Agent**. The agent is installed in all instances/servers running in clouds that are managed by Scalr. It's purpose is to execute actions in the instances upon receipt of those actions from the Scalr Server, and to provide monitoring and status information back to the Scalr Server.

Scalr Server can be installed on a single host but this would typically only be done for non-critical installations, such as staging or pre-prod environment. For production use Scalr should be installed on multiple hosts and configured with HA and redundancy to ensure continuity of service.

Software Architecture
---------------------

.. image:: images/sw_arch.png
   :scale: 50%
