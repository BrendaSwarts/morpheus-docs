RabbitMQ Cluster
^^^^^^^^^^^^^^^^^

An HA deployment will also include a Highly Available RabbitMQ.  This can be achieved through RabbitMQ's HA-Mirrored Queues on at least 3, independent nodes.  To accomplish this we recommend following Pivotal's documentation on RabbitMQ here: https://www.rabbitmq.com/ha.html and https://www.rabbitmq.com/clustering.html

Install RabbitMQ on the 3 nodes and create a cluster.

.. NOTE:: For the most up to date RPM package we recommend using this link: https://www.rabbitmq.com/install-rpm.html#downloads

.. IMPORTANT:: Morpheus connects to AMQP over 5672 or 5671(SSL) and 61613 or 61614(SSL)

RabbitMQ Installation and Configuration
````````````````````````````````````````

.. IMPORTANT:: This is a sample configuration only. Customer configurations and requirements will vary.

Prerequisites
..............

.. code-block:: bash

   yum install epel-release
   yum install erlang

Install RabbitMQ on the 3 nodes
.................................

.. code-block:: bash

   wget https://dl.bintray.com/rabbitmq/rabbitmq-server-rpm/rabbitmq-server-3.6.12-1.el7.noarch.rpm

   rpm --import https://www.rabbitmq.com/rabbitmq-release-signing-key.asc

   yum -y install rabbitmq-server-3.6.12-1.el7.noarch.rpm

   chkconfig rabbitmq-server on

   rabbitmq-server -detached

On Node 1:
>>>>>>>>>>>

.. code-block:: bash

  cat /var/lib/rabbitmq/.erlang.cookie

Copy this value

On Nodes 2 & 3:
>>>>>>>>>>>>>>>

#. Overwrite ``/var/lib/rabbitmq/.erlang.cookie`` with value from previous step and change its permissions using the follow commands.

   .. code-block:: bash

      chown rabbitmq:rabbitmq /var/lib/rabbitmq/*
      chmod 400 /var/lib/rabbitmq/.erlang.cookie


#. edit ``/etc/hosts`` file to refer to shortname of node 1

   example:

   .. code-block:: bash

    10.30.20.100 rabbit-1

#. Run the commands to join each node to the cluster

   .. code-block:: bash

      rabbitmqctl stop
      rabbitmq-server -detached
      rabbitmqctl stop_app
      rabbitmqctl join_cluster rabbit@<<node 1 shortname>>
      rabbitmqctl start_app

On Node 1
>>>>>>>>>>

.. code-block:: bash

   rabbitmqctl add_user <<admin username>> <<password>>
   rabbitmqctl set_permissions -p / <<admin username>> ".*" ".*" ".*"
   rabbitmqctl set_user_tags <<admin username>> administrator

On All Nodes:
>>>>>>>>>>>>>

.. code-block:: bash

   rabbitmq-plugins enable rabbitmq_stomp

Recommended Rabbitmq Policies:
```````````````````````````````

.. code-block:: bash

   rabbitmqctl set_policy -p morpheus --apply-to queues --priority 2 statCommands "statCommands.*" '{"expires":1800000, "ha-mode":"all"}'
   rabbitmqctl set_policy -p morpheus --apply-to queues --priority 2 morpheusAgentActions "morpheusAgentActions.*" '{"expires":1800000, "ha-mode":"all"}'
   rabbitmqctl set_policy -p morpheus --apply-to all --priority 1 ha ".*" '{"ha-mode":"all"}'
