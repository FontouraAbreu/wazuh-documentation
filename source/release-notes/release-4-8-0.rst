.. Copyright (C) 2015, Wazuh, Inc.

.. meta::
  :description: Wazuh 4.8.0 has been released. Check out our release notes to discover the changes and additions of this release.

4.8.0 Release notes - 12 June 2024
==================================

This section lists the changes in version 4.8.0. Every update of the Wazuh solution is cumulative and includes all enhancements and fixes from previous releases.

Highlights
----------

This release introduces a major refactor of the Vulnerability Detector module that increases coverage and improves reliability by using a centralized feed of curated vulnerabilities maintained by Wazuh. It introduces global queries for vulnerability detection information, allowing users to search through vulnerability detection data across all endpoints.

The Wazuh dashboard notifies users whenever there's a newer Wazuh version available and offers a revamped UX navigation experience by completely overhauling the menu layout.

To support the centralized vulnerability feed and update check services, Wazuh has developed a new platform aimed at integrating and distributing Cyber Threat Intelligence (CTI) data.

Package inventory can now collect information from expanded sources, including the Snap package manager.

The release also addresses hundreds of bugs of varying impacts, further stabilizing the platform and improving the overall user experience.

-  `Vulnerability Detector refactor <https://github.com/wazuh/wazuh/issues/14153>`__: Vulnerability detection uses a centralized feed maintained by Wazuh and introduces global queries, significantly improving vulnerability detection capabilities and performance.
-  `Update check service UI <https://github.com/wazuh/wazuh-dashboard/issues/84>`__: Users can now be notified whenever there's a new Wazuh version available.
-  `Wazuh dashboard UX redesign <https://github.com/wazuh/wazuh-dashboard/issues/90>`__: A significant overhaul aimed at enhancing the user interface and experience, making navigation and operation more intuitive.
-  `Snap packages support <https://github.com/wazuh/wazuh/issues/15429>`__ & `PYPI and Node packages support <https://github.com/wazuh/wazuh-documentation/issues/6342>`__: Wazuh now includes support for inventorying packages installed through the Snap package manager, improving visibility into software management.

Breaking changes
----------------

Manager
^^^^^^^

-  The Vulnerability Detection module no longer downloads external vulnerability feeds indexed by Canonical, Debian, Red Hat, Arch Linux, Amazon Linux Advisories Security (ALAS), Microsoft, and the National Vulnerability Database (NVD). Instead, the vulnerability detection capability now uses the new Wazuh CTI platform. `wazuh #14153 <https://github.com/wazuh/wazuh/issues/14153>`__
-  The Vulnerability Detection module requires setting up communication with the Wazuh indexer. `wazuh #14153 <https://github.com/wazuh/wazuh/issues/14153>`__
-  The Vulnerability Detector module has been renamed to Vulnerability Detection. The ``vulnerability-detector`` configuration option has been renamed to ``vulnerability-detection``. `wazuh #19781 <https://github.com/wazuh/wazuh/issues/19781>`__

Dashboard plugin
^^^^^^^^^^^^^^^^

-  The  Wazuh dashboard ``disabled_roles`` setting has been removed. Now, the Wazuh dashboard is visible to every Wazuh indexer role. `wazuh-dashboard-plugins #5841 <https://github.com/wazuh/wazuh-dashboard-plugins/issues/5841>`__
-  The  Wazuh dashboard ``customization.logo.sidebar`` setting has been removed, and the sidebar logo is no longer customizable. `wazuh-dashboard-plugins #5841 <https://github.com/wazuh/wazuh-dashboard-plugins/issues/5841>`__
-  The ``extensions.*`` settings have been removed. Now, all Wazuh modules are visible in the main menu. `wazuh-dashboard-plugins #5841 <https://github.com/wazuh/wazuh-dashboard-plugins/issues/5841>`__
-  The default Wazuh dashboard home URL has changed from ``https://<WAZUH_DASHBOARD_URL>/app/wazuh``  to ``https://<WAZUH_DASHBOARD_URL>/app/wz-home``. You can check the ``/etc/wazuh-dashboard/opensearch_dashboard.yml`` configuration file and replace the ``uiSettings.overrides.defaultRoute: /app/wazuh`` setting with ``uiSettings.overrides.defaultRoute: /app/wz-home`` if needed. An ``app not found`` error will appear if this value is incorrect. `wazuh-packages #2497 <https://github.com/wazuh/wazuh-packages/pull/2497>`__

What's new
----------

This release includes new features or enhancements as the following:

Manager
^^^^^^^

