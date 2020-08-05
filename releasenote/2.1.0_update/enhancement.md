# Changed APIs

<br />

EnOS 2.1 Update Release introduces the following API behavioral changes.

## Connection Service

.. list-table::
   :widths: 40 60
   :header-rows: 1

   * - API
     - Description
   * - `Download File <../../connect/download_file>`_
     - Added ``category`` to request parameter (URI) which indicates the type of the file to be downloaded.
   * - `Upload Attribute <../../connect/upload_integration_attributes>`_
     - Added a required parameter ``Content-length`` to the header of the file form-data in the request body. The parameter indicates the file size.
   * - `Upload Event <../../connect/upload_integration_events>`_
     - Added a required parameter ``Content-length`` to the header of the file form-data in the request body. The parameter indicates the file size.
   * - `Upload Measurement Point <../../connect/upload_integration_measurepoints>`_
     - Added a required parameter ``Content-length`` to the header of the file form-data in the request body. The parameter indicates the file size.
   * - `Apply Certificate <../../connect/apply_cert>`_
     - Added ``issueAuthority`` to the request parameters. Updated error codes.
   * - `Renew Certificate <../../connect/update_cert>`_
     - Added ``issueAuthority`` to the request parameters. Updated error codes.
   * - `Revoke Certificate <../../connect/delete_cert>`_
     - Updated error codes.
   * - `List Certificate <../../connect/list_cert>`_
     - Updated error codes.
   * - `Search Device <../../connect/search_device>`_
     - ``Expression`` supports querying by ``deviceAttributes`` and ``deviceTags``.

## Batch Processing Service

Starting from EnOS 2.1.2 release, the **Dataflow Service** is renamed **Batch Processing Service**. In the API request URL, ``dataflow-batch-service`` is changed to ``batch-processing-service``, and the API version is upgraded to ``v2.1``. The new version includes the following updates:

.. list-table::
   :widths: 20 20 30 30
   :header-rows: 1

   * - Changed Item
     - Before
     - After
     - Impact
   * - Response field rename
     - status
     - code
     - All APIs
   * - Successful request
     - Success
     - OK
     - All APIs
   * - ``searchValue`` filed rename
     - searchValue
     - expression
     - Get My Flow
   * - ``pagination`` struct
     - Value of ``pageNo`` starts from 0
     - Value of ``pageNo`` starts from 1
     - Search Flow，List Flow Instances

<!--end-->
