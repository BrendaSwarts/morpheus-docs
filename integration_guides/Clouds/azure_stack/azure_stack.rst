Azure Stack
------------

Overview
^^^^^^^^^

Azure Stack is Microsoft's Azure Cloud for on-premises environments. Azure Stack contains the core Azure services, allowing organizations to take advantage of Azure's offerings with the security, compliance, and financial benefits of hosting it in their own data-centers.

* Virtual Machine Provisioning
* Backups / Snapshots
* Resource Group Sync & Selection
* Network Sync & Selection
* Security Group Sync & Selection
* Storage Account Sync & Selection
* Marketplace Search and Provisioning
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

Combine these features with public Azure and |morpheus| can provide a single pane of glass and self service portal for managing instances scattered across both Azure offerings.

Requirements
^^^^^^^^^^^^^

Azure Stack Accessibility
~~~~~~~~~~~~~~~~~~~~~~~~~

By default, the Azure Stack management url's are not accessible from an external network. Port mappings and DNS must be configured for communication between the |morpheus| Appliance and Azure Stack.

.. IMPORTANT:: In order to communicate with Azure Stack, |morpheus| must be able to reach the internal Azure Stack network. The Azure Stack Portal needs to be exposed to the |morpheus| Appliances' network with corresponding entries added to DNS.

One option to expose the Internal Azure Stack network to the |morpheus| Appliances' network is to use the 'Expose-AzureStackPortal.ps1' powershell script from https://gallery.technet.microsoft.com/scriptcenter/Expose-the-Azure-Stack-7ef68b19. An Azure Stack Port Mapping Tool is also available.

Below is a sample output from the script for reference:

.. code-block:: shell

        [Admin Portal] Created port mappings on 10.30.23.120 to 192.168.102.8
        [Admin Portal] Ports: 13011 30015 13001 13010 13021 13020 443 13003 12646 12647 12648 12649 12650 12495 13026 12499
        [Admin Portal] DNS: 10.30.23.120 - adminportal.local.azurestack.external adminmanagement.local.azurestack.external

        [Tenant Portal] Created port mappings on 10.30.23.121 to 192.168.102.10
        [Tenant Portal] Ports: 13011 30015 13001 13010 13021 13020 443 13003 12646 12647 12648 12649 12650 12495 13026 12499
        [Tenant Portal] DNS: 10.30.23.121 - portal.local.azurestack.external management.local.azurestack.external

        [Blob Storage] Created port mappings on 10.30.23.122 to 192.168.102.4
        [Blob Storage] Ports: 80 443
        [Blob Storage] DNS: 10.30.23.122  *.blob.local.azurestack.external

        VERBOSE: DNS delegation/forwarding is optional, change the DNS records on MAS-DC01 manually (dnsmgmt.msc from Host).
        [DNS Delegation] Created port mappings on 10.30.23.120 to 192.168.200.224
        [DNS Delegation] Ports: 53 (TCP/UDP)
        [DNS Delegation] DNS: local.azurestack.external NS 10.30.23.120
        [DNS Delegation] Change records on MAS-DC01 manually if you plan to use DNS forwarding.
        [DNS Delegation] Change records back to the original internal IPs before running this script again.

        VERBOSE: App Service detected and external IP's specified, creating mappings....
        [App Service API] Created port mappings on 10.30.23.123 to 192.168.102.17
        [App Service API] Ports: 443
        [App Service API] DNS: 10.30.23.123  api.appservice.local.azurestack.external
        [App Service Apps] Created port mappings on 10.30.23.124 to 192.168.102.15
        [App Service Apps] Ports: 80 443 21 990
        [App Service Apps] DNS: 10.30.23.124  *.appservice.local.azurestack.external


Azure Stack Resources
~~~~~~~~~~~~~~~~~~~~~

The following resources need to be created and configured inside Azure Stack for successful provisioning:

* Resource Group(s)
* Virtual Network(s)
* Storage Account(s)
* Network Security Group(s)

  * Inbound ports open from |morpheus| Appliance: 22, 5985, 3389
  * Outbound ports open to |morpheus| Appliance: 80, 443

.. NOTE:: Proper Network and Network Security Group configuration is required for |morpheus| agent install, communication, and remote console access. Other configurations, such as docker instances, will need the appropriate ports opened as well.

Required Credentials & Permissions
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Credentials to integrate |morpheus| with Azure Stack are located in both the public Azure Portal and the Private Azure Stack Portal. The Azure Active Directory Application used must be an owner of the Azure Stack subscription.

Azure Portal:
  * Azure Active Directory Application Credentials
  * Directory ID
  * Management URL
  * Identity Resource URL
  * Application ID
  * Key Value

Azure Stack Portal:
  * Azure Stack Subscription ID
  * Active Directory App from Azure portal added as owner of the Azure Stack Subscription in Azure Stack.


Adding an Azure Stack Cloud
^^^^^^^^^^^^^^^^^^^^^^^^^^^

Configure
~~~~~~~~~~

