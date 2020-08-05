# Machine Learning Forecast

Get the predition results of the deployed machine learning algorithm model.

For information about deploying algorithm models, see [Algorithm Model Hosting](/docs/offline-data/en/2.1.0/model_deployment/index.html).

## Request Format

```
POST https://{apigw-address}/ml-service/v1.0/forecasts?action=run
```

## Request Parameters (URI)

.. list-table::
   :widths: 15 25 15 15 30
   :header-rows: 1

   * - Name
     - Location (Path/Query)
     - Mandatory/Optional
     - Data Type
     - Description
   * - orgId
     - Query
     - Mandatory
     - String
     - The organization ID which the user belongs to. `How to get orgId >> </docs/api/en/2.1.0/api_faqs#id-orgid-orgid>`__
   * - serviceId
     - Query
     - Mandatory
     - String
     - The service ID that is generated after deploying the algorithm model. `How to get serviceId >> </docs/offline-data/en/2.1.0/model_deployment/managing_deployment.html>`__


## Request Parameters (Body)

.. list-table::
   :widths: 20 20 20 40
   :header-rows: 1

   * - Name
     - Mandatory/Optional
     - Data Type
     - Description
   * - parameters
     - Mandatory
     - String
     - The business parameters for the algorithm model in JSON format. The parameters and values must match with the requirements of the model.


## Response Parameters

.. list-table::
   :widths: 20 30 50
   :header-rows: 1

   * - Name
     - Data Type
     - Description
   * - data
     - Struct
     - The returned prediction results in JSON format. Data type of the results can be basic data types, complex types, and array.


## Samples

### Request Sample

```json
url: https://{apigw-address}/ml-service/v1.0/forecasts?action=run&orgId=yourOrgId&serviceId=f40fbb09-ce20-463f-bb18
method: POST
requestBody:
{
  "parameters": {
    "ColumnNames": [
      "age",
      "workclass",
      "fnlwgt",
      "education",
      "education-num",
      "marital-status",
      "occupation",
      "relationship",
      "race",
      "sex",
      "capital-gain",
      "capital-loss",
      "hours-per-week",
      "native-country"
    ],
    "Values": [
      [
        "0",
        "value",
        "0",
        "value",
        "0",
        "value",
        "value",
        "value",
        "value",
        "value",
        "0",
        "0",
        "0",
        "value"
      ],
      [
        "0",
        "value",
        "0",
        "value",
        "0",
        "value",
        "value",
        "value",
        "value",
        "value",
        "0",
        "0",
        "0",
        "value"
      ]
    ]
  }
}
```

### Return Sample

```json
{
  "status": 0,
  "msg": "Success",
  "data": {
        "ColumnNames": [
          "Scored Labels",
          "Scored Probabilities"
        ],
        "ColumnTypes": [
          "String",
          "Numeric"
        ],
        "Values": [
          [
            "value",
            "0"
          ],
          [
            "value",
            "0"
          ]
        ]
  }
}
```
