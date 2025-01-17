Layouts
-------

.. image::

- Layouts are attached to Instance types. A Layout can only be attached to a single Instance Type and a single Technology Type.

- An Instance Type can have one or many Layouts attached to it, allowing for a single Instance Type to work with any Technology Type.

- Node Types are added to Layouts. A Layout can have one or many node types attached to it. Node types can be shared across Layouts of matching Technology Types.

.. important:: Once an Instance Type is defined on a Layout and saved, the Instance Type setting on the Layout cannot be changed.

Layout List view
^^^^^^^^^^^^^^^^

The Layout list view shows all available Instances Types including Name, Version, associated Instance Type and description.

- The Technology Filter will filter the displayed layouts by selected Technology.
- The Instance Type Filter will filter the displayed Layout by associated Instance Type.
- Layout Names link to the Layouts associated Layout Detail page.
- Instance Types link to the Layouts associated Layout Detail page.
- The pencil icon open the Edit Layout modal
- The Trash Can icon deletes the Layout.

  .. note:: A Layout that is in use cannot be deleted.

- Select :guilabel:`+ ADD` to add a new Layout. Layouts can also be created form an Instance Types detail page.

Layout Detail View
^^^^^^^^^^^^^^^^^^

The Layout Detail view shows details on the Layout and all associated Node Types.

- Select a Layout Name from the Layout list page or Instance Type Detail page to get to a Layout Detail page.


Layout Configuration Options
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Instance Type
  Select the Instance Type to add the new Layout to. Custom Instance Types must already be created and one layout cannot be added to multiple instance types, or change Instance Types after creation.

  .. NOTE:: Layouts cannot be added to System Instance Types.

Name
  The name the layout will present as in the Configuration Options dropdown in the provisioning wizard
Version
  The version number or name for the Layout. Layouts in an Instance Type with the same version will all show under the Configuration Options dropdown when that version in selected while provisioning.
Description
  Description of the layout, viewable on the Layout list tab.
Technology
  Technology determines which cloud this layout will be available for, and which Node Types can be added to it.
Minimum Memory
  Defines the Minimum amount of Memory required for this Layout. Only Service Plans that meet the defined Minimum Memory value will be available during Provisioning when this Layout is selected, and custom memory values must meet this minimum. 0 equals no Minimum Memory requirement. This Minimum Memory value will override any Virtual Image Minimum Memory requirements.
Workflow
  Select a Workflow to automatically run and be attached to associated Instances using this Layout. If a Workflow is defined, it is not presented in the Provisioning Wizard and is not user configurable.
Supports Convert to Managed
  Enabled to allow users to select this layout when converting a Discovered workload to managed.
Enable Scaling (Horizontal)
  Enables Instances with this layout to use Scaling features
Environment Variables
  Custom evars to be added to the instance when provisioned.
Option Types
  Search for and then select one or multiple Option Types to add to Layout. Option Type input fields (except for Hidden Option Types) will appear in Provisioning, App, Blueprint, and Cloning wizards when this layout is selected.
Nodes
  Single or multiple nodes can be added to a Layout by searching for and selecting the node(s). An example of a layout with multiple nodes is the Hyper-V MySQL Master/Slave layout pictured below (note this is the Layout detail screen after the layout has been created.)
