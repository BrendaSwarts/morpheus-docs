Nutanix
-------

Overview
^^^^^^^^^

Nutanix simplifies datacenter infrastructure by integrating server and storage resources allowing applications to run at scale. |morpheus| provides and avenue to enhance the Nutanix resources to allow efficient and seamless deployment of applications as a virtual machine (VM) or as a container on a Docker host.

Features
^^^^^^^^^

* Virtual Machine Provisioning
* Containers
* Backups / Snapshots
* Resources Groups
* Migrations
* Auto Scaling
* Load Balancing
* Remote Console
* Periodic Synchronization
* Lifecycle Management and Resize

|morpheus| can provide a single pane of glass and self-service portal for managing multiple Nutanix Clusters and allowing the seamless deployment of applications.

.. Note:: Prism Central is not currently supported

Getting Started
^^^^^^^^^^^^^^^^

To get started this a few prerequisites must first be met.  The Nutanix cluster should be provisioned and available on the network. |morpheus| will look login to the Nutanix cluster with the Nutanix admin credentials and is typically located at the https://fqdn:9440 url.

Adding a Nutanix Cloud
^^^^^^^^^^^^^^^^^^^^^^^

The Nutanix cluster should be available and responding to the https://fqdn:9440 url for authentication by |morpheus| .

API URL
  example: https://10.30.21.220:9440
USERNAME
  Nutanix admin username
PASSWORD
  Nutanix admin password
Inventory Existing Instances
  If enabled, existing Virtual Machines will be inventoried and appear as unmanaged Virtual Machines in |morpheus| .

.. include:: /integration_guides/advanced_options.rst

Service Plans
^^^^^^^^^^^^^^

A default set of Service Plans are created in |morpheus| for the VMware provisioning engine. These Service Plans can be considered akin to AWS Flavors or Openstack Flavors. They provide a means to set predefined tiers on memory, storage, cores, and cpu. Price tables can also be applied to these so estimated cost per virtual machine can be tracked as well as pricing for customers. By default, these options are fixed sizes but can be configured for dynamic sizing. A service plan can be configured to allow a custom user entry for memory, storage, or cpu. To configure this, simply edit an existing Service Plan tied to Nutanix or create a new one. These all can be easily managed from the Admin | Service Plans & Pricing section.

Docker
^^^^^^^

So far this document has covered how to add the Nutanix cloud integration and has enabled users the ability to provision virtual machine based instances via the Add Instance catalog in Provisioning. Another great feature provided by |morpheus| out of the box is the ability to use Docker containers and even support multiple containers per Docker host. To do this a Docker Host must first be provisioned into Nutanix (multiple are needed when dealing with horizontal scaling scenarios).

To provision a Docker Host simply navigate to the Cloud detail page or Infrastructure Hosts section. From there click the + Container Host button to add a Nutanix Docker Host. |morpheus| views a Docker host just like any other Hypervisor with the caveat being that it is used for running containerized images instead of virtualized ones. Once a Docker Host is successfully provisioned a green checkmark will appear to the right of the host marking it as available for use. In the event of a failure click into the relevant host that failed and an error explaining the failure will be displayed in red at the top.

Some common error scenarios include network connectivity. For a Docker Host to function properly, it must be able to resolve the |morpheus| appliance url which can be configured in Admin Settings. If it is unable to resolve and negotiate with the appliance than the agent installation will fail and provisioning instructions will not be able to be issued to the host.