-  `#21201 <https://github.com/wazuh/wazuh/pull/21201>`__ Refactored vulnerability detection capability.
-  `#18476 <https://github.com/wazuh/wazuh/pull/18476>`__ Improved ``wazuh-db`` detection of deleted database files.
-  `#16893 <https://github.com/wazuh/wazuh/pull/16893>`__ Added ``timeout`` and ``retry`` parameters to the VirusTotal integration.
-  `#18988 <https://github.com/wazuh/wazuh/pull/18988>`__ Extended ``wazuh-analysisd`` EPS metrics with events dropped by overload and remaining credits in the previous cycle.
-  `#19819 <https://github.com/wazuh/wazuh/pull/19819>`__ Replaced Filebeat date index name processor to ensure the indices are identifiable by the index alias for auto-rollover.
-  `#18466 <https://github.com/wazuh/wazuh/pull/18466>`__ Updated API and framework packages installation commands to use ``pip`` instead of direct invocation of ``setuptools``.
-  `#17015 <https://github.com/wazuh/wazuh/pull/17015>`__ Refactored how cluster status dates are treated in the cluster.
-  `#21602 <https://github.com/wazuh/wazuh/pull/21602>`__ The log message about file rotation and signature from wazuh-monitord has been updated.
-  `#21670 <https://github.com/wazuh/wazuh/pull/21670>`__ Implemented a dedicated keystore for indexer configuration to improve management of sensitive information.
-  `#22774 <https://github.com/wazuh/wazuh/pull/22774>`__ Improved Wazuh-DB performance by adjusting SQLite synchronization policy.
-  `#17750 <https://github.com/wazuh/wazuh/pull/17750>`__ Upgraded docker-compose V1 to V2 in API Integration test scripts.

Agent
^^^^^

-  `#15740 <https://github.com/wazuh/wazuh/pull/15740>`__ Added snap package manager support to Syscollector.
-  `#18574 <https://github.com/wazuh/wazuh/pull/18574>`__ Disabled host's IP query by Logcollector when ``ip_update_interval=0``.
-  `#17932 <https://github.com/wazuh/wazuh/pull/17932>`__ Added event size validation for the external integrations.
-  `#17623 <https://github.com/wazuh/wazuh/pull/17623>`__ Refactored and modularized the AWS integration code.
-  `#17623 <https://github.com/wazuh/wazuh/pull/17623>`__ Added new unit tests for the AWS integration.
-  `#19064 <https://github.com/wazuh/wazuh/pull/19064>`__ Added multiple tenants support to the MS Graph integration module.
-  `#16200 <https://github.com/wazuh/wazuh/pull/16200>`__ FIM now buffers the Linux audit events for who-data to prevent side effects in other components.
-  `#19720 <https://github.com/wazuh/wazuh/pull/19720>`__ The sub-process execution implementation has been improved.
-  `#20649 <https://github.com/wazuh/wazuh/pull/20649>`__ Added geolocation mapping for the AWS WAF events.
-  `#21530 <https://github.com/wazuh/wazuh/pull/21530>`__ Added a validation to reject unsupported regions when using the inspector service.
-  `#21561 <https://github.com/wazuh/wazuh/pull/21561>`__ Added additional information on some AWS integration errors.
-  `#21791 <https://github.com/wazuh/wazuh/pull/21791>`__ Replaced the usage of `fopen` with `wfopen` to avoid processing invalid characters on Windows.
-  `#21637 <https://github.com/wazuh/wazuh/pull/21637>`__ Fixed installation script to prevent macOS agent to start automatically after installation.

RESTful API
^^^^^^^^^^^

-  `#19952 <https://github.com/wazuh/wazuh/pull/19952>`__ Added new ``GET /manager/version/check`` API endpoint to obtain information about new releases of Wazuh.
-  `#20119 <https://github.com/wazuh/wazuh/pull/20119>`__ Removed ``PUT /vulnerability``, ``GET /vulnerability/{agent_id}``, ``GET /vulnerability/{agent_id}/last_scan`` and ``GET /vulnerability/{agent_id}/summary/{field}`` API endpoints as they were deprecated in version 4.7.0. Use the Wazuh indexer REST API instead.
-  `#20420 <https://github.com/wazuh/wazuh/pull/20420>`__ Added the ``auto`` option to the ``ssl_protocol`` setting in the API configuration. This option enables automatic negotiation of the TLS certificate.
-  `#21572 <https://github.com/wazuh/wazuh/pull/21572>`__ Removed the ``compilation_date`` field from ``GET /cluster/{node_id}/info`` and ``GET /manager/info`` endpoints.
-  `#22387 <https://github.com/wazuh/wazuh/pull/22387>`__ Deprecated the ``cache`` configuration option.
-  `#17048 <https://github.com/wazuh/wazuh/pull/17048>`__ Removed the ``custom`` parameter from the ``PUT /active-response`` endpoint.
-  `#22727 <https://github.com/wazuh/wazuh/pull/22727>`__ Added API configuration option to protect the Wazuh indexer configuration from updates.

