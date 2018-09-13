.. include:: ../GLOBAL.rst

.. _ldap_auth:

Enable LDAP Authentication
===========================

Scalr supports LDAP Authentication and authorization using Active Directory, both for the Web Control Panel and the API.

Configuration
^^^^^^^^^^^^^
To enable LDAP, you must configure it in the global config file (/etc/scalr-server/scalr-server.rb).

.. code-block:: ruby

   app[:configuration] = {
    :scalr => {
     # Tells Scalr to use LDAP for authentication
      :auth_mode => 'ldap',
      :connections => {
        :ldap => {
         # Tells Scalr what LDAP server to connect to
          :bind_type => 'regular',
          :host => 'ldap://Na.Corp.Company.com',
          :port => ‘389’,
        # Tells Scalr what LDAP service account to use when validating users
          :user => ‘User’,
          :pass => ‘Password’,
    # Swap with above for LDAPS
    #:host => 'ldaps://Na.Corp.Company.com',
      #:port => '636',

          # Tells Scalr where to look for users and groups
          :base_dn => 'OU=Accounts Active,OU=Enterprise,DC=Na,DC=Corp,DC=Company,DC=com',
          :base_dn_groups => 'DC=Na,DC=Corp,DC=Company,DC=com',

          # Tells Scalr what attributes to look at
          :username_attribute => 'sAMAccountName',
          :groupname_attribute => 'sAMAccountName',


          # Tells Scalr how group membership is represented
          :group_member_attribute_type => 'member',

          # Tells Scalr to use filters to speed up queries
          :filter => {
          :users => '(&(objectClass=user))',
          :groups => '(&(objectClass=group))',
          },

          # Uncomment for debug output if you can't login
          :debug => 1,
        }
      }
    }
  }

    # This will be injected into your ldap.conf
    # Uncomment and configure cert settings when using ldaps
    #app[:ldap_configuration] = '
    #TLS_CACERT /etc/ssl/f5.pem
    #TLS_CIPHER_SUITE TLSv1+RSA

The above is an example, you may need to add/remove fields as necessary. The full list of fields can be found in the :ref:`ldap` section of our advanced configurations page.

.. note:: |SCALR_SERVER_RB|
