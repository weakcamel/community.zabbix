==============================
community.zabbix Release Notes
==============================

.. contents:: Topics


v1.1.0
======

Release Summary
---------------

| Release date: 2020-10-22


Minor Changes
-------------

- all roles - added ``zabbix_{agent,web,server,proxy,javagateway}_conf_mode`` option for configuring a mode of the configuration file for each Zabbix service.
- zabbix_proxy (role) - added an option ``innodb_default_row_format`` for MariaDB/MySQL if it isn't set to ``dynamic``.
- zabbix_server - fixed installation output when using MySQL database to not print PostgreSQL.
- zabbix_user - ``passwd`` no longer required when ALL groups in ``usrgrps`` use LDAP as ``gui_access`` (see `#240 <https://github.com/ansible-collections/community.zabbix/issues/232>`_).
- zabbix_user - no longer requires ``usrgrps`` when ``state=absent`` (see `#240 <https://github.com/ansible-collections/community.zabbix/issues/232>`_).
- zabbix_web - added several configuration options for the PHP-FPM setup to configure the listen (socket) file.
- zabbix_web - added support for configuring Zabbix Web with Nginx, same way as with Apache.

Bugfixes
--------

- all roles - missing ``become`` set to ``true`` was added to each task that requires admin privleges.
- zabbix_agent - added new properties and updated documentation to allow for correct Zabbix Agent2 configuration.
- zabbix_agent - fixed bug where Nginx prevented Apache from working as it was part of the FPM configuration.

v1.0.0
======

Release Summary
---------------

| Release date: 2020-08-16


Minor Changes
-------------

- Added the possibility to configure the ``mode`` for the ``zabbix_{agent,server,proxy}_include`` directories.
- all roles - added the possibility to configure the ``mode`` for the ``yum`` repositories files in case it contains credentials.
- zabbix_agent - ``zabbix-sender`` and ``zabbix-get`` will not be installed when ``zabbix_repo`` is set to ``epel``, as they are not part of the repository.
- zabbix_agent - added option to change between HTTP/HTTPS with ``zabbix_repo_yum_schema``.
- zabbix_agent - can also install the zabbix-agent2 application when ``zabbix_agent2`` is set to ``true``.
- zabbix_proxy (role) - a user and group are created on the host when ``zabbix_repo`` is set to ``epel``.
- zabbix_proxy (role) - now supports ``startpreprocessors`` setting and encryption when connecting to database (see `#164 <https://github.com/ansible-collections/community.zabbix/pull/164>`_).
- zabbix_server - a user and group are created on the host when ``zabbix_repo`` is set to ``epel``.
- zabbix_server - added option to change between HTTP/HTTPS with ``zabbix_repo_yum_schema``.
- zabbix_server - now supports ``startpreprocessors`` setting and encryption when connecting to database (see `#164 <https://github.com/ansible-collections/community.zabbix/pull/164>`_).
- zabbix_web - a property is added ``zabbix_web_doubleprecision`` which currently is set to ``false`` for default installations. For new installations this should be set to ``True``. For upgraded installations, please read database `upgrade notes <https://www.zabbix.com/documentation/current/manual/installation/upgrade_notes_500>`_ (Paragraph "Enabling extended range of numeric (float) values") before enabling this option.
- zabbix_web - added option to change between HTTP/HTTPS with ``zabbix_repo_yum_schema``.
- zabbix_web - don't remove the files that Zabbix will install during installation when you don't want to configure a virtual host configuration.

Breaking Changes / Porting Guide
--------------------------------

- zabbix_javagateway - options ``javagateway_pidfile``, ``javagateway_listenip``, ``javagateway_listenport`` and ``javagateway_startpollers`` renamed to ``zabbix_javagateway_xyz`` (see `UPGRADE.md <https://github.com/ansible-collections/community.zabbix/blob/main/docs/UPGRADE.md>`_).

Bugfixes
--------

- all roles - a ``handler`` is configured when ``zabbix_http(s)_proxy`` is defined which will remove the proxy line from the repository files. This results that execution of the roles are not idempotent anymore.
- zabbix_proxy (role) - ``StartPreprocessors`` only works with version 4.2 or higher. When a lower version is used, it will not be added to the configuration.
- zabbix_proxy (role) - only install the sql files that needs to be executed for when ``zabbix_repo`` is set to ``epel``.
- zabbix_server - ``StartPreprocessors`` only works with version 4.2 or higher. When a lower version is used, it will not be added to the configuration.
- zabbix_server - only install the sql files that needs to be executed for when ``zabbix_repo`` is set to ``epel``.

v0.3.0
======

Release Summary
---------------

| Release date: 2020-07-26


Minor Changes
-------------

- All roles now **support Zabbix 5.0** and by default install this version (see `#131 <https://github.com/ansible-collections/community.zabbix/pull/131>`_ and `#121 <https://github.com/ansible-collections/community.zabbix/pull/121>`_).
- Roles will now install gnupg on Debian OS family if not present.
- zabbix_action - no longer requires ``password`` and ``ssh_*key_file`` parameters at the same time for ``remote_command`` operations of type SSH.
- zabbix_action - parameter ``ssh_auth_type`` for SSH ``remote_command`` operation now correctly identifies which other parameters are required.
- zabbix_discovery_rule - refactoring module to use ``module_utils`` classes and functions, adjust return values on success, add documentation for return values.
- zabbix_discovery_rule - refactoring the module to remove unnecessary variables and fix a variable typo.
- zabbix_mediatype - new options ``message_templates``, ``description`` and many more related to ``type=webhook``.
- zabbix_mediatype - now supports new ``webhook`` media type.

Bugfixes
--------

