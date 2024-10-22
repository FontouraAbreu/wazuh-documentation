.. Copyright (C) 2015, Wazuh, Inc.

.. meta::
   :description: You can use the native support for managing and authenticating users or integrate with external user management systems.

Authentication and authorization
================================

You can use the native support for managing and authenticating users or integrate with external user management systems.

.. note::

   You cannot log in to the Wazuh dashboard of your environment with your Wazuh Cloud account credentials. To log in to the Wazuh dashboard, use the default credentials from the Wazuh Cloud Console page or the credentials of any user you already created in the Wazuh dashboard.

Native support for users and roles
----------------------------------

The Wazuh dashboard allows you to add users, create roles, and map roles to users. The following sections highlight more on this.

-  `Creating an internal user and mapping it to Wazuh`_
-  `Creating and setting a Wazuh admin user`_
-  `Creating and setting a Wazuh read-only user`_

Creating an internal user and mapping it to Wazuh
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Follow these steps to create an internal user and map it to its appropriate role.

#. Log into your :doc:`Wazuh dashboard <../getting-started/access-wazuh-wui>` as administrator.
#. Click the upper-left menu icon **☰** and expand **Indexer management** then select **Security**.
#. Select **Internal users** on the left pane then click **Create internal user** and complete the empty fields with the requested information. Click **Apply** to complete the action.

   .. thumbnail:: /images/cloud-service/create-internal-user.gif
      :title: Create internal user
      :alt: Create internal user
      :align: center
      :width: 80%

#. Follow these steps to map the user to the appropriate role:

   #. Click on **Roles** on the left panel and click the role name selected to open the window.
   #. Select the **Mapped users** tab and click **Manage mapping**.
   #. Add the user you created in the previous steps and click **Map** to confirm the action.

      .. thumbnail:: /images/cloud-service/map-user-to-role.gif
         :title: Map user to role
         :alt: Map user to role
         :align: center
         :width: 80%

#. Follow these steps to map the user with Wazuh:

   #. Click the upper-left menu icon **☰** and expand **Server management** then click on **Security**.
   #. On the **Security** page, go to the **Roles mapping** pane.
   #. Click **Create Role mapping** and complete the empty fields with the following parameters:

      -  **Role mapping name**: Assign a name to the role mapping.
      -  **Roles**: Select the Wazuh roles that you want to map the user with.
      -  **Internal users**: Select the internal user created previously.
   #. Click **Save role mapping** to save and map the user with Wazuh.

   .. thumbnail:: /images/cloud-service/map-user.gif
      :title: Map user
      :alt: Map user
      :align: center
      :width: 80%

Creating and setting a Wazuh admin user
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Follow these steps to create an internal user, create a new role mapping, and give administrator permissions to the user.

#. Log into your :doc:`Wazuh dashboard <../getting-started/access-wazuh-wui>` as administrator.
#. Click the upper-left menu icon **☰** and expand **Indexer management** then click on **Security**, and then **Internal users** to open the internal users' page.
#. Click **Create internal user**, complete the empty fields with the requested information, and click **Create** to complete the action.

   .. thumbnail:: /images/cloud-service/create-internal-user.gif
      :title: Create internal user
      :alt: Create internal user
      :align: center
      :width: 80%

#. Follow these steps to map the user to the appropriate role:

   #. Click on **Roles** to open the roles page and search for the ``all_access`` role in the roles list and select it.
   #. Click **Duplicate** role at the top right to duplicate the role.
   #. Assign a name to the new role, then click **Create** to confirm the action.
   #. On the newly created role page, select the **Mapped users** tab and click **Manage mapping**.
   #. Add the user you created in the previous steps and click **Map** to confirm the action.

   .. note::

      Reserved roles are restricted for any permission customizations. You can create a custom role with the same permissions or duplicate a reserved role for further customization.

#. Follow these steps to map the user with Wazuh:

   #. Click the upper-left menu icon **☰** and expand **Server management** then click on **Security**.
   #. On the **Security** page, go to the **Roles mapping** pane.
   #. Click **Create Role mapping** and complete the empty fields with the following parameters:

      -  **Role mapping name**: Assign a name to the role mapping.
      -  **Roles**: Select administrator.
      -  **Internal users**: Select the internal user created previously.

   #. Click **Save role mapping** to save and map the user with Wazuh as administrator.

   .. thumbnail:: /images/cloud-service/map-user2.gif
      :title: Map user
      :alt: Map user
      :align: center
      :width: 80%

Creating and setting a Wazuh read-only user
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Follow these steps to create an internal user, create a new role mapping, and give read-only permissions to the user.

#. Log into your :doc:`Wazuh dashboard </cloud-service/getting-started/access-wazuh-wui>` as administrator.

#. Click the upper-left menu icon **☰** and expand **Indexer management** then click on **Security**, and then **Internal users** to open the internal users' page.

#. Click **Create internal user**, complete the empty fields with the requested information, and click **Create** to complete the action.

#. Follow these steps to map the user to the appropriate role:

   #. Click **Create role**, complete the empty fields with the following parameters, and then click **Create** to complete the task.

      - **Name**: Assign a name to the role.
      - **Cluster permissions**: ``cluster_composite_ops_ro``
      - **Index**: ``*``
      - **Index permissions**: ``read``
      - **Tenant permissions**: ``global_tenant`` and select the **Read only** option.

   #. Select the **Mapped users** tab and click **Manage mapping**.
   #. Add the user you created in the previous steps and click **Map** to confirm the action.

#. Follow these steps to map the user with Wazuh:

   #. Click the upper-left menu icon **☰** and expand **Server management** then click on **Security**.
   #. On the **Security** page, go to the **Roles mapping** pane.
   #. Click **Create Role mapping** and complete the empty fields with the following parameters:

      - **Role mapping name**: Assign a name to the role mapping.
      - **Roles**: Select ``readonly``.
      - **Internal users**: Select the internal user created previously.

   #. Click **Save role mapping** to save and map the user with Wazuh as *read-only*. 

To add more read-only users, you can skip the role creation task and map the users to the already existing read-only role.


Integrating with external user management systems
-------------------------------------------------

You can configure Wazuh to communicate with an external user management system such as LDAP to authenticate users. Open a support ticket through the **Help** section on your Wazuh Cloud Console to perform this integration.
