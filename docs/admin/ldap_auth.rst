.. include:: global_directives.inc

.. _ldap_auth:

*******************
LDAP authentication
*******************

To enable LDAP authentication, please set the ``$authenticateAgainst`` variable to "LDAP" in ``$HRM_CONFIG/hrm_client_config.inc`` and in ``$HRM_CONFIG/hrm_server_config.inc``

.. code-block:: php

    <?php
    ...
    // Authentication type: MYSQL, ACTIVE_DIR or LDAP
    $authenticateAgainst = "LDAP";
    ...

Then, copy ``$HRM_SAMPLES/ldap.config.inc.sample`` to ``$HRM_CONFIG/ldap.config.inc`` and edit it.

.. code-block:: php

    <?php
    // This file is part of the Huygens Remote Manager
    // Copyright and license notice: see license.txt

    // the machine on which the ldap server is running
    $ldap_host = "localhost";

    // the port for the ldap connection
    $ldap_port="389";

    // Use SSL (LDAPS)
    $ldap_use_ssl = false;

    // Use TLS: if you wish to use TLS you should ensure that $ldap_use_ssl is 
    // set to false and vice-versa
    $ldap_use_tls = false;

    // the ldap root
    $ldap_root="dc=root,dc=country";

    // the base for the manager DN (either cn or uid)
    $ldap_manager_base_DN="cn";

    // the ldap manager (username only!)
    $ldap_manager="manager";

    // the ldap manager password
    $ldap_password = "secret";

    // ldap manager OU: use this in case the ldap_manager is in some special OU
    // that distinguishes it from the other users. $ldap_manager_ou will be
    // prepended to $ldap_user_search_DN.
    // Set it to "" if $ldap_user_search_DN can be used for binding
    $ldap_manager_ou="ou=special_user";

    // User search DN (without ldap root)
    $ldap_user_search_DN="cn=users";

    // Users often belong to more than one group. To filter for the desired one,
    // fill the $ldap_valid_groups array with the ones to be filtered against.
    // If more than one group fits, the first will be taken.
    // Fill the array as follows: $ldap_valid_groups = array( "group1", "group2" )
    // with as many groups as you need.
    $ldap_valid_groups = array( );

