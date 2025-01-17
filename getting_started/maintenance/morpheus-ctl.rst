morpheus-ctl tips
=====================

``morpheus-ctl`` is useful beyond reconfigures and starting the ui, and many commands can be run across all services, or scoped to a singe service.

Some common commands include:

morpheus-ctl status
  This list all the installed services and their current Status
morpheus-ctl start (service)
  This starts all services if no service is specified, or starts the specified service. For example,

  - ``morpheus-ctl start/stop/restart/kill`` on an all-in-one appliance will start, stop, restart or kill mysql, elasticsearch, rabbitmq, check-server, redis, guacd and the morpheus-ui, one by one.
  - ``morpheus-ctl start/stop/restart/kill morpheus-ui`` will only start, stop, restart or kill the morpheus-ui service, leaving the other service in their current state.  Same goes for ``morpheus-ctl start/stop/restart/kill mysql``, ``morpheus-ctl start/stop/restart/kill elasticsearch`` etc.


``morpheus-ctl`` commands:

.. code-block:: bash

     General Commands:

       cleanse
         Delete *all* morpheus data, and start from scratch.
       help
         Print this help message.
       reconfigure
         Reconfigure the application.
       show-config
         Show the configuration that would be generated by reconfigure.
       uninstall
         Kill all processes and uninstall the process supervisor (data will be preserved).

      Service Management Commands:

        graceful-kill
          Attempt a graceful stop, then SIGKILL the entire process group.
        hup
          Send the services a HUP.
        int
          Send the services an INT.
        kill
          Send the services a KILL.
        once
          Start the services if they are down. Do not restart them if they stop.
        restart
          Stop the services if they are running, then start them again.
        service-list
          List all the services (enabled services appear with a *.)
        start
          Start services if they are down, and restart them if they stop.
        status
          Show the status of all the services.
        stop
          Stop the services, and do not restart them.
        tail
          Watch the service logs of all enabled services.
        term
          Send the services a TERM.

      Elasticsearch Commands:

        elastic-util
          Backup/Restore ElasticSearch data

      Firewall Commands:

        firewall-enable-blocking
          Enables firewall blocking mode.