Ruleset
^^^^^^^

-  `#19528 <https://github.com/wazuh/wazuh/pull/19528>`__ Added rules to detect IcedID attacks.
-  `#17780 <https://github.com/wazuh/wazuh/pull/17780>`__ Added new SCA policy for Amazon Linux 2023.
-  `#18721 <https://github.com/wazuh/wazuh/pull/18721>`__ Revised SCA policy for Ubuntu Linux 18.04.
-  `#17515 <https://github.com/wazuh/wazuh/pull/17515>`__ Revised SCA policy for Ubuntu Linux 22.04.
-  `#18440 <https://github.com/wazuh/wazuh/pull/18440>`__ Revised SCA policy for Red Hat Enterprise Linux 7.
-  `#17770 <https://github.com/wazuh/wazuh/pull/17770>`__ Revised SCA policy for Red Hat Enterprise Linux 8.
-  `#17412 <https://github.com/wazuh/wazuh/pull/17412>`__ Revised SCA policy for Red Hat Enterprise Linux 9.
-  `#17624 <https://github.com/wazuh/wazuh/pull/17624>`__ Revised SCA policy for CentOS 7.
-  `#18439 <https://github.com/wazuh/wazuh/pull/18439>`__ Revised SCA policy for CentOS 8.
-  `#18010 <https://github.com/wazuh/wazuh/pull/18010>`__ Revised SCA policy for Debian 8.
-  `#17922 <https://github.com/wazuh/wazuh/pull/17922>`__ Revised SCA policy for Debian 10.
-  `#18695 <https://github.com/wazuh/wazuh/pull/18695>`__ Revised SCA policy for Amazon Linux 2.
-  `#18985 <https://github.com/wazuh/wazuh/pull/18985>`__ Revised SCA policy for SUSE Linux Enterprise 15.
-  `#19037 <https://github.com/wazuh/wazuh/pull/19037>`__ Revised SCA policy for macOS 13.0 Ventura.
-  `#19515 <https://github.com/wazuh/wazuh/pull/19515>`__ Revised SCA policy for Microsoft Windows 10 Enterprise.
-  `#20044 <https://github.com/wazuh/wazuh/pull/20044>`__ Revised SCA policy for Microsoft Windows 11 Enterprise.
-  `#17518 <https://github.com/wazuh/wazuh/pull/17518>`__ Updated MITRE DB to v13.1.

Other
^^^^^

-  `#20003 <https://github.com/wazuh/wazuh/pull/20003>`__ Upgraded embedded Python version to ``3.10.13``.
-  `#23112 <https://github.com/wazuh/wazuh/pull/23112>`__ Upgraded external ``aiohttp`` library dependency version to ``3.9.5``.
-  `#22221 <https://github.com/wazuh/wazuh/pull/22221>`__ Upgraded external ``cryptography`` library dependency version to ``42.0.4``.
-  `#21710 <https://github.com/wazuh/wazuh/pull/21710>`__ Upgraded external ``curl`` library dependency version to ``8.5.0``.
-  `#20003 <https://github.com/wazuh/wazuh/pull/20003>`__ Upgraded external ``grpcio`` library dependency version to ``1.58.0``.
-  `#23112 <https://github.com/wazuh/wazuh/pull/23112>`__ Upgraded external ``idna`` library dependency version to ``3.7``.
-  `#21684 <https://github.com/wazuh/wazuh/pull/21684>`__ Upgraded external ``Jinja2`` library dependency version to ``3.1.3``.
-  `#21710 <https://github.com/wazuh/wazuh/pull/21710>`__ Upgraded external ``libarchive`` library dependency version to ``3.7.2``.
-  `#20003 <https://github.com/wazuh/wazuh/pull/20003>`__ Upgraded external ``numpy`` library dependency version to ``1.26.0``.
-  `#21710 <https://github.com/wazuh/wazuh/pull/21710>`__ Upgraded external ``pcre2`` library dependency version to ``10.42``.
-  `#20493 <https://github.com/wazuh/wazuh/pull/20493>`__ Upgraded external ``pyarrow`` library dependency version to ``14.0.1``.
-  `#21710 <https://github.com/wazuh/wazuh/pull/21710>`__ Upgraded external ``rpm`` library dependency version to ``4.18.2``.
-  `#20741 <https://github.com/wazuh/wazuh/pull/20741>`__ Upgraded external ``SQLAlchemy`` library dependency version to ``2.0.23``.
-  `#21710 <https://github.com/wazuh/wazuh/pull/21710>`__ Upgraded external ``sqlite`` library dependency version to ``3.45.0``.
-  `#20630 <https://github.com/wazuh/wazuh/pull/20630>`__ Upgraded external ``urllib3`` library dependency version to ``1.26.18``.
-  `#21710 <https://github.com/wazuh/wazuh/pull/21710>`__ Upgraded external ``zlib`` library dependency version to ``1.3.1``.
-  `#21710 <https://github.com/wazuh/wazuh/pull/21710>`__ Added external ``lua`` library dependency version ``5.3.6``.
-  `#21749 <https://github.com/wazuh/wazuh/pull/21749>`__ Added external ``PyJWT`` library dependency version ``2.8.0``.
-  `#21749 <https://github.com/wazuh/wazuh/pull/21749>`__ Removed external ``python-jose`` and ``ecdsa`` library dependencies.

