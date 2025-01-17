Azure
-----

Overview
^^^^^^^^^

Azure is Microsoft's public cloud offering. Offering a full range of services and features across the globe in various datacenters. It is the equivalent of AWS for Microsoft running primarily on the Hyper-V based hypervisor. While it is a great public cloud offering, it can be somewhat difficult to get integrated with which is what this guide aims to cover.

Features
^^^^^^^^^

* Virtual Machine Provisioning
* Azure SQL Database
* Backups / Snapshots
* Resource Group Sync & Selection
* Network Sync & Selection
* Security Group Sync & Selection
* Storage Account Sync & Selection
* Marketplace Search and Provisioning
* Azure Marketplace Custom Library Item Support
* Remote Console
* Periodic Synchronization
* Lifecycle Management and Resize
* Availability Set Support
* Azure Load Balancers
* Azure Storage
* Docker Host Provisioning & Management
* Service Plan Sync
* Pricing Sync with markup options
* Cost Estimator

Combine these features with on premise solutions like Azure-Stack and |morpheus| can provide a single pane of glass and self service portal for managing instances scattered across both public Azure and private Azure Stack offerings.

.. NOTE:: |morpheus| even supports integrating with CSP based accounts in Azure (typically used by managed service providers).

Requirements
^^^^^^^^^^^^^

* Azure Active Directory Application & Credentials

  * Client ID (old portal) / Application ID (new portal)
  * Client Secret (old portal) / Key Value (new portal)
  * Tenant ID (old Portal) / Directory ID (new portal)
  * Azure Subscription ID

* Above Active Directory App added as owner of this Azure Subscription
* Existing Azure Resources

  * Network Security Group(s)
    * Typical Inbound ports open from |morpheus| Appliance: 22, 5985, 3389

    * Typical Outbound to |morpheus| Appliance: 80, 443

      * These are required for |morpheus| agent install, communication, and remote console access for windows and linux. Other configurations, such as docker instances, will need the appropriate ports opened as well.

  * Virtual Network(s)

    * Public IP assignment required for instances if |morpheus| Appliance is not able to communicate with Azure instances private ip's.

  * Resource Group(s)
  * Storage Account(s)

.. NOTE:: |morpheus| v2.10.3 added support for multiple Resource Groups and Storage Accounts per cloud, making our Azure integration more capable and easier to configure. Prior versions of |morpheus| supported one resource group and one storage account per cloud, with the security group and network selection limited to the scoped Resource Group. If you are on an earlier version of |morpheus| , please note you will need to add an Azure cloud integration for each Resource Group and Storage Account you would like to use.

Azure Active Directory Credentials
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

If you do not already have the Azure Active Directory credentials required to add an Azure cloud to |morpheus| , use the steps below to obtain them.

.. IMPORTANT:: Microsoft recently added support for Active Directory application configuration in the new Azure portal. Previously, users had to use the old portal to get the required credentials to integrate Azure with |morpheus| . The instructions below are updated for the new portal. Microsoft also changed the naming conventions of the credentials:


.. csv-table:: Old and New Portal Naming Conventions:
   :header: Old Azure Portal Name, New Azure Portal Name
   :widths: 100, 100

   "Tenant ID", "Directory ID"
   "Client ID", "Application ID"

Creating an Azure Active Directory Application
'''''''''''''''''''''''''''''''''''''''''''''''

If you do not have an existing Azure Active Directory application for |morpheus| , you will need to create a new on by:

#. Log into the Azure portal
#. Select "Azure Active Directory"
#. Select "App Registrations"
#. Select "New Application Registration"

   .. image:: /images/azure/newazure-f3af4.png

#. Next, give your new AD app a name, specify Web app / API for the type (default) and enter any url for the Sign-on URL:

   .. image:: /images/azure/newazure-8c7ca.png

#. Click Create and your new Azure Active Directory Application will be created.

   .. image:: /images/azure/newazure-f4e2d.png

Now that we have (or already had) our AD app, we will gather the credentials required for the |morpheus| Azure integration.

Tenant ID/Directory ID
'''''''''''''''''''''''

