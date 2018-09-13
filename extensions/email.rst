.. include:: ../GLOBAL.rst

.. _email:

Enable Email Integration
========================

In Scalr you can integrate with a SMTP server to send emails when the following events occur:

* User creation and password resets
* Application provisioning from Service Catalog
* Cost Analytics reports and notifications
* Budget threshold warnings
* Farm Lease expirations
* Non-Standard lease requests/approvals etc

Configuring Email
-----------------
To enable email, add the following settings to your scalr-server.rb:

.. code-block:: ruby

  # Email settings. Unless you set those, Scalr will not deliver email.
  app[:email_from_address] = 'scalr@scalr.example.com'    # Source address for the messages sent by Scalr
  app[:email_from_name] = 'Scalr Service'                 # Source name for the messages sent by Scalr
  app[:email_mailserver] = nil     # Set this to 'host:port' of your SMTP server for email to be delivered. If you don't set it, no mail will be sent. Example '127.0.0.1:25'
  app[:email_configuration] = 'FromLineOverride=YES'   # Additional configuration to inject into /opt/scalr-server/etc/ssmtp/ssmtp.conf.  FromLineOverride=YES allows for "From" override.

.. note:: |SCALR_SERVER_RB|