Dashboard plugin
^^^^^^^^^^^^^^^^

-  `#5791 <https://github.com/wazuh/wazuh-dashboard-plugins/pull/5791>`__ Added remember server address check.
-  `#6093 <https://github.com/wazuh/wazuh-dashboard-plugins/pull/6093>`__ Added a notification about new Wazuh updates and a button to check their availability. `#6256 <https://github.com/wazuh/wazuh-dashboard-plugins/pull/6256>`__ `#6328 <https://github.com/wazuh/wazuh-dashboard-plugins/pull/6328>`__
-  `#6083 <https://github.com/wazuh/wazuh-dashboard-plugins/pull/6083>`__ Added the ``ssl_agent_ca`` configuration to the **SSL Settings** form.
-  `#5896 <https://github.com/wazuh/wazuh-dashboard-plugins/pull/5896>`__ Added global vulnerabilities dashboards.
-  `#5840 <https://github.com/wazuh/wazuh-dashboard-plugins/pull/5840>`__ Added an agent selector to the agent view.
-  `#5840 <https://github.com/wazuh/wazuh-dashboard-plugins/pull/5840>`__ Moved the Wazuh menu into the side menu. `#6226 <https://github.com/wazuh/wazuh-dashboard-plugins/pull/6226>`__ `#6423 <https://github.com/wazuh/wazuh-dashboard-plugins/pull/6423>`__  `#6510 <https://github.com/wazuh/wazuh-dashboard-plugins/pull/6510>`__ `#6591 <https://github.com/wazuh/wazuh-dashboard-plugins/pull/6591>`__
-  `#5840 <https://github.com/wazuh/wazuh-dashboard-plugins/pull/5840>`__ Removed the ``disabled_roles`` and ``customization.logo.sidebar`` settings.
-  `#5840 <https://github.com/wazuh/wazuh-dashboard-plugins/pull/5840>`__ Removed module visibility configuration and removed the ``extensions.*`` settings.
-  `#6035 <https://github.com/wazuh/wazuh-dashboard-plugins/pull/6035>`__ Updated all dashboard visualization definitions. `#6632 <https://github.com/wazuh/wazuh-dashboard-plugins/pull/6632>`__  `#6690 <https://github.com/wazuh/wazuh-dashboard-plugins/pull/6690>`__
-  `#6067 <https://github.com/wazuh/wazuh-dashboard-plugins/pull/6067>`__ Reorganized tabs order in all modules.
-  `#6174 <https://github.com/wazuh/wazuh-dashboard-plugins/pull/6174>`__ Removed the implicit filter of WQL language of the search bar UI.
-  `#6373 <https://github.com/wazuh/wazuh-dashboard-plugins/pull/6373>`__ Changed the **API configuration** title to **API Connections**.
-  `#6366 <https://github.com/wazuh/wazuh-dashboard-plugins/pull/6366>`__ Removed **Compilation date** field from the **Status** view.
-  `#6361 <https://github.com/wazuh/wazuh-dashboard-plugins/pull/6361>`__ Removed ``WAZUH_REGISTRATION_SERVER`` variable from Windows agent deployment command.
-  `#6354 <https://github.com/wazuh/wazuh-dashboard-plugins/pull/6354>`__ Added a dash character and a tooltip element to **Run as** in the API configuration table to indicate it's been disabled.
-  `#6364 <https://github.com/wazuh/wazuh-dashboard-plugins/pull/6364>`__ Added tooltip element to **Most active agent** in **Details** in the **Endpoint summary** view and renamed a label element. `#6421 <https://github.com/wazuh/wazuh-dashboard-plugins/pull/6421>`__
-  `#6379 <https://github.com/wazuh/wazuh-dashboard-plugins/pull/6379>`__ Changed overview home top KPIs. `#6408 <https://github.com/wazuh/wazuh-dashboard-plugins/pull/6408>`__ `#6569 <https://github.com/wazuh/wazuh-dashboard-plugins/pull/6569>`__
-  `#6341 <https://github.com/wazuh/wazuh-dashboard-plugins/pull/6341>`__ Removed notice of old **Discover** deprecation.
-  `#6492 <https://github.com/wazuh/wazuh-dashboard-plugins/pull/6492>`__ Updated the PDF report year number to 2024.
-  `#6702 <https://github.com/wazuh/wazuh-dashboard-plugins/pull/6702>`__ Adjusted font style of **Endpoints summary** KPIs, **Index pattern**, and API selectors, as well as adjusted the **Dev Tools** column widths.

