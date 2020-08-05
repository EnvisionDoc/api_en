# New APIs

<br />

In EnOS 2.1 Update Release, we added support to the following new APIs and API services.

## Connection Service

.. list-table::
   :widths: 40 60
   :header-rows: 1

   * - API Name
     - Description
   * - `Upload Attribute <../../connect/upload_integration_attributes>`_
     - Upload the attribute data of a device, including file-type data.
   * - `Upload Events <../../connect/upload_integration_events>`_
     - Upload the event data of a device, including file-type data.
   * - `Upload Measurement Points <../../connect/upload_integration_measurepoints>`_
     - Upload the measurement point data of a device, including file-type data.
   * - `Download File <../../connect/download_file>`_
     - Download a file from a device.
   * - `Delete File <../../connect/delete_file>`_
     - Delete a file from a device.

## TSDB Data Service

Starting from this release, the **TSDB Data Service** version is upgraded to ``v2.1`` (V2.0 is still in service). The new version has the following new functions and enhancements:

.. list-table::
   :widths: 20 20 30 30
   :header-rows: 1

   * - New Feature / Changes
     - Before
     - After
     - Impact
   * - New request parameter
     - N/A
     - localTimeFormat
     - All APIs
   * - New request parameter
     - N/A
     - itemFormat
     - All APIs
   * - Request method
     - GET/POST
     - POST
     - All APIs
   * - Changed request/response parameter
     - measurepoints
     - pointIds
     - All APIs
   * - Changed request/response parameter
     - meaurepointsWithLogic
     - pointIdsWithLogic
     - All APIs
   * - Changed request/response parameter
     - meaurepoint
     - pointId
     - All APIs
   * - Renamed response code
     - status
     - code
     - All APIs
   * - Message for successful request
     - Success
     - OK
     - All APIs

<br />

The following API is added to the TSDB Data Service API V2.1:

.. list-table::
   :widths: 40 60
   :header-rows: 1

   * - API Name
     - Description
   * - `Delete Asset Latest Data <../../tsdb_service/v2.1/delete_asset_latest_data>`_
     - Delete the latest data of the specified measurement points of specified devices.


## TSDB Policy Service

.. list-table::
   :widths: 40 60
   :header-rows: 1

   * - API Name
     - Description
   * - `Get Storage Policy <../../tsdb_policy/get_storage_policy>`_
     - Get the TSDB storage policy corresponding to the model measurement point.
   * - `Save Storage Policy <../../tsdb_policy/save_storage_policy>`_
     - With storage policy ID, update and save the configuration of specified storage policy.


## IAM Service

.. list-table::
   :widths: 40 60
   :header-rows: 1

   * - API Name
     - Description
   * - `Log In <../../iam/login>`_
     - Log in EnOS.
   * - `Get Session Information <../../iam/get_session_information>`_
     - Get login session information.
   * - `List User Organization <../../iam/list_user_organization>`_
     - List the organizations to which a user belongs.

## Application Portal Service

.. list-table::
   :widths: 40 60
   :header-rows: 1

   * - API Name
     - Description
   * - `Log In Via Authorization Code <../../app_portal/login_via_code>`__
     - Log in Application Portal via authorization code
   * - `Get User Domain <../../app_portal/get_user_domain>`_
     - Get the domain information of a user using the email address.
   * - `Get User Structures <../../app_portal/get_user_structures>`_
     - Get information of the organization structure to which a user is assigned.
   * - `Get Users with Asset Access <../../app_portal/get_privileged_users_to_asset>`_
     - Get the list of users who have access to a particular asset.
   * - `Get Unresolved Messages <../../app_portal/get_unresolved_messages>`_
     - Get the list of unconfirmed application messages.


## Data Federation Service

.. list-table::
   :widths: 40 60
   :header-rows: 1

   * - API Name
     - Description
   * - `List Channels <../../data_federation/list_channels>`__
     - Get the list of created channels (Read and Write) in the organization.
   * - `Read Data <../../data_federation/read_data>`__
     - Read data by providing SQL query through the specified channel.
   * - `List Jobs <../../data_federation/list_jobs>`__
     - Get the data reading jobs or data writing jobs of a specified channel.
   * - `Get Job Details <../../data_federation/get_job_details>`__
     - Get detailed information of a data reading job or a data writing job.
   * - `Write Message <../../data_federation/write_message>`__
     - Write message to data source through a specified channel.
   * - `Write Chunk File <../../data_federation/write_chunk_file>`__
     - Write file chunks to data source through a specified channel.


## Stream Processing Service

.. list-table::
   :widths: 40 60
   :header-rows: 1

   * - API Name
     - Description
   * - `Get Stage State <../../streaming/get_stage_state>`__
     - Get the intermediate state data of a specified operator (stage) in a stream processing job.
   * - `Delete Stage State <../../streaming/delete_stage_state>`__
     - Delete the intermediate state data of a specified operator (stage) in a stream processing job.

<!--end-->
