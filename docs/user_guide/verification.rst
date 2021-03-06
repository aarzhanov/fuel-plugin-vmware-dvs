Verify a deployed environment with VMware DVS plugin
----------------------------------------------------

After you deploy an environment with VMware DVS plugin, complete the
following verification steps:

#. Log in to a controller node.
#. Run the :command:`neutron agent-list` command to verify whether the
   DVS agent is present in the list of Neutron agents and is ready for use:

   * The ``alive`` column should contain the ``:-)`` value.
   * The ``admin_state_up`` column should contain the ``True`` value.

   .. code-block:: console

    $ neutron agent-list
    +----+-----------+-----------+------+---------------+-----------------+
    |id  |agent_type |host       |alive |admin_state_up |binary           |
    +----+-----------+-----------+----------------------+-----------------+
    |... |DVS agent  |vcenter-sn2|:-)   |True           |neutron-dvs-agent|
    +----+-----------+-----------+------+---------------+-----------------+

   .. note:: In the example above, the ``availability_zone`` column was
    removed from the output of the :command:`neutron agent-list` command.

#. Log in to the Fuel web UI.
#. Click the :guilabel:`Health Check` tab.
#. Run necessary health tests. For details, see:
   `Verify your OpenStack environment <http://docs.openstack.org/developer/fuel-docs/userdocs/fuel-user-guide/verify-environment.html>`_.
