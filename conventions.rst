Basically, a note to myself: :)

general
=======

* do not use abbreviated YAML syntax

  * e.g., not: ``[foo, bar]``, ``package: name=foo state=present``

how to modify configurations
============================

* try to preserve the possibility to have local modifications
  (done manually on remote machine)
* try to make it transparent which files have been edited via Ansible

* if we can add our changes to a separate file
  (in directories like ``/etc/cron.d``)

  * prefer writing the file via ``blockinfile``

    * since it creates nice "managed by Ansible" markers by itself
    * instead of using the ``copy`` module
    * also, |mods| are still possible

      * by editing the file outside the block

    * # let's see if this is feasible

* if we *cannot* add our changes to a separate file
  (e.g. ``/etc/postfix/main.cf``)

  * prefer ``lineinfile``

    * since it can deal with pre-existing configurations
      (i.e., lines in the file)

      * and |mods| are still possible

    * hence, keep the (Ansible) configuration options in (a) map(s)

where to put configurations in the roles
========================================

In order of preference:

* configuration in a file in the ``files`` directory

  * if the file contents make sense on their own / if the
    configuration file is usable on its own

    * makes it easier for others to re-use the files
    * for, e.g., ``blockinfile``, load contents with
      ``{{ lookup('file', '/foo.txt') }}``

  * if file does not need any variables (wouldn't work)
  * use the same path in the ``files`` as on the remote
    (e.g.: remote ``/x/y.conf`` stored as ``files/x/y.conf``)

    * if possible
    * for transparency

* in variables

  * preferred
  * esp. the more individual the configuration is

* hard-coded in the task files

  * if invariant for the role

task scheduling
===============

* try to use systemd timers

  * profit from useful features

    * e.g., ``ConditionCapability``, ``Persistent``

  * it'll probably go in that direction anyway

* to defer tasks on battery, a separate, unified solution is required

  * i.e., do not include a solution to wait for AC in every timer/unit
    separately

    * since most systems do have permanent AC and it would be a waste
      of resources to run the checks anyway

  * maybe systemd override files which add ``ExecStartPre`` to wait
    for AC

become
======

* specify ``become: yes`` in the tasks and don't require users of the
  roles to specify ``become: yes`` globally on Play level

.. |mods| replace:: manual modifications on the remote machine
