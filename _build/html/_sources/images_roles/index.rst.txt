.. include:: ../GLOBAL.rst

.. _images_roles:

Images and Roles in Scalr
=========================

|SCOPE_SCALR| |SCOPE_ACC| |SCOPE_ENV|

Images and Roles are the two fundamental features of Scalr that allow you to build reusable infrastructure components. We describe Images and Roles in :ref:`terminology` and are reproducing those descriptions here for your convenience.

.. include:: /introduction/terminology.rst
   :start-after: Term-Images-Role-Start
   :end-before: Term-Images-Role-End

Please work through the sections listed below to understand the full details of working with Images and Roles.

* :ref:`registering_images`
* :ref:`roles`
* :ref:`multicloud_roles`
* :ref:`images_from_servers`

Cloning, Promoting and Using
----------------------------

.. |CLONE| image:: images/clone.png
           :scale: 40%

.. |PROMO| image:: images/promote.png
           :scale: 40%

.. |USE| image:: images/use.png
           :scale: 40%

Additional Image and Role options are available from the right hand panel when an Image or Role is selected from the Image or Role list.

.. csv-table::
   :header-rows: 1
   :widths: 25,15,60

   Option,For, Description
   Clone |CLONE|,Role,Create a new role based on an existing Role
   Promote |PROMO|,"Image, Role",Promote to a higher scope to make more widely available
   Use |USE|,Role,Add the Role directly to a Farm from the list
