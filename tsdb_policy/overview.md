# TSDB Policy Service Overview


## API List

.. list-table::
   :widths: auto
   :header-rows: 1

   * - Operation Name
     - Description
   * - `Get Measurement Point TSDB Metadata <get_points_tsdb_meta_data>`__
     - Get the TSDB storage policy corresponding to the model measurement point. A measurement point can have multiple storage policies, depending on its data type and usage. This API returns all the TSDB storage policy metadata in the current organization for the specified measurement point.
   * - `Get Storage Policy <get_storage_policy>`__
     - Get detailed information of specified storage policy with storage policy ID.
   * - `Save Storage Policy <save_storage_policy>`__
     - With storage policy ID, update and save the configuration of specified storage policy.


## Common Error Codes

.. list-table::
   :widths: 10 40 50
   :header-rows: 1

   * - Code
     - Message
     - Description
   * - 0
     - OK
     - API request is successful.
   * - 500
     - Internal Server Error
     - Internal server error (applies to the `Get Measurement Point TSDB Metadata` API ony).
   * - 80500
     - INTERNAL SERVER ERROR
     - Internal server error. For details, check the returned error message.


<!--end-->
