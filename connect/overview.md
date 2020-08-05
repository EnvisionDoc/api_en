# Connection Service Overview



Provide management operations for products, devices, and commands.


## Product

.. list-table::
   :widths: auto
   :header-rows: 1

   * - Operation Name
     - Description
   * - `Create Product <create_product>`__
     - Create a product
   * - `Delete Product <delete_product>`__
     - Delete a product
   * - `Get Product <get_product>`__
     - Get the details of a product via its ``productKey``
   * - `Search Product <search_product>`__
     - Search for products based on the search criteria
   * - `Update Product <update_product>`__
     - Update a product



## Device

.. list-table::
   :widths: auto
   :header-rows: 1

   * - Operation Name
     - Description
   * - `Create Device <create_device>`__
     - Create a device
   * - `Delete Device <delete_device>`__
     - Delete a device
   * - `Disable Device <disable_device>`__
     - Disable a device
   * - `Enable Device <enable_device>`__
     - Activate a device
   * - `Get Device <get_device>`__
     - Get the information of a device
   * - `Replace Device <replace_device>`__
     - Replace the ``deviceKey`` of a device without changing its ``assetId``
   * - `Search Device <search_device>`__
     - Search for devices based on the search criteria
   * - `Update Device <update_device>`__
     - Update a device

## Certificate

.. list-table::
   :widths: auto
   :header-rows: 1

   * - Operation Name
     - Description
   * - `Apply Certificate <apply_cert>`__
     - Apply for a certificate and bind it to a device
   * - `Renew Certificate <update_cert>`__
     - Update a certificate and bind it to a device
   * - `Revoke Certificate <delete_cert>`__
     - Revoke a certificate bound to a device
   * - `List Certificate <list_cert>`__
     - List the certificates bound to a device


## Gateway and Sub-Device

.. list-table::
   :widths: auto
   :header-rows: 1

   * - Operation Name
     - Description
   * - `Add Sub-Device <add_sub_device>`__
     - Add new sub-devices to the gateway device
   * - `Get Gateway <get_gateway>`__
     - Get the gateway information based on the specified sub-device
   * - `Remove Sub-Device <remove_sub_device>`__
     - Remove sub-devices from the gateway
   * - `Search Sub-Device <search_sub_device>`__
     - Search for sub-devices under the specified gateway





## Device Data

.. list-table::
   :widths: auto
   :header-rows: 1

   * - Operation Name
     - Description
   * - `Cancel Command <cancel_command>`__
     - Cancel cached commands
   * - `Get Command <get_command>`__
     - Get the details of a command
   * - `Get Event <get_event>`__
     - Get the details of an event via ``eventId``
   * - `Invoke Service <invoke_service>`__
     - Service invocation interface for the device
   * - `Search Command <search_command>`__
     - Search for commands
   * - `Search Event <search_event>`__
     - Search for events based on the search criteria
   * - `Set Measurement Point <set_measurepoint>`__
     - Measurepoint setting interface
   * - `Delete File <delete_file>`__ (Preview)
     - Delete a file from a device
   * - `Download File <download_file>`__ (Preview)
     - Download a file from a device

## HTTP Integration (Preview)

.. list-table::
   :widths: auto
   :header-rows: 1

   * - Operation Name
     - Description
   * - `Upload Attribute <upload_integration_attributes>`__ (Preview)
     - Upload the attribute data of a device, including file-type data
   * - `Upload Event <upload_integration_events>`__ (Preview)
     - Upload the event data of a device, including file-type data
   * - `Upload Measurement Point <upload_integration_measurepoints>`__ (Preview)
     - Upload the measurement point data of a device, including file-type data


<!--end-->
