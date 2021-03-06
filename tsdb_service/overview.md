# TSDB Data Service Overview

The EnOS Time Series Database (TSDB) data service provides the interfaces listed below for developers to invoke for data and application development. EnOS TSDB provides efficient and stable storage management for time series data that is ingested from devices or generated by the stream processing engine. Currently, EnOS TSDB can store the following types of asset data:

- Original data of AI measurement points
- Minute-level normalized data of AI measurement points
- Device status (DI) data
- Generic data
- Power consumption/production data

<br />

For more information about TSDB storage, see [Managing Time Series Data](/docs/data-asset/en/2.1.0/howto/storage/index.html).

## API List

.. list-table::
   :widths: auto
   :header-rows: 1

   * - Operation Name
     - Description
   * - `Filter Asset Latest Data <filter_asset_latest_data>`__
     - Filter and query the latest data of a single measurement point for multiple devices.
   * - `Get Asset AI Data with Aggregation Logic <get_asset_ai_data_with_aggregation_logic>`__
     - Get the original AI data (or aggregated data) of a specified measurement point of a specified device within a certain period.
   * - `Get Asset AI Raw Data <get_asset_ai_raw_data>`__
     - Get the original AI data of a specified measurement point of a specified device within a certain period.
   * - `Get Asset Current Day Electric Power <get_asset_current_day_electric_power>`__
     - Get the accumulated power consumption/production data of a specified device from 00:00 (local time) to current time.
   * - `Get Asset DI Data <get_asset_di_data>`__
     - Get the status (DI) data of a specified device within a certain period.
   * - `Get Asset DI Data Duration <get_asset_di_data_durations>`__
     - Get the duration of different status (DI) data of a specified device within a certain period.
   * - `Get Asset Electric Power Data <get_asset_electric_power_data>`__
     - Get the power consumption/production data of a specified device within a certain period.
   * - `Get Asset Generic Data <get_asset_generic_data>`__
     - Get the generic data of a specified measurement point of a specified device within a certain period.
   * - `Get Asset Latest Data <get_asset_latest_data>`__
     - Get the latest data of all measurement points of a specified device.
   * - `Get Asset Raw Data By Time Range <get_asset_raw_data_by_time_range>`__
     - Get the original data of a specified measurement point of a specified device within a certain period (including AI, DI, and Generic data types).

## Request Method

TSDB Data Service supports both the GET and POST methods:

- GET: The request parameters are included in the request URL, which can be used for requests with less parameters.
- POST: The request parameters are included in the request body, which can be used for requests with long parameters (e.g., when querying data of multiple assets).

<br />

The API documentation provides reference for both the GET and POST methods.

## Common Error Codes

.. list-table::
   :widths: 10 40 50
   :header-rows: 1

   * - Code
     - Error Information
     - Description
   * - 0
     - Success
     - API request is successful.
   * - 400
     - Invalid param error
     - Parameters or parameter values are not valid. For details, refer to the error messages.
   * - 701
     - Sata service ERROR
     - An exception occurs with the data service.
   * - 702
     - An error occurred when execute query in data service.
     - Data query failed due to error of the data service. Please try again later.


<!--end-->