Packages
^^^^^^^^

-  `#2332 <https://github.com/wazuh/wazuh-packages/pull/2332>`__ Added check into the installation assistant to prevent the use of public IP addresses.
-  `#2365 <https://github.com/wazuh/wazuh-packages/pull/2365>`__ Removed the ``postProvision.sh`` script. It's no longer used in OVA generation.
-  `#2364 <https://github.com/wazuh/wazuh-packages/pull/2364>`__ Added ``curl`` error messages in downloads.
-  `#2469 <https://github.com/wazuh/wazuh-packages/pull/2469>`__ Improved debug output in the installation assistant.
-  `#2557 <https://github.com/wazuh/wazuh-packages/pull/2557>`__ Added SCA policy for Amazon Linux 2023 in SPECS.
-  `#2558 <https://github.com/wazuh/wazuh-packages/pull/2558>`__ Wazuh password tool now recognizes UI created users.
-  `#2562 <https://github.com/wazuh/wazuh-packages/pull/2562>`__ Bumped Wazuh indexer to OpenSearch 2.10.0.
-  `#2563 <https://github.com/wazuh/wazuh-packages/pull/2563>`__ Bumped Wazuh dashboard to OpenSearch Dashboards 2.10.0.
-  `#2577 <https://github.com/wazuh/wazuh-packages/pull/2577>`__ Added APT and YUM lock logic to the Wazuh installation assistant.
-  `#2164 <https://github.com/wazuh/wazuh-packages/pull/2164>`__ Deprecated CentOS 6 and Debian 7 for the Wazuh manager compilation, while still supporting them in the Wazuh agent compilation.
-  `#2588 <https://github.com/wazuh/wazuh-packages/pull/2588>`__ Added logic to the installation assistant to check for clean Wazuh central components removal.
-  `#2615 <https://github.com/wazuh/wazuh-packages/pull/2615>`__ Added branding images to the header of Wazuh dashboard.
-  `#2696 <https://github.com/wazuh/wazuh-packages/pull/2696>`__ Updated Filebeat module version to 0.4 in Wazuh installation assistant.
-  `#2695 <https://github.com/wazuh/wazuh-packages/pull/2695>`__ Added content database in RPM and DEB packages.
-  `#2669 <https://github.com/wazuh/wazuh-packages/pull/2669>`__ Upgraded ``botocore`` dependency in WPK package Docker containers.
-  `#2738 <https://github.com/wazuh/wazuh-packages/pull/2738>`__ Added ``xz utils`` as requirement.
-  `#2777 <https://github.com/wazuh/wazuh-packages/pull/2777>`__ Added support for refactored vulnerability detector in the installation assistant.
-  `#2797 <https://github.com/wazuh/wazuh-packages/pull/2797>`__ The Wazuh installation assistant now uses ``127.0.0.1`` instead of ``localhost`` in the Wazuh dashboard configuration. `#2808 <https://github.com/wazuh/wazuh-packages/pull/2808>`__
-  `#2801 <https://github.com/wazuh/wazuh-packages/pull/2801>`__ Added check into the installation assistant to ensure ``sudo`` package is installed.
-  `#2802 <https://github.com/wazuh/wazuh-packages/pull/2802>`__ Added the Wazuh keystore functionality to the passwords tool.
-  `#2809 <https://github.com/wazuh/wazuh-packages/pull/2809>`__ Upgrade scripts to support building Wazuh with OpenSSL 3.0.
-  `#2784 <https://github.com/wazuh/wazuh-packages/pull/2784>`__ Added rollback and exit in case the Wazuh indexer security admin fails.
-  `#2804 <https://github.com/wazuh/wazuh-packages/pull/2804>`__ Added the keystore tool for both RPM and DEB manager packages creation. `#2802 <https://github.com/wazuh/wazuh-packages/pull/2802>`_
-  `#2798 <https://github.com/wazuh/wazuh-packages/pull/2798>`__ Add compression for the Wazuh manager due to inclusion of Vulnerability Detection databases.
-  `#2796 <https://github.com/wazuh/wazuh-packages/pull/2796>`__ Simplified the Wazuh dashboard help menu entries.
-  `#2792 <https://github.com/wazuh/wazuh-packages/pull/2792>`__ Improved certificates generation output when using the Wazuh Installation Assistant and the Wazuh Certs Tool.
-  `#2891 <https://github.com/wazuh/wazuh-packages/pull/2891>`__ Skipped certificate validation for CentOS 5 package generation.
-  `#2890 <https://github.com/wazuh/wazuh-packages/pull/2890>`__ Updated the file permissions of vulnerability detection-related directories.
-  `#2966 <https://github.com/wazuh/wazuh-packages/pull/2966>`__ Added Ubuntu 24 support to the Wazuh installation assistant.
-  `#2422 <https://github.com/wazuh/wazuh-packages/pull/2422>`__ Added the possibility of registering the ``localhost`` domain in the installation assistant and in the cert-tool.
-  `#2408 <https://github.com/wazuh/wazuh-packages/pull/2408>`__ Added new AWS files to Solaris SPECS.
-  `#2553 <https://github.com/wazuh/wazuh-packages/pull/2553>`__ Added new role to grant ISM API permissions.
-  `#2578 <https://github.com/wazuh/wazuh-packages/pull/2578>`__ Changed the order of Explore category and Indexer/dashboard management title on dashboard.
-  `#2582 <https://github.com/wazuh/wazuh-packages/pull/2582>`__ Added the ISM init script to the Wazuh indexer package.
-  `#2584 <https://github.com/wazuh/wazuh-packages/pull/2584>`__ Added ISM script in installation assistant.
-  `#2586 <https://github.com/wazuh/wazuh-packages/pull/2586>`__ Moved ISM scripts from package to base.
-  `#2590 <https://github.com/wazuh/wazuh-packages/pull/2590>`__ Extended ``indexer-init.sh`` to accept arguments.
-  `#2592 <https://github.com/wazuh/wazuh-packages/pull/2592>`__ Updated the initialize cluster script in the offline installation workflow.
-  `#2598 <https://github.com/wazuh/wazuh-packages/pull/2598>`__ Updated ``min_doc_count`` value.
-  `#2606 <https://github.com/wazuh/wazuh-packages/pull/2606>`__ Improved ISM init script.
-  `#2609 <https://github.com/wazuh/wazuh-packages/pull/2609>`__ Adapted wazuhapp and Wazuh dashboard to install the Wazuh ``CheckUpdates`` and ``Core`` plugins.
-  `#2639 <https://github.com/wazuh/wazuh-packages/pull/2639>`__ Changed check yum lock function.
-  `#2653 <https://github.com/wazuh/wazuh-packages/pull/2653>`__ Collapsed initially the application categories in the side menu of Wazuh dashboard.
-  `#2687 <https://github.com/wazuh/wazuh-packages/pull/2687>`__ Added ``common_checkAptLock`` function.
-  `#2700 <https://github.com/wazuh/wazuh-packages/pull/2700>`__ Updated ``indexer-ism-init.sh``.
-  `#2711 <https://github.com/wazuh/wazuh-packages/pull/2711>`__ Ensured ``config`` is present in ``ossec.conf`` after upgrade via rpm.
-  `#2712 <https://github.com/wazuh/wazuh-packages/pull/2712>`__ Added ``wazuh-filebeat`` template to Wazuh indexer.
-  `#2713 <https://github.com/wazuh/wazuh-packages/pull/2713>`__ Removed ``wazuh-template`` json.
-  `#2726 <https://github.com/wazuh/wazuh-packages/pull/2726>`__ Updated ``indexer-ism-init.sh``.
-  `#2733 <https://github.com/wazuh/wazuh-packages/pull/2733>`__ Updated ``indexer-ism-init.sh``.
-  `#2742 <https://github.com/wazuh/wazuh-packages/pull/2742>`__ Vulnerability detection refactor.
-  `#2748 <https://github.com/wazuh/wazuh-packages/pull/2748>`__ Removed flag ``--download-content``.
-  `#2782 <https://github.com/wazuh/wazuh-packages/pull/2782>`__ Split CentOS and RHEL check.
-  `#2789 <https://github.com/wazuh/wazuh-packages/pull/2789>`__ Updated Wazuh favicon for Safari.
-  `#2795 <https://github.com/wazuh/wazuh-packages/pull/2795>`__ Replaced category management description.
-  `#2792 <https://github.com/wazuh/wazuh-packages/pull/2792>`__ Improved certificates generation output when using the Wazuh Installation Assistant and the Wazuh Certs Tool.
-  `#2807 <https://github.com/wazuh/wazuh-packages/pull/2807>`__ Silenced sudo package check.
-  `#2821 <https://github.com/wazuh/wazuh-packages/pull/2821>`__ Removed debug variable in Admin certificate generation.
-  `#2822 <https://github.com/wazuh/wazuh-packages/pull/2822>`__ Do not decompress .tar.xz file, remove xz dependency.
-  `#2827 <https://github.com/wazuh/wazuh-packages/pull/2827>`__ Added step for restore ``ossec.conf`` file in backup/restore scripts.
-  `#2838 <https://github.com/wazuh/wazuh-packages/pull/2838>`__ Removed ``download-content.sh`` and ``download.rules`` files.

