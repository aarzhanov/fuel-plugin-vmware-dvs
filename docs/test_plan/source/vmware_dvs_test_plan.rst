=============================================
Test Plan for VMware DVS plugin version 3.1.1
=============================================

************
Introduction
************

Purpose
=======

The main purpose of this document is to describe Quality Assurance activities
required to ensure that the Fuel plugin for Neutron ML2 vmware_dvs driver
is ready for production. The project will be able to offer VMware DVS
integration functionality with MOS.

The scope of this plan defines the following objectives:

* Identify testing activities;
* Outline testing approach, test types, test cycle that will be used;
* List of metrics and deliverable elements;
* List of items for testing and out of testing scope;
* Detect exit criteria in testing purposes;
* Describe test environment.

Scope
=====

The Fuel VMware DVS plugin includes Neutron ML2 Driver For VMware vCenter DVS
which is developed by third party. This test plan covers the full functionality
of Fuel VMware DVS plugin, includes basic scenarios related to the DVS driver
for Neutron.

The following test types should be provided:

* Smoke/BVT tests
* Integration tests
* System tests
* Destructive tests
* GUI tests

Performance testing will be executed on the scale lab and a custom set of rally
scenarios must be run with the DVS environment. The configuration, environment,
and scenarios for performance/scale testing must be determined separately.

Intended Audience
=================

This document is intended for project team staff (QA and Dev engineers and
managers) and all other persons who are interested in testing results.

Limitation
==========

The plugin (or its components) has the following limitations:

* VMware DVS plugin can be enabled only in environments with Neutron as a networking option
* Only VLANs are supported for tenant network separation.
* Only vSphere 5.5 & 6.0 are supported.

Product compatibility matrix
============================

.. list-table:: product compatibility matrix
   :widths: 15 10 30
   :header-rows: 1

   * - Requirement
     - Version
     - Comment
   * - MOS
     - 9.2 with Mitaka
     -
   * - Operating System
     - Ubuntu 14.04
     -
   * - vSphere
     - 5.5, 6.0
     -

Test environment, infrastructure and tools
==========================================

The following configuration should be used in the testing:

* 1 physnet to 1 DVS switch (dvSwitch).

Other recommendation are in the test cases.

**************************************
Evaluation Mission and Test Motivation
**************************************

The main goal of the project is to build a MOS plugin that integrates
the Neutron ML2 Driver For VMware vCenter DVS. This will allow to use Neutron
for networking in VMware-related environments. The plugin must be compatible
with the version 9.2 of Mirantis OpenStack and should be tested with the
software/hardware described in `product compatibility matrix`_.

See the VMware DVS Plugin specification for more details.

Evaluation mission
==================

* Find pressing issues with the integration of Neutron ML2 driver for DVS.
* Verify the specification.
* Provide tests for the maintenance update.
* Lab environment deployment.
* Deploy MOS with the developed plugin installed.
* Create and run specific tests for plugin/deployment.
* Verify the documentation.

*****************
Target Test Items
*****************

* Install/uninstall Fuel Vmware-DVS plugin
* Deploy Cluster with Fuel Vmware-DVS plugin by Fuel
    * Roles of nodes
        * Controller
        * Compute
        * Cinder
        * Mongo
        * Compute-VMware
        * Cinder-VMware
    * Hypervisors:
        * KVM + vCenter
        * Qemu + vCenter
    * Storage:
        * Ceph
        * Cinder
        * VMWare vCenter/ESXi datastore for images
    * Network
        * Neutron with VLAN segmentation
        * HA + Neutron with VLAN
    * Additional components
        * Ceilometer
        * Health Check
    * Upgrade master node
* MOS and VMware-DVS plugin
    * Computes (Nova)
        * Launch and manage instances
        * Launch instances in batch
    * Networks (Neutron)
        * Create and manage public and private networks
        * Create and manage routers
        * Port binding / disabling
        * Port security
        * Security groups
        * Assign vNIC to a VM
        * Connection between instances
    * Heat
        * Create stack from template
        * Delete stack
    * Keystone
        * Create and manage roles
    * Horizon
        * Create and manage projects
        * Create and manage users
    * Glance
        * Create and manage images
* GUI
    * Fuel UI
* CLI
    * Fuel CLI

*************
Test approach
*************

The project test approach consists of Smoke, Integration, System, Regression
Failover and Acceptance test levels.

**Smoke testing**

The goal of smoke testing is to ensure that the most critical features of Fuel
VMware DVS plugin work after new build delivery. Smoke tests will be used by
QA to accept software builds from Development team.

**Integration and System testing**

The goal of integration and system testing is to ensure that new or modified
components of Fuel and MOS work effectively with Fuel VMware DVS plugin
without gaps in dataflow.

**Regression testing**

The goal of regression testing is to verify that key features of Fuel VMware
DVS plugin are not affected by any changes performed during preparation to
release (includes defects fixing, new features introduction and possible
updates).

**Failover testing**

Failover and recovery testing ensures that the target-of-test can successfully
failover and recover from a variety of hardware, software, or network
malfunctions with undue loss of data or data integrity.

**Acceptance testing**

The goal of acceptance testing is to ensure that Fuel VMware DVS plugin has
reached a level of stability that meets requirements and acceptance criteria.


***********************
Entry and exit criteria
***********************

Criteria for test process starting
==================================

Before test process can be started it is needed to make some preparation
actions - to execute important preconditions. The following steps must be
executed successfully for starting test phase:

* all project requirements are reviewed and confirmed;
* implementation of testing features has finished (a new build is ready for testing);
* implementation code is stored in GIT;
* test environment is prepared with correct configuration, installed all needed software, hardware;
* test environment contains the latest delivered build for testing;
* test plan is ready and confirmed internally;
* implementation of manual tests and autotests (if any) has finished.

Feature exit criteria
=====================

Testing of a feature can be finished when:

* All planned tests (prepared before) for the feature are executed; no defects are found during this run;
* All planned tests for the feature are executed; defects found during this run are verified or confirmed to be acceptable (known issues);
* The time for testing of that feature according to the project plan has run out and Project Manager confirms that no changes to the schedule are possible.

Suspension and resumption criteria
==================================

Testing of a particular feature is suspended if there is a blocking issue
which prevents tests execution. Blocking issue can be one of the following:

* Testing environment for the feature is not ready
* Testing environment is unavailable due to failure
* Feature has a blocking defect, which prevents further usage of this feature and there is no workaround available

************
Deliverables
************

List of deliverables
====================

Project testing activities are to be resulted in the following reporting documents:

* Test plan
* Test report
* Automated test cases

Acceptance criteria
===================

* All acceptance criteria for user stories are met
* All test cases are executed. BVT tests are passed
* Critical and high issues are fixed
* All required documents are delivered
* Release notes including a report on the known errors of that release

**********
Test cases
**********

.. include:: test_suite_smoke.rst
.. include:: test_suite_system.rst
.. include:: test_suite_failover.rst
