Prerequisites
-------------

Before you install and configure the osc-hardware-profiles service,
you must create a database, service credentials, and API endpoints.

#. To create the database, complete these steps:

   * Use the database access client to connect to the database
     server as the ``root`` user:

     .. code-block:: console

        $ mysql -u root -p

   * Create the ``osc_hw_profiles`` database:

     .. code-block:: none

        CREATE DATABASE osc_hw_profiles;

   * Grant proper access to the ``osc_hw_profiles`` database:

     .. code-block:: none

        GRANT ALL PRIVILEGES ON osc_hw_profiles.* TO 'osc_hw_profiles'@'localhost' \
          IDENTIFIED BY 'OSC_HW_PROFILES_DBPASS';
        GRANT ALL PRIVILEGES ON osc_hw_profiles.* TO 'osc_hw_profiles'@'%' \
          IDENTIFIED BY 'OSC_HW_PROFILES_DBPASS';

     Replace ``OSC_HW_PROFILES_DBPASS`` with a suitable password.

   * Exit the database access client.

     .. code-block:: none

        exit;

#. Source the ``admin`` credentials to gain access to
   admin-only CLI commands:

   .. code-block:: console

      $ . admin-openrc

#. To create the service credentials, complete these steps:

   * Create the ``osc_hw_profiles`` user:

     .. code-block:: console

        $ openstack user create --domain default --password-prompt osc_hw_profiles

   * Add the ``admin`` role to the ``osc_hw_profiles`` user:

     .. code-block:: console

        $ openstack role add --project service --user osc_hw_profiles admin

   * Create the osc_hw_profiles service entities:

     .. code-block:: console

        $ openstack service create --name osc_hw_profiles --description "osc-hardware-profiles" osc-hardware-profiles

#. Create the osc-hardware-profiles service API endpoints:

   .. code-block:: console

      $ openstack endpoint create --region RegionOne \
        osc-hardware-profiles public http://controller:XXXX/vY/%\(tenant_id\)s
      $ openstack endpoint create --region RegionOne \
        osc-hardware-profiles internal http://controller:XXXX/vY/%\(tenant_id\)s
      $ openstack endpoint create --region RegionOne \
        osc-hardware-profiles admin http://controller:XXXX/vY/%\(tenant_id\)s