Resolved issues
---------------

This release resolves known issues as the following:

Manager
^^^^^^^

-  `#17886 <https://github.com/wazuh/wazuh/pull/17886>`__ Updated cluster connection cleanup to remove temporary files when the connection between a worker and a master is broken.
-  `#23371 <https://github.com/wazuh/wazuh/pull/23371>`__ Added a mechanism to prevent cluster errors from an expected wazuh-db exception.
-  `#23216 <https://github.com/wazuh/wazuh/pull/23216>`__ Fixed a race condition when creating agent database files from a template.

Agent
^^^^^

-  `#16839 <https://github.com/wazuh/wazuh/pull/16839>`__ Fixed process path retrieval in Syscollector on Windows XP.
-  `#16056 <https://github.com/wazuh/wazuh/pull/16056>`__ Fixed the OS version detection on Alpine Linux.
-  `#18642 <https://github.com/wazuh/wazuh/pull/18642>`__ Fixed Solaris 10 name not showing in the dashboard.
-  `#21932 <https://github.com/wazuh/wazuh/pull/21932>`__ Fixed an error in macOS Ventura compilation from sources.
-  `#23532 <https://github.com/wazuh/wazuh/pull/23532>`__ Fixed PyPI package gathering on macOS Sonoma.

RESTful API
^^^^^^^^^^^

