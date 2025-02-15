Configuration
=============

Phoenix 6 simplifies the configuration process through the use of device-specific ``Configuration`` classes, as well as configuration groups.

.. note:: For more information about configuration in Phoenix 6, see :doc:`/docs/api-reference/api-usage/configuration`.

Applying Configs
----------------

.. list-table::
   :width: 100%
   :widths: 1 99

   * - .. centered:: v5
     - .. tab-set::

         .. tab-item:: Java
            :sync: Java

            .. code-block:: Java

               // set slot 0 gains
               // 50 ms timeout on each config call
               m_motor.config_kF(0, 0.05, 50);
               m_motor.config_kP(0, 0.046, 50);
               m_motor.config_kI(0, 0.0002, 50);
               m_motor.config_kD(0, 0.42, 50);

         .. tab-item:: C++
            :sync: C++

            .. code-block:: cpp

               // set slot 0 gains
               // 50 ms timeout on each config call
               m_motor.Config_kF(0, 0.05, 50);
               m_motor.Config_kP(0, 0.046, 50);
               m_motor.Config_kI(0, 0.0002, 50);
               m_motor.Config_kD(0, 0.42, 50);

   * - .. centered:: v6
     - .. tab-set::

         .. tab-item:: Java
            :sync: Java

            .. code-block:: java

               // set slot 0 gains
               var slot0Configs = new Slot0Configs();
               slot0Configs.kV = 0.12;
               slot0Configs.kP = 0.11;
               slot0Configs.kI = 0.5;
               slot0Configs.kD = 0.001;

               // apply gains, 50 ms total timeout
               m_talonFX.getConfigurator().apply(slot0Configs, 0.050);

         .. tab-item:: C++
            :sync: C++

            .. code-block:: cpp

               // set slot 0 gains
               configs::Slot0Configs slot0Configs{};
               slot0Configs.kV = 0.12;
               slot0Configs.kP = 0.11;
               slot0Configs.kI = 0.5;
               slot0Configs.kD = 0.001;

               // apply gains, 50 ms total timeout
               m_talonFX.GetConfigurator().Apply(slot0Configs, 50_ms);

Factory Defaulting Configs
^^^^^^^^^^^^^^^^^^^^^^^^^^

.. list-table::
   :width: 100%
   :widths: 1 99

   * - .. centered:: v5
     - .. tab-set::

         .. tab-item:: Java
            :sync: Java

            .. code-block:: Java

               // user must remember to factory default if they configure devices in code
               m_motor.configFactoryDefault();

         .. tab-item:: C++
            :sync: C++

            .. code-block:: cpp

               // user must remember to factory default if they configure devices in code
               m_motor.ConfigFactoryDefault();

   * - .. centered:: v6
     - .. tab-set::

         .. tab-item:: Java
            :sync: Java

            .. code-block:: Java

               // any unmodified configs in a configuration object are *automatically* factory-defaulted;
               // user can perform a full factory default by passing a new device configuration object
               m_motor.getConfigurator().apply(new TalonFXConfiguration());

         .. tab-item:: C++
            :sync: C++

            .. code-block:: cpp

               // any unmodified configs in a configuration object are *automatically* factory-defaulted;
               // user can perform a full factory default by passing a new device configuration object
               m_motor.GetConfigurator().Apply(TalonFXConfiguration{});

Retrieving Configs
------------------

.. list-table::
   :width: 100%
   :widths: 1 99

   * - .. centered:: v5
     - .. tab-set::

         .. tab-item:: Java
            :sync: Java

            .. code-block:: Java

               // a limited number of configs have configGet* methods;
               // for example, you can get the supply current limits
               var supplyCurLim = new SupplyCurrentLimitConfiguration();
               m_motor.configGetSupplyCurrentLimit(supplyCurLim);

         .. tab-item:: C++
            :sync: C++

            .. code-block:: cpp

               // a limited number of configs have ConfigGet* methods;
               // for example, you can get the supply current limits
               SupplyCurrentLimitConfiguration supplyCurLim{};
               m_motor.ConfigGetSupplyCurrentLimit(supplyCurLim);

   * - .. centered:: v6
     - .. tab-set::

         .. tab-item:: Java
            :sync: Java

            .. code-block:: Java

               var fx_cfg = new TalonFXConfiguration();
               // fetch *all* configs currently applied to the device
               m_motor.getConfigurator().refresh(fx_cfg);

         .. tab-item:: C++
            :sync: C++

            .. code-block:: cpp

               configs::TalonFXConfiguration fx_cfg{};
               // fetch *all* configs currently applied to the device
               m_motor.GetConfigurator().Refresh(fx_cfg);
