.. include:: ../GLOBAL.rst

Enable SAML Authentication
===========================

Integration with Scalr
^^^^^^^^^^^^^^^^^^^^^^
When SAML is activated, it will move the authentication step outside of Scalr and hand it over to the SAML server that you have configured. During sign in to Scalr, the user will be transferred to a sign in page provided by the SAML server. After sign in, the user will then be redirected back to Scalr which will subsequently treat the user as signed in.

Configuration
^^^^^^^^^^^^^
To enable SAML, you must configure it in the global config file (/etc/scalr-server/scalr-server.rb).

SAML support is activated by setting auth_mode=saml in the Scalr configuration file (scalr-server.rb).  Once this is enabled our entityID is https://scalr.server/public/saml?metadata

Example:

.. code-block:: ruby

   app[:configuration] = {
    "scalr" => {
      "auth_mode" => "saml",
      "connections" => {
        "saml" => {
          "idp" => {
            "entity_id" => "https://idp.domain/saml/metadata",
            "single_sign_on_service" => {
              "url" => "https://your-labs.idp.domain/trust/saml2/http-post/sso"
            },
            "single_logout_service" => {
              "url" => "https://your-labs.idp.domain/trust/saml2/http-redirect/slo"
            },
            "cert_fingerprint" => "AA:BB:CC:DD:EE:FF",
            "cert_fingerprint_algorithm" => "sha256"
            }
          }
        }
      }
    }

The above is an example, you may need to add/remove fields as necessary. The full list of fields can be found in the :ref:`saml` section of our advanced configurations page.

.. note:: |SCALR_SERVER_RB|
