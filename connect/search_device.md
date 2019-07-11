# Search Device

*Note:  This documentation is in the progress of translation. Thanks for your visit!*

Query the device information.

## Request format

```
https://{apigw-address}/connect-service/v2.1/devices?action=search
```

## Request parameters (URI)

| Name | Location (Path/Query) | Required or Not | Data Type | Description |
|---------------|------------------|----------|-----------|--------------|
| orgId         | Query            | True     | String    | Organization ID which the asset belongs to. [How to get orgId information](/docs/api/en/latest/api_faqs#how-to-get-orgid-information-orgid)                |


## Request parameters (Body)

| Name | Required or Not | Data Type | Description |
|----------------|---------------|--------------------------|---|
| expression| False         | String               | Query expressions, which supports for sql-like query. The fields that are supported for query include: `modelId`, `assetId`, `measurepointId`, `hitRuleId`, `severityId`, `typeId`, `subTypeId`, `contentId`, `eventType`, `eventId` and `tag`. The supported arithmetic operators are "=" and "in", and the logical operator is "and". [How to use expression](/docs/api/en/latest/api_faqs.html#id1)|
| pagination  | False  |Pagination request structure | Random pagination. The default is to sort in descending order by occurTime, and the user can not specify the sorting field. The default pagination size is 10 pages. [Pagination Request Structure] (/docs/api/en/latest/overview.html?highlight=pagination#pagination) |
| projection| False         | Projection structure          | Used to describe the object projection to be returned in the interface request. For details, see [How does projection crop the result set](/docs/api/en/latest/api_faqs.html#how-does-projection-crop-the-result-set)|



## Response parameters

| Name | Data Type | Description |
|-------------|-------------------|-----------------------------|
| data | Device structure                     | Information of a group of sub-devices of the specified page under the gateway. See [Device Structure] (/docs/api/en/latest/connect/search_device.html#id4) |


### Device structure

| Name | Data Type | Description |
|------------------|-----------------------|----------------------------|
| orgId |  String | Organization ID which the asset belongs to |
| assetId  | String         |Asset ID|
| modelId             | String                          | Model ID which the asset belongs to|
| modelIdPath      | String                            | Model ID path                                                               |
| productKey       | String                            | Product Key                                                                |
| productName      | StringI18n                        | Product name                                                                |
| productType      | String                            | Product type                                                                  |
| dataFormat       | String                            | Data format. Custom means that any user-customized data format is supported, while Json means that only the EnOS device protocol formats are supported |
| deviceKey        | String                            | Device key                                                                    |
| deviceName       | StringI18n                        | Device name                                                                   |
| deviceSecret     | String                            | Device connection key                                                             |
| deviceDesc       | String                            | Device description                                                                   |
| timezone         | String                            | Timezone where the device is located                                                               |
| deviceAttributes | Map (Key is of String type and the value is of String type) | Device attributes                                                                 |
| deviceTags       | Map (Key is of String type and the value is of String type) | Device marks                                                                 |
| createTime       | Long                              | Device creation time                                                             |
| status           | String                            | Device status (online, offline, inactive or disable)                         |
| activeTime       | Long                              | Device activation time                                                             |
| lastOnlineTime   | Long                              | Last online time of device                                                       |
| lastOnlineTime   | Long                              | Last offline time of device                                                       |


## Sample 1

### Request sample

```
url:https://{apigw-address}/connect-service/v2.1/devices?action=search&orgId=o15475450989191
method:  POST
requestBody:  {
	"pagination": {
		"pageNo": 2,
		"pageSize": 5
	}
}
```

### Return sample

```json
responseBody:  {
	"code": 0,
	"msg": "OK",
	"requestId": "59ecd409-7baa-4726-ba10-c0bde35ffb09",
	"data": [{
		"orgId": "o15475450989191",
		"assetId": "7u4bfyO0",
		"modelId": "lxctimelooker",
		"modelIdPath": "/lxctimelooker",
		"productKey": "vzzG0GFg",
		"productName": {
			"defaultValue": "lxcpro",
			"i18nValue": {}
		},
		"productType": "Device",
		"dataFormat": "Json",
		"deviceKey": "TeyRhjOnfh",
		"deviceName": {
			"defaultValue": "time2dev11",
			"i18nValue": {}
		},
		"deviceSecret": "iCp1wixMv843ABrYnD3I",
		"deviceDesc": null,
		"timezone": "+09:00",
		"deviceAttributes": {},
		"deviceTags": {},
		"createTime": 1558421750575,
		"status": "offline",
		"activeTime": 1558482329972,
		"lastOnlineTime": 1560743915454,
		"lastOfflineTime": 1560744095454
	}, {
		"orgId": "o15475450989191",
		"assetId": "Fi0HQ8FO",
		"modelId": "AlterTest0615",
		"modelIdPath": "/AlterTest0615",
		"productKey": "gHuxgR8s",
		"productName": {
			"defaultValue": "AlterTest0615_Product",
			"i18nValue": {}
		},
		"productType": "Device",
		"dataFormat": "Json",
		"deviceKey": "325132545",
		"deviceName": {
			"defaultValue": "AlterTest0615",
			"i18nValue": {}
		},
		"deviceSecret": "V2Ny4NTlt40NZDaF3xj5",
		"deviceDesc": null,
		"timezone": "+08:00",
		"deviceAttributes": {},
		"deviceTags": {},
		"createTime": 1560564762147,
		"status": "offline",
		"activeTime": 1560564838673,
		"lastOnlineTime": 1560743931247,
		"lastOfflineTime": 1560743931712
	}, {
		"orgId": "o15475450989191",
		"assetId": "6FytqleL",
		"modelId": "AlterTest0614",
		"modelIdPath": "/AlterTest0614",
		"productKey": "zpFCD7pd",
		"productName": {
			"defaultValue": "AlterTest0614_Product",
			"i18nValue": {}
		},
		"productType": "Device",
		"dataFormat": "Json",
		"deviceKey": "324314123431",
		"deviceName": {
			"defaultValue": "AlterTest0614",
			"i18nValue": {}
		},
		"deviceSecret": "R6wPIKHaMrcwnpzOSZYe",
		"deviceDesc": null,
		"timezone": "+08:00",
		"deviceAttributes": {
			"aaa": 1,
			"76": 0
		},
		"deviceTags": {},
		"createTime": 1560493341919,
		"status": "offline",
		"activeTime": 1560493435761,
		"lastOnlineTime": 1560743930253,
		"lastOfflineTime": 1560743930346
	}, {
		"orgId": "o15475450989191",
		"assetId": "V4TjS0n4",
		"modelId": "AlertTest0613",
		"modelIdPath": "/AAA100/AlertTest0613",
		"productKey": "gTsWB8mX",
		"productName": {
			"defaultValue": "AlertTest0613_Product",
			"i18nValue": {}
		},
		"productType": "Device",
		"dataFormat": "Json",
		"deviceKey": "324132514331",
		"deviceName": {
			"defaultValue": "AlertTest0613",
			"i18nValue": {}
		},
		"deviceSecret": "0u06LivvksMGxtJoSBT5",
		"deviceDesc": null,
		"timezone": "+08:00",
		"deviceAttributes": {
			"aaa": 1,
			"76": 0
		},
		"deviceTags": {},
		"createTime": 1560389949661,
		"status": "offline",
		"activeTime": 1560390227903,
		"lastOnlineTime": 1560743916848,
		"lastOfflineTime": 1560743929003
	}, {
		"orgId": "o15475450989191",
		"assetId": "wjIXsqTQ",
		"modelId": "zcmx---1",
		"modelIdPath": "/zcmx---1",
		"productKey": "J5GKPipa",
		"productName": {
			"defaultValue": "zccp-----1",
			"i18nValue": {}
		},
		"productType": "Device",
		"dataFormat": "Json",
		"deviceKey": "krL0iNa4as",
		"deviceName": {
			"defaultValue": "zccp-----222",
			"i18nValue": {}
		},
		"deviceSecret": "KUiw16CE4A4QTabkt0QN",
		"deviceDesc": null,
		"timezone": "+08:00",
		"deviceAttributes": {
			"timestamp1": 1,
			"float1": 1.0,
			"bool11": false,
			"int1": 1,
			"string1": "1",
			"double1": 1.0,
			"12221": false,
			"array1": [1],
			"stuct1": {
				"int11": 1
			},
			"file1": "ftp://a.com/demo.txt",
			"enum": 1,
			"dete1": "2019-05-06"
		},
		"deviceTags": {},
		"createTime": 1559294746435,
		"status": "inactive",
		"activeTime": 0,
		"lastOnlineTime": 0,
		"lastOfflineTime": 0
	}],
	"pagination": {
		"sortedBy": null,
		"pageNo": 2,
		"pageSize": 5,
		"totalSize": 6511
	}
}
```