-  `#20527 <https://github.com/wazuh/wazuh/pull/20527>`__ Fixed a warning from SQLAlchemy involving detached Roles instances in RBAC.
-  `#23120 <https://github.com/wazuh/wazuh/pull/23120>`__ Fixed an issue in ``GET /manager/configuration`` where only the last of multiple ``<ignore>`` items in the configuration file was displayed.

Dashboard plugin
^^^^^^^^^^^^^^^^

-  `#5840 <https://github.com/wazuh/wazuh-dashboard-plugins/pull/5840>`__ Fixed a problem with the agent menu header when the side menu is docked.
-  `#6102 <https://github.com/wazuh/wazuh-dashboard-plugins/pull/6102>`__ Fixed how the query filters apply on the Security Alerts table.
-  `#6177 <https://github.com/wazuh/wazuh-dashboard-plugins/pull/6177>`__ Fixed exception in agent view when an agent doesn't have policies.
-  `#6177 <https://github.com/wazuh/wazuh-dashboard-plugins/pull/6177>`__ Fixed exception in **Inventory** when agents don't have operating system information.
-  `#6177 <https://github.com/wazuh/wazuh-dashboard-plugins/pull/6177>`__ Fixed pinned agent state in URL.
-  `#6234 <https://github.com/wazuh/wazuh-dashboard-plugins/pull/6234>`__ Fixed invalid date format in **About** and **Agents** views.
-  `#6305 <https://github.com/wazuh/wazuh-dashboard-plugins/pull/6305>`__ Fixed issue with script to install agents on macOS if using the registration password deployment variable.
-  `#6327 <https://github.com/wazuh/wazuh-dashboard-plugins/pull/6327>`__ Fixed an issue preventing the use of a hostname as the **Server address** in **Deploy New Agent**.
-  `#6342 <https://github.com/wazuh/wazuh-dashboard-plugins/pull/6342>`__ Fixed wrong **Queue Usage** values in **Server management** > **Statistics**.
-  `#6352 <https://github.com/wazuh/wazuh-dashboard-plugins/pull/6352>`__ Fixed **Statistics** view errors when cluster mode is disabled.
-  `#6374 <https://github.com/wazuh/wazuh-dashboard-plugins/pull/6374>`__ Fixed the help menu, to be consistent and avoid duplication.
-  `#6378 <https://github.com/wazuh/wazuh-dashboard-plugins/pull/6378>`__ Fixed the axis label visual bug from dashboards.
-  `#6431 <https://github.com/wazuh/wazuh-dashboard-plugins/pull/6431>`__ Fixed error displaying when clicking **Refresh** in **MITRE ATT&CK** if the the Wazuh indexer service is down.
-  `#6484 <https://github.com/wazuh/wazuh-dashboard-plugins/pull/6484>`__ Fixed minor style issues. `#6489 <https://github.com/wazuh/wazuh-dashboard-plugins/pull/6489>`__ `#6587 <https://github.com/wazuh/wazuh-dashboard-plugins/pull/6587>`__
-  `#6617 <https://github.com/wazuh/wazuh-dashboard-plugins/pull/6617>`__ Fixed error when clicking **Log collection** in **Configuration** of a disconnected agent.
-  `#6333 <https://github.com/wazuh/wazuh-dashboard-plugins/pull/6333>`__ Fixed a typo in an abbreviation for Fully Qualified Domain Name.
-  `#6553 <https://github.com/wazuh/wazuh-dashboard-plugins/pull/6553>`__ Fixed "*View alerts of this Rule*" link.

