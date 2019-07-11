# Update Device

*Note:  This documentation is in the progress of translation. Thanks for your visit!*

Update devices. The `IsPathcUpdate` is taken as true in the update mode. The `assetId` (or `productKey` and `deviceKey`) is the request field, and other fields are update fields.

## Request format

```
https://{apigw-address}/connect-service/v2.1/devices?action=update
```

## Request parameters (URI)

Note: In the following non-mandatory fields, you must provide a combination of `assetId` or `productKey` and `deviceKey` to specify the device.

| Name | Location (Path/Query) | Required or Not | Data Type | Description |
|---------------|------------------|----------|-----------|--------------|
| orgId         | Query            | True     | String    | Organization ID which the asset belongs to. [How to get orgId information](/docs/api/en/latest/api_faqs#how-to-get-orgid-information-orgid)                |
| assetId  | Query          | False      | String        | Asset ID, which supports querying multiple assets; multiple asset IDs are separated by commas. [How to get assetId information](/docs/api/en/latest/api_faqs.html#how-to-get-assetid-information-assetid) |
| productKey | Query         | False      | String         | Product Key      |
| deviceKey | Query         | False     | String          | Device key          |


## Request parameters (Body)

| Name | Required or Not | Data Type | Description |
|----------------|---------------|--------------------------|---|
|timezone | True          | String         | Timezone where the device to be updated is located     |
| deviceName | True          | StringI18n | Name of the device to be updated         |
| deviceAttributes | False         | Map       | Attributes of the device to be updated         |
| deviceTags   | False         | Map (Key is of String type and the value is of String type)    | Tags of the device to be updated |
| deviceDesc  | False         | String    | Description of the device to be updated     |




## Response parameters

| Name | Data Type | Description |
|-------------|-------------------|-----------------------------|
| data |    String        | (Null) |





## Sample 1

### Request sample

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
	}
	"deviceDesc": "test for updatedevice"
}
```

### Return sample

```json
responseBody:  {
	"code": 0,
	"msg": "OK",
	"requestId": "0d61752e-0633-4846-abb1-b6fb39801a5f",
	"data": ""
}
```

