# Update Device



Update devices. The `IsPathcUpdate` is taken as true in the update mode. The `assetId` (or `productKey` and `deviceKey`) is the request field, and other fields are updat fields.

## Request Format

```
https://{apigw-address}/connect-service/v2.1/devices?action=update
```

## Request Parameters (URI)

.. note:: In the following non-required fields, you must provide ``assetId`` or a combination of ``productKey`` and ``deviceKey`` to specify the device.

>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>


| Name | Location (Path/Query) | Required or Not | Data Type | Description |
|---------------|------------------|----------|-----------|--------------|
| orgId         | Query            | True     | String    | Organization ID which the asset belongs to. [How to get orgId>>](/docs/api/en/2.0.9/api_faqs#how-to-get-organization-id-orgid-orgid)                |
| assetId  | Query          | False      | String        | Asset ID. [How to get assetId>>](/docs/api/en/2.0.9/api_faqs.html#how-to-get-asset-id-assetid-assetid) |
| productKey | Query         | False      | String         | Product Key     |
| deviceKey | Query         | False     | String          | Device Key         |


## Request Parameters (Body)

| Name | Required or Not | Data Type | Description |
|----------------|---------------|--------------------------|---|
|timezone | True          | String         | Timezone where the device to be updated is located     |
| deviceName | True          | StringI18n | Name of the device to be updated, see [Internationalized name struct>>](/docs/api/en/2.0.9/api_faqs.html#internationalized-name-struct)         |
| deviceAttributes | False         | Map       | Attributes of the device to be updated         |
| deviceTags   | False         | Map (Key is of String type and the value is of String type)    | Tags of the device to be updated |
| deviceDesc  | False         | String    | Description of the device to be updated     |




## Response Parameters

| Name | Data Type | Description |
|-------------|-------------------|-----------------------------|
| data |    String        | (Null) |





## Sample 1

### Request Sample

```
url:https://{apigw-address}/connect-service/v2.1/devices?action=update&orgId=o15475450989191&assetId=9HhK0YxX
method:  POST
requestBody:  {
	"deviceTags": {
		"test": "test for tags"
	},
	"deviceAttributes": {
		"int11": 617
	},
	"deviceName": {
		"defaultValue": "testforname",
		"i18nValue": {}
	},
	"deviceDesc": "test for updatedevice"
}
```

### Return Sample

```json
responseBody:  {
	"code": 0,
	"msg": "OK",
	"requestId": "0d61752e-0633-4846-abb1-b6fb39801a5f",
	"data": ""
}
```

