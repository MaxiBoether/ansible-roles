some Ansible roles
==================

This repository contains Ansible roles.

The roles cover most of my administrative tasks and configurations
(which have to be fulfilled/applied more than once).

The roles are developed mainly for Debian(-based) systems. So
Debian-based might also work or, at least, almost work. Other
distributions probably won't work.

The roles are intended to be somewhat reusable,
but please do not apply them blindly.
Make sure you read and understand a role before running it.
Otherwise, you'll possibly loose something you love.

If you run these roles, have recent backups.

Feel free to read/try/use/extend them
and to contact me if you have any questions.

The most intensively developed, used and maintained role is
``managed_host``, which tries to generically configure and harden
heterogeneously configured systems (i.e. "snowflake" systems).

You (should) find README files in the roles' directories.
There are also `a few random notes on (intended) conventions
<conventions.rst>`__.

configuration variables
-----------------------

Some configuration points are provided via the roles' variables;
please see the roles' ``defaults/main.yml``.
Of course, you can override the roles' defaults.

We sometimes provide ``<variable name>_extra`` which will be considered
*in addition to* ``<variable name>`` (e.g., lists are extended,
dictionaries are merged, etc.). PRs welcome where ``<variable
name>_extra`` is not implemented yet.

Alternatively, you can use the Ansible configuration ``hash_behaviour =
merge`` to achieve merging of dictionaries "globally", e.g., where
``<variable name>_extra`` is not implemented yet.

links
-----

Further configuration files – which are not used by these roles — are
kept at `gitlab.com/lpirl/dotfiles
<https://gitlab.com/lpirl/dotfiles>`__.
