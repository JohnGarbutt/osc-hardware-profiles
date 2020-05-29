2. Edit the ``/etc/osc_hw_profiles/osc_hw_profiles.conf`` file and complete the following
   actions:

   * In the ``[database]`` section, configure database access:

     .. code-block:: ini

        [database]
        ...
        connection = mysql+pymysql://osc_hw_profiles:OSC_HW_PROFILES_DBPASS@controller/osc_hw_profiles
