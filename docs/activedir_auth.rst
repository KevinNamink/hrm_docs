.. include:: global_directives.inc

.. _activedir_auth:

*******************************
Active Directory authentication
*******************************

To enable Active Directory authentication, please set the ``$authenticateAgainst`` variable to "ACTIVE_DIR" in ``$CONFIG/hrm_client_config.inc`` and in ``$CONFIG/hrm_server_config.inc``

.. code-block:: php

    <?php
    ...
    // Authentication type: MYSQL, ACTIVE_DIR or LDAP
    $authenticateAgainst = "ACTIVE_DIR";
    ...

Then, copy ``$SAMPLES/active_directory.config.inc.sample`` to ``$CONFIG/active_directory.config.inc`` and edit it.

.. code-block:: php

    <?php
    // This file is part of the Huygens Remote Manager
    // Copyright and license notice: see license.txt

    // See http://adldap.sourceforge.net/wiki/doku.php?id=api_configuration for
    // detailed help on configuring adLdap.

    // The account suffix for your domain
    $ACCOUNT_SUFFIX = "@mydomain.local";
    
    // The base dn for your domain
    $BASE_DN = "DC=mydomain,DC=local"; 
    
    // Array of domain controllers. Specifiy multiple controllers if you would
    // like the class to balance the LDAP queries amongst multiple servers
    $DOMAIN_CONTROLLERS = array ("dc01.mydomain.local");

    // Domain controller port
    $AD_PORT = 389;

    // User name suffix
    $AD_USERNAME_SUFFIX = "";

    // User name suffix matching string
    $AD_USERNAME_SUFFIX_REPLACE_MATCH = "";

    // User name suffix replacing string
    $AD_USERNAME_SUFFIX_REPLACE_STRING = "";

    // Optional account with higher privileges for searching (otherwise
    // leave it to NULL). This should be set to a domain admin account (only
    // read operations are performed!)
    $AD_USERNAME = NULL;
    $AD_PASSWORD = NULL;
    
    // Tweak to get the real primary group from Active Directory. It works if
    // the user's primary group is domain users.
    // http://support.microsoft.com/?kbid=321360
    $REAL_PRIMARY_GROUP = true;
    
    // Use SSL (LDAPS)
    $USE_SSL = false;
    
    // Use TLS: if you wish to use TLS you should ensure that $USE_SSL is 
    // set to false and vice-versa
    $USE_TLS = false;
    
    // When querying group memberships, do it recursively 
    $RECURSIVE_GROUPS = true;

    // Users usually belong to several groups. GROUP_INDEX defines
    // which level of the hierarchy to consider (starts by 0). This
    // obviously assumes that the sequence of groups memberships is
    // constant among users. Set $GROUP_INDEX to -1 to get an array
    // with all groups for the user. Please notice that this can also
    // be used in combination with the next parameter.
    $GROUP_INDEX = 0;

    // If there is no way to get the desired group by using $GROUP_INDEX,
    // this is an additional little trick. For this to work, $GROUP_INDEX
    // MUST be set to -1, and the following array must contain the list of
    // valid groups to be considered. This way, for each user the complete
    // list of groups will be returned from the Active Directory, and of
    // those, the one that is contained in the following array will be picked.
    // If more than one matching group is found, the first will be taken. If
    // no match is found, all groups will be returned.
    // Fill the array as follows: $VALID_GROUPS = array( "group1", "group2" )
    // with as many groups as you need.
    $VALID_GROUPS = array( );    

Special case: Active Directory forests
======================================

In most installations, the variables ``$AD_USERNAME_SUFFIX``, ``$AD_USERNAME_SUFFIX_REPLACE_MATCH`` and ``$AD_USERNAME_SUFFIX_REPLACE_STRING`` can be left unchanged (i.e. ``""``). These are meant for the case where HRM users belong to different Active Directory subdomains, e.g.         

    `user@subdoman@domain.ch`

and they log in to the HRM using:

    `user@subdomain`

Consider following example:

.. code-block:: php

    <?php
    ...
    $BASE_DN = "DC=A, DC=B, DC=C"; 
    $DOMAIN_CONTROLLERS = array("prefix.A.B.C");
    $AD_USERNAME_SUFFIX = ".A.B.C";
    $AD_USERNAME_SUFFIX_REPLACE_MATCH = "@B.A.B.C"
    $AD_USERNAME_SUFFIX_REPLACE_STRING = "@A.B.C"