While still in the Active Directory Section:

#. Select Properties
#. Copy the Directory ID
#. Store/Paste for use as the Tenant ID when Adding your Azure cloud in |morpheus|

   .. image:: /images/azure/newazure-044cf.png

Client ID/Application ID
'''''''''''''''''''''''''

#. Select App Registrations
#. Select your Active Directory Application
#. Copy the Application ID
#. Store/Paste for use as the Client ID when Adding your Azure cloud in |morpheus|

   .. image:: /images/azure/newazure-3c6fa.png

Client Secret/Key Value
''''''''''''''''''''''''

While still in your Active Directory Application:

#. Select Keys in the Settings pane
#. Enter a name for the key
#. Select a duration
#. Select save
#. Copy the Key Value
#. Store/Paste for use as the Client Secret when Adding your Azure cloud in |morpheus|

   .. IMPORTANT:: Copy the key value. You won't be able to retrieve after you leave this blade.

   .. image:: /images/azure/newazure-7b82b.png

You now have the 3 Active directory credentials required for |morpheus| Azure cloud integration.

Subscription ID
''''''''''''''''

The last credential required for the |morpheus| Azure cloud integration is the Azure Subscription ID

#. Select Resource Groups
#. Select a Resource Group (instruction below if you do not have an existing resource group)
#. Copy the Subscription ID
#. Store/Paste for use as the Subscription ID when Adding your Azure cloud in |morpheus|

   .. image:: /images/azure/newazure-e446f.png

Make Azure Active Directory Application owner of Subscription
'''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''

The Active Directory Application used needs to be an owner of the subscription used for the Azure |morpheus| cloud integration.

#. In the Subscription pane, select "Access Control (IAM)"

   .. image:: /images/azure/newazure-bd9f1.png

#. Click "+ Add", in the pane to the right, select "1 Select a role" and then select "Owner"

   .. image:: /images/azure/newazure-cfd51.png

#. Select "2. Add Users" and in the search box begin to type the name of the AD Application created earlier.

   .. NOTE:: the AD Application will not display by default and must be searched for.

   .. image:: /images/azure/newazure-7f61c.png

#. Select the Application, then click "Select" at the bottom of the Add Users pane, and the select "OK" at the bottom of the Add Access pane.

   .. IMPORTANT:: Be sure to select "OK" at the bottom of the Add Access pane or the user addition will not save.

   .. image:: /images/azure/newazure-560be.png

You now have the required Credentials to add an Azure cloud integration into |morpheus| .

.. IMPORTANT:: You will also need to have existing Network Security Group(s), Virtual Networks(s) and Storage Accounts(s). Instructions for creating these can be found later in this article.

Add Azure cloud in |morpheus|
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Azure is now ready to be added into |morpheus| . Ensure you have the noted Subscription ID, Tenant ID, Client ID, and Client Secret accessible.

#. In Infrastructure - Clouds, select :guilabel:`+ CREATE CLOUD` and select Azure from the cloud widget.

   OR

#. In Infrastructure, Groups- you can select the Clouds tab of a Group and click :guilabel:`+ ADD` next to Azure in the Public Cloud section

#. Enter the following:

   * Name
   * Location (optional)
   * Domain (if not localdomain)
   * Scale Priority
   * Subscription ID (from step 18)
   * Tenant ID (from step 16)
   * Client ID (from step 13)
   * Client Secret (from step 13)

   If everything is entered correctly, the Location dropdown will populate.

#. Select the Location/Region to scope the cloud to (additional Clouds can be added for multiple regions)
#. Select All or specify a Resource Group to scope this cloud to
#. Optionally select "Inventory Existing Instances" (This will inventory your existing vm's in Azure and list them in |morpheus| as unmanaged instances.)
#. Click :guilabel:`+ Save Changes`

   .. image:: /images/azure/newazure-5f512.png