Packages
^^^^^^^^

-  `#2381 <https://github.com/wazuh/wazuh-packages/pull/2381>`__ Fixed DNS validation in the installation assistant.
-  `#2401 <https://github.com/wazuh/wazuh-packages/pull/2401>`__ Fixed debug redirection in the installation assistant.
-  `#2850 <https://github.com/wazuh/wazuh-packages/pull/2850>`__ Fixed certificates generation output for certificates not created.
-  `#2906 <https://github.com/wazuh/wazuh-packages/pull/2906>`__ Moved up the hardware check of the installation assistant. Now dependencies don't get installed if it fails.
-  `#2380 <https://github.com/wazuh/wazuh-packages/pull/2380>`__ Fixed ``source_branch`` variable in ``master`` branch.
-  `#2535 <https://github.com/wazuh/wazuh-packages/pull/2535>`__ Fixed ``mkdir wazuh-install-files`` error.
-  `#2560 <https://github.com/wazuh/wazuh-packages/pull/2560>`__ Fixed ``internalusers-backup`` directory owner and permissions.
-  `#2585 <https://github.com/wazuh/wazuh-packages/pull/2585>`__ Fixed bug with ``-i`` option.
-  `#2646 <https://github.com/wazuh/wazuh-packages/pull/2646>`__ Fixed ``wazuh-indexer.spec`` duplicated information.
-  `#2723 <https://github.com/wazuh/wazuh-packages/pull/2723>`__ Fixed Filebeat template URL in Wazuh indexer.
-  `#2796 <https://github.com/wazuh/wazuh-packages/pull/2796>`__ Fixed duplicated help menu.

Changelogs
----------

The repository changelogs provide more details about the changes.

Product repositories
^^^^^^^^^^^^^^^^^^^^

-  `wazuh/wazuh <https://github.com/wazuh/wazuh/blob/v4.8.0/CHANGELOG.md>`__
-  `wazuh/wazuh-dashboard-plugins <https://github.com/wazuh/wazuh-dashboard-plugins/blob/v4.8.0-2.10.0/CHANGELOG.md>`__
-  `wazuh/wazuh-packages <https://github.com/wazuh/wazuh-packages/blob/v4.8.0/CHANGELOG.md>`__

Auxiliary repositories
^^^^^^^^^^^^^^^^^^^^^^^

-  `wazuh/wazuh-ansible <https://github.com/wazuh/wazuh-ansible/blob/v4.8.0/CHANGELOG.md>`__
-  `wazuh/wazuh-kubernetes <https://github.com/wazuh/wazuh-kubernetes/blob/v4.8.0/CHANGELOG.md>`__
-  `wazuh/wazuh-puppet <https://github.com/wazuh/wazuh-puppet/blob/v4.8.0/CHANGELOG.md>`__
-  `wazuh/wazuh-docker <https://github.com/wazuh/wazuh-docker/blob/v4.8.0/CHANGELOG.md>`__

-  `wazuh/wazuh-qa <https://github.com/wazuh/wazuh-qa/blob/v4.8.0/CHANGELOG.md>`__
-  `wazuh/qa-integration-framework <https://github.com/wazuh/qa-integration-framework/blob/v4.8.0/CHANGELOG.md>`__

-  `wazuh/wazuh-documentation <https://github.com/wazuh/wazuh-documentation/blob/v4.8.0/CHANGELOG.md>`__
