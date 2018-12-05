.. _lab_manage_workloads:

------------------------
Lab - Managing Workloads
------------------------

Overview
++++++++

Get experience using VM management tasks from Prism, which include power actions, searching, cloning, and migrating.

Workload Management
+++++++++++++++++++

Now that you have a couple VMs deployed, let’s have some fun and explore some of the VM management tasks with AHV.

Power Actions and Console Access
................................

Explore VM power actions and console access.

In **Prism Element > VM > Table**.

Locate the Linux VM you created in the previous lab (Linux_VM-*initials*). (Use Prism’s search function if necessary)

.. note::

  Note that the Power State column for that VM shows a red dot, indicating that the VM is powered off.

Now lets power on the VM:

Select the VM, then click **Power On**.

Next lets open a console session:

Select the VM, then click **Launch Console**.

.. note::

  When the console window opens, note that there are four actions available in the console (Send Mount ISO, CTRL-ALT-DEL, Take Screen Capture, and Power).

.. figure:: images/manage_workloads_01.png

.. note::

  In ESX:

  - The steps in this exercise could also be done from Prism while using an ESXi cluster that has its VMware vCenter instance is registered to Prism.

  .. figure:: images/manage_workloads_06.png

Prism Search
............

The Prism search function makes it easier to identify problems or find feature documentation in Prism Central. Use Prism Central’s search capabilities by typing a few search queries to see how easy this can make the tasks above.


Suggestions:

- vm cpu > 1
- vm mem > 2
- vm iops
- create vm
- powered on
- powered on cpu = 8

In **Prism Central >** :fa:`search`.

- Note the result types: Entity, Alerts, and Help.
- Click the star icon to save a search.

.. note::

  The search hot key (a slash mark, or /) can be used from anywhere in the Prism Central UI to bring up the search function.

Clone a VM
..........

In **Prism Element > VM > Table**.

Find and make two clones of the Linux-*initials* virtual machine you created earlier.

Select the VM, then click **Clone** from the **Actions** drop-down menu.

Fill out the following fields and click **Save**:

- **Number of Clones** - 2
- **Prefix Name**  - Linux-*initials*-Clone
- **Starting Index Number** - 1

.. figure:: images/manage_workloads_02.png

Leave them **Powered Off**.

Migrate a VM Between Hosts
..........................

In **Prism Element > VM > Table**.

Locate the Linux VMs from the previous lab (Linux_VM-*initials*).

- Use Search with the Initials you used.

You should see that it has no entry in the **Host** column when it is powered off.

.. figure:: images/manage_workloads_03.png

Select the **Powered On** VM, then click **Migrate**.

You can either choose one of the other hosts in the cluster as a migration target for the VM, or accept the default and let AHV automatically select a location.

Click **Migrate** to finalize the action.

When the task completes, verify that your VM host location has changed from the host recorded above to the new location you selected.

.. figure:: images/manage_workloads_04.png

Configure VM-to-Host Affinity Policies
......................................

In **Prism Element > VM > Table**.

Locate the Linux VMs from the previous lab (Linux_VM-*initials*).

- Use Search with the Initials you used.

Select a **Powered OFF** VM, then click **Update** and **+ Set Affinity**.

Select two **Hosts** to which the VM can have affinity, and click **Save** and **Save** to finish.

.. note:: We select more then one host so the VM has a place to migrate too in the event of a Node failure.

Power On the VM, and verify it is on one of the **Hosts** you selected in the affinity policy.

Select the VM, then click **Migrate**.

You should see the following message:

- This VM has host affinity with 2 out of the 4 available hosts. It can only be migrated to those hosts.

Click **Migrate**.

You should see that the VM has moved to the other host.

High Availability
.................

High availability is enabled by default for AHV and will restart VMs in a best-effort manner in the event of a host failure. Additional configuration can set resource reservations to ensure there is capacity during an HA event.

VMware HA works by providing high availability for virtual machines by pooling the virtual machines and the hosts they reside on into a cluster. The hosts in that cluster are then monitored and in case there is a failure, the VMs residing on the failed host would get restarted on alternate hosts. This feature must be turned on in vSphere, as opposed to AHV where it’s on by default without reservation.

Takeaways
+++++++++

- In this lab you got to experience first hand how AHV provides a complete set of tools and actions that can be done manage the VMs in the cluster.
- It is possible to register an ESXI cluster to Prism and be able to perform some of the basic VM management tasks right from Prism as well.