Your Azure Cloud will be created.

   .. image:: /images/azure/newazure-2a7fe.png

Creating Resources in Azure
^^^^^^^^^^^^^^^^^^^^^^^^^^^

If you do not have existing Network Security Groups, Virtual Networks, or Storage Accounts, you can create them by following the steps below:

Create a Network Security Group
'''''''''''''''''''''''''''''''

#. In the main Azure toolbar, select the right arrow at the bottom of the toolbar (if collapsed) and search for and select Network Security Groups.

   .. image:: /images/azure/newazure-83506.png

#. Click "+ Add" at the top of the Network security groups pane

   .. image:: /images/azure/newazure-3357f.png

#. Enter a unique name for the security group, select the correct subscription, and either select the resource group being used, or create a new one as shown below. Also verify the Location is the same, and then click "Create" at the bottom of the pane.

   .. image:: /images/azure/newazure-7c098.png

#. Configure inbound and outbound rules for the security group. Ports 80 (http), 443 (https) 22 (ssh) and 5985 (winrm) need to be open to and from the |morpheus| appliance.

Create a Virtual Network
'''''''''''''''''''''''''

#. In the main Azure toolbar, select the right arrow at the bottom of the toolbar (if collapsed) and search for and select Virtual Networks.

   .. image:: /images/azure/newazure-7ecb2.png

#. Click "+ Add" at the top of the Virtual Networks pane

   .. image:: /images/azure/newazure-db3a5.png

#. Enter a unique name for the virtual network, the correct subscription, select "Use existing" and select the same resource group as the Network Security Group. Also verify the Location is the same, and then click "Create" at the bottom of the pane.

   .. image:: /images/azure/newazure-a3066.png

Create a Storage Account
'''''''''''''''''''''''''

#. In the main Azure toolbar, select the right arrow at the bottom of the toolbar (if collapsed) and search for and select Storage Accounts.

   .. image:: /images/azure/newazure-4429f.png

#. Click "+ Add" at the top of the Storage accounts pane

   .. image:: /images/azure/newazure-7947e.png

#. Enter a unique name for the storage account, select "Locally-redundant storage (LRS) for Replication, select the correct subscription, select "Use existing" and select the same resource group as the Network Security Group and Virtual Network. Also verify the Location is the same, and finally click "Create" at the bottom of the pane.

   .. image:: /images/azure/newazure-b89ea.png

Docker
^^^^^^

So far this document has covered how to add the Azure cloud integration and has enabled users the ability to provision virtual machine based instances via the Add Instance catalog in Provisioning. Another great feature provided by |morpheus| out of the box is the ability to use Docker containers and even support multiple containers per Docker host. To do this a Docker Host must first be provisioned into Azure (multiple are needed when dealing with horizontal scaling scenarios).

.. image:: /images/azure/newazure-7971d.png

To provision a Docker Host simply navigate to the Cloud detail page or Infrastructure?Hosts section. From there click the + Container Host button to add a Azure Docker Host. This host will show up in the Hosts tab. |morpheus| views a Docker host just like any other Hypervisor with the caveat being that it is used for running containerized images instead of virtualized ones. Once a Docker Host is successfully provisioned a green checkmark will appear to the right of the host marking it as available for use. In the event of a failure click into the relevant host that failed and an error explaining the failure will be displayed in red at the top.

Some common error scenarios include network connectivity. For a Docker Host to function properly, it must be able to resolve the |morpheus| appliance url which can be configured in Admin|Settings. If it is unable to resolve and negotiate with the appliance than the agent installation will fail and provisioning instructions will not be able to be issued to the host.

Multi-tenancy
^^^^^^^^^^^^^

A very common scenario for Managed Service Providers is the need to provide access to Azure resources on a customer by customer basis. With Azure several administrative features have been added to ensure customer resources are properly scoped and isolated. For Azure it is possible to assign specific Networks, and Resource Groups to customer accounts or even set the public visibility of certain resources, therefore allowing all sub accounts access to the resource.

.. include:: scalesets.rst