#. In the |morpheus| UI, navigate to ``Infrastructure -> Clouds`` and Select :guilabel:`+ CREATE CLOUD`
#. Select *AZURE STACK (PRIVATE)* from the Clouds list and select :guilabel:`NEXT`
#. In the Configure section, enter:

   NAME
    Internal name for the Cloud in |morpheus|
   LOCATION
    (Optional) Can be used to specify the location of the Cloud or add a description.
   VISIBILITY
    Determines Tenant visibility for the Cloud.
      * Private: Access to the Cloud is limited to the assigned Tenant (Master Tenant by default)
      * Public: Access to the Cloud can be configured for Tenants in their Tenant Role permissions.

   IDENTITY URL
    https://login.microsoftonline.com
   MANAGEMENT URL*
    Azure AD Azure Stack Administrator app or Microsoft Azure Stack Administrator app url. Example: https://adminmanagement.local.azurestack.external/
   IDENTITY RESOURCE URL
    Azure AD Azure Stack Administrator App ID URI Example: https://adminmanagement.xxxxxxx.onmicrosoft.com/4a80e607-4259-4ac6-83e2-2fabeaf2eh83
   BASE DOMAIN
    This should match the base domain in your Management url. Example: local.azurestack.external
   SUBSCRIPTION ID
    Subscription ID from Azure Stack portal (this is different from the Subscription ID in you Azure portal used when configuring Azure Stack)
   TENANT ID
    This is the Directory ID from the Azure AD directory
   CLIENT ID
    Application ID of Azure AD app with Azure Stack permissions granted, and has been added as an owner of the Azure Stack subscription (in the Azure Stack portal).
   CLIENT SECRET
    Key Value of Application ID used above

    .. note:: Once all credentials are entered and validated, the Location and Resource Group fields will populate.

   Location
    Select an Azure Stack region for the cloud to scope to. This typically will be "local".
   Resource Group
    Select All or a single Resource Group to scope the cloud to. Selecting a single Resource Group will only sync resources in that Resource Group and disable Resource Group selection during provisioning. All will sync all resources and allow specifying the Resource Group during provisioning.
   Inventory Existing Instances
    If enabled, existing Virtual Machines will be inventoried and appear as unmanaged Virtual Machines in |morpheus|.

#. The Azure Stack cloud is ready to be added to a group and saved. Additional configuration options available:

.. NOTE:: All fields and options can be edited after the Cloud is created.

Advanced Options
   DOMAIN
    Specify a default domain for instances provisioned to this Cloud.
   SCALE PRIORITY
    Specifies the priority with which an instance will scale into the cloud. A lower priority number means this cloud integration will take scale precedence over other cloud integrations in the group.
   APPLIANCE URL
    Alternate Appliance url for scenarios when the default Appliance URL (configured in `admin -> settings`) is not reachable or resolvable for Instances provisioned in this cloud. The Appliance URL is used for Agent install and reporting.
   TIME ZONE
    Configures the time zone on provisioned VM's if necessary.
   DATACENTER ID
    Used for differentiating pricing among multiple datacenters. Leave blank unless prices are properly configured.
   HYPER-CONVERGED ENABLED
    Not applicable for Azure Stack
   DNS INTEGRATION
    Records for instances provisioned in this cloud will be added to selected DNS integration.
   SERVICE REGISTRY
    Services for instances provisioned in this cloud will be added to selected Service Registry integration.
   CONFIG MANAGEMENT
    Select a Chef, Salt, Ansible or Puppet integration to be used with this Cloud.
   AGENT INSTALL MODE
    * SSH / WINRM: |morpheus| will use SSH or WINRM for Agent install.
    * Cloud-Init (when available): |morpheus| will utilize Cloud-Init or Cloudbase-Init for agent install when provisioning images with Cloud-Init/Cloudbase-Init installed. |morpheus| will fall back on SSH or WINRM if cloud-init is not installed on the provisioned image.

   API PROXY
    Required when a Proxy Server blocks communication between the |morpheus| Appliance and the Cloud. Proxies can be added in the `Infrastructure -> Networks -> Proxies` tab.

Provisioning Options
  API PROXY
    Required when a Proxy Server blocks communication between an Instance and the |morpheus| Appliance. Proxies can be added in the `Infrastructure -> Networks -> Proxies` tab.
  Bypass Proxy for Appliance URL
    Enable to bypass proxy settings (if added) for Instance Agent communication to the Appliance URL.
  USER DATA (LINUX)
    Add cloud-init user data using bash syntax.

Once all options are configured, select NEXT to add the cloud to a Group.

Group
~~~~~~

A Group must be specified or created for the new Cloud to be added to. Clouds can be added to additional Groups or removed from Groups after being created.

USE EXISTING
  Add the new Cloud to an exiting Group in |morpheus| .
CREATE NEW
  Creates a new Group in |morpheus| and adds the Cloud to the Group.

Review
~~~~~~~

Confirm all settings are correct and select COMPLETE. The Azure Stack Cloud will be added, and |morpheus| will perform the initial cloud sync of:

* Virtual Machines (if Inventory Existing Instances is enabled)
* Networks
* Virtual Images/Blueprints
* Network Security Groups
* Storage Accounts
* Marketplace Catalog
* Availability Sets

.. TIP:: Synced Networks can be configured or deactivated from the Networks section in this Clouds detail page, or in the `Infrastructure -> Networks` section.