- zabbix_action - choices for the ``inventory`` paramter sub option in ``*operations`` arguments have been clarified to ``manual`` and ``automatic``.
- zabbix_action - fixed error on changed API fields ``*default_message`` and ``*default_subject`` for Zabbix 5.0 (see `#92 <https://github.com/ansible-collections/community.zabbix/pull/92>`_).
- zabbix_action - module will no longer fail when searching for global script provided to ``script_name`` parameter.
- zabbix_action - now correctly selects mediatype for the (normal|recovery|update) operations with Zabbix 4.4 and newer.
- zabbix_agent - fixed installation of agent on Windows to directories with spaces.
- zabbix_agent - role should no longer fail when looking for ``getenforce`` binary.
- zabbix_host - module will no longer convert context part of user macro to upper case.
- zabbix_proxy (role) - will now correctly install python3-libsemanage on RHEL OS family.
- zabbix_service - fixed the zabbix_service has no idempotency with Zabbix 5.0.
- zabbix_web - now no longer fails when rendering apache vhost template.

New Modules
-----------

- community.zabbix.zabbix_discovery_rule - Manage Zabbix discovery rules
- community.zabbix.zabbix_usergroup - Manage Zabbix user groups

v0.2.0
======

Release Summary
---------------

| Release date: 2020-06-15 

Minor Changes
-------------

- Documentation for roles moved to ``docs/`` sub-directory in the collection.
- New **role zabbix_agent** - previously known as dj-wasabi/zabbix-agent (also see `UPGRADE.md <https://github.com/ansible-collections/community.zabbix/blob/main/docs/UPGRADE.md>`_ for each role).
- New **role zabbix_javagateway** - previously known as dj-wasabi/zabbix-javagateway.
- New **role zabbix_proxy** - previously known as dj-wasabi/zabbix-proxy.
- New **role zabbix_server** - previously known as dj-wasabi/zabbix-server.
- New **role zabbix_web** - previously known as dj-wasabi/zabbix-web.
- zabbix_action - new alias ``update_operations`` for ``acknowledge_operations`` parameter.
- zabbix_host - ``macros`` now support new macro types ``text`` and ``secret``.
- zabbix_host - new option ``details`` (additional SNMP details) for ``interfaces`` parameter.
- zabbix_host - now supports Zabbix 5.0.
- zabbix_proxy (module) - now supports Zabbix 5.0.
- zabbix_screen - ``host_group`` parameter now accepts multiple groups.

Bugfixes
--------

- zabbix_action - documented ``value2`` parameter and ``notify_all_involved`` option.
- zabbix_maintenance - changing value of ``description`` parameter now actually updates maintenance's description.
- zabbix_template - is now able to perform ``state=dump`` when using ``ansible-playbook --check``.
- zabbix_template - no longer imports template from ``template_json`` or ``template_xml`` when using ``ansible-playbook --check``.

v0.1.0
======

Release Summary
---------------

| Release date: 2020-06-15


Minor Changes
-------------

- zabbix inventory plugin now no longer prints DeprecationWarning when used with Python3 due to SafeConfigParser.
- zabbix_action - arguments ``event_source`` and ``esc_period`` no longer required when ``state=absent``.
- zabbix_host - fixed inventory_mode key error, which occurs with Zabbix 4.4.1 or more (see `#65304 <https://github.com/ansible/ansible/issues/65304>`_).
- zabbix_host - was not possible to update a host where visible_name was not set in zabbix.
- zabbix_mediatype - Fixed to support zabbix 4.4 or more and python3 (see `#67693 <https://github.com/ansible/ansible/pull/67693>`_).
- zabbix_template - fixed error when providing empty ``link_templates`` to the module (see `#66417 <https://github.com/ansible/ansible/issues/66417>`_).
- zabbix_template - fixed invalid (non-importable) output provided by exporting XML (see `#66466 <https://github.com/ansible/ansible/issues/66466>`_).
- zabbix_user - Fixed an issue where module failed with zabbix 4.4 or above (see `#67475 <https://github.com/ansible/ansible/pull/67475>`_).

Deprecated Features
-------------------

- zabbix_proxy (module) - deprecates ``interface`` sub-options ``type`` and ``main`` when proxy type is set to passive via ``status=passive``. Make sure these suboptions are removed from your playbook as they were never supported by Zabbix in the first place.

Bugfixes
--------

- zabbix_action - allow str values for ``esc_period`` options (see `#66841 <https://github.com/ansible/ansible/pull/66841>`_).
- zabbix_action - no longer requires ``esc_period`` and ``event_source`` arguments when ``state=absent``.
- zabbix_host - now supports configuring user macros and host tags on the managed host (see `#66777 <https://github.com/ansible/ansible/pull/66777>`_).
- zabbix_host_info - ``host_name`` based search results now include host groups.
- zabbix_hostmacro - ``macro_name`` now accepts macros in zabbix native format as well (e.g. ``{$MACRO}``).
- zabbix_hostmacro - ``macro_value`` is no longer required when ``state=absent``.
- zabbix_proxy (module) - ``interface`` sub-options ``type`` and ``main`` are now deprecated and will be removed in community.general 3.0.0. Also, the values passed to ``interface`` are now checked for correct types and unexpected keys.
- zabbix_proxy (module) - added option proxy_address for comma-delimited list of IP/CIDR addresses or DNS names to accept active proxy requests from.
- zabbix_template - add new option omit_date to remove date from exported/dumped template (see `#67302 <https://github.com/ansible/ansible/pull/67302>`_).
- zabbix_template - adding new update rule templateLinkage.deleteMissing for newer zabbix versions (see `#66747 <https://github.com/ansible/ansible/pull/66747>`_).
- zabbix_template_info - add new option omit_date to remove date from exported/dumped template (see `#67302 <https://github.com/ansible/ansible/pull/67302>`_).
