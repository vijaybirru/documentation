.. include:: ../GLOBAL.rst

Connecting Scalr to OpenStack
=============================

Scalr needs access to your Cloud Platform(s) in order to provision and manage infrastructure on your behalf. You will therefore need to configure Scalr with your OpenStack credentials. There are 4 steps to this task.

1. Configure OpenStack API Access
2. Configure VPC's
3. Configure Instance Connection Policy
4. Add OpenStack credentials to Scalr and link to |ENVIRONMENTS|.

.. note::
   | **Your credentials are safe with us**
   | Credentials are stored securely and encrypted. Scalr will not use your Credentials for any purpose you have not agreed to. Our terms of service can be found on the Scalr Website Policies Page.
   | **Why Does Scalr Need Credentials?**
   | Cloud Credentials are needed by Scalr to provision and manage cloud infrastructure on your behalf.

Configuring OpenStack for Scalr
-------------------------------

Before creating access keys and connecting Scalr to OpenStack there are some configuration considerations that may need to implemented to ensure Scalr can connect to your instances in OpenStack.

Configure OpenStack API Access
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Scalr and the Scalr Agent ("Scalarizr") need to be able to reach the OpenStack API ports for a certain number of OpenStack services. These ports should therefore be available for access by your Scalr Server, and by the instances it is managing.

.. warning::
   | Your OpenStack installation may make those services available on a non-default port. To find out the exact port for your installation, use the following OpenStack CLI command:
   | ``keystone catalog``

.. note:: All ports to be opened will be TCP and only need to be open in one direction, Scalr Server > OpenStack and Scalarizr Agent > OpenStack.

===========  ========== ============= ============
Description  Name       Type          Default Port
===========  ========== ============= ============
Nova         nova       compute       8774
Keystone     keystone   identity      5000
Neutron      neutron    network       9696
Swift        swift      object-store  8080
Glance API   glance     image         9292
Cinder       cinder_v2  volumev2      8776
===========  ========== ============= ============

Configure Virtual Private Cloud (VPC)
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. |vpc_link| raw:: html

   <a href="hhttps://wiki.openstack.org/wiki/Blueprint-VPC" target="_blank">Blueprint VPC</a>

.. |peer_link| raw:: html

   <a href="https://docs.openstack.org/networking-bgpvpn/latest/" target="_blank">Neutron BGP VPN Interconnection Documentation</a>

You have the option to create or configure an OpenStack VPC to work with Scalr. This isnt strictly required but please refer to |vpc_link| |NEWWIN| for more information.

Configure Instance Connection Policy
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

You will also need to perform some additional configuration work to ensure that Scalr can connect to your OpenStack instances. There are three options for this.

#. **Public** - Scalr will ONLY connect to the Public IP of instances. Only use this option if ALL instances managed by Scalr will have a Public IP.
#. **Local** - Scalr will ONLY connect to the local/private IP of instances. This option is only possible if one of the following scenarios applies.

   #. All your managed instances are in the same Network or VPC as the Scalr server.
   #. You have routing or peering connections to all the other Networks/VPC's where Scalr managed instances reside. For some information on establishing peer connections between OpenStack networks via VPN please see |peer_link| |NEWWIN| for more details.

#. **Auto** - (default) Scalr will connect to the Public IP of an instance if it has one, otherwise it will fall back to the local/private IP.

If you choose to use the "public" or "local" option then you need to login to your Scalr server and update the configuration in ``/etc/scalr-server/scalr-server.rb`` by adding the following entry. (NOTE: this entry must be merged with any exiting entries in the ```app[:configuration] = ``` structure)

.. code-block:: python

   app[:configuration] = {
    "scalr" => {
      "openstack" => {
        "instance_connection_policy" => "local" or "public"
       }
     }
   }

After adding this entry you must re-configure scalr by running ``sudo scalr-server-ctl reconfigure``.


Adding OpenStack Credentials to Scalr
-------------------------------------

.. include:: credentials-generic.rst

1. After selecting Add Credentials, you will be prompted to configure your Cloud Credentials and properties:

.. image:: images/OpenStack-creds.png
   :scale: 70%

2. Enter the credentials and other details for OpenStack and Click Save. You will see a screen similar to this.

.. image:: images/OpenStack-creds_2.png
  :scale: 70%

.. |CACHE| image:: images/cache-clear.png
           :scale: 40%

.. note:: The Openstack credentials screen includes cache clear button |CACHE|. Scalr maintains a cache of Openstack Flavors (instance sizes) which it refreshes every 24 hours. If you make changes to Flavors in Openstack, and these are not being reflected in Scalr, you can click on the "CLEAR" button and Scalr will refresh the cache.

You can now proceed to adding these credentials to your |ENVIRONMENTS|.
