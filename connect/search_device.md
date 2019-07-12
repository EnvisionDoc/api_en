# Search Device



Query the device information.

## Request Format

```
https://{apigw-address}/connect-service/v2.1/devices?action=search
```

## Request Parameters (URI)

| Name | Location (Path/Query) | Required or Not | Data Type | Description |
|---------------|------------------|----------|-----------|--------------|
| orgId         | Query            | True     | String    | Organization ID which the asset belongs to. [How to get orgId](/docs/api/en/latest/api_faqs#how-to-get-organization-id-orgid-orgid)                |


## Request Parameters (Body)



<table>
            <tr align="left">
                <th>Name</th>
                <th>Required or Not</th>
                <th>Data Tyoe</th>
				<th>Description</th>
            </tr>
            <tr>
                <td>expression</td>
                <td>False</td>
                <td>String</td>
				<td>Query expression. The fields that are supported for query include:<code>productKey</code>, <code>deviceKey</code>, <code>assetId</code>, <code>productType</code>, <code>deviceName</code>, and <code>status</code>
				<ul>
				<li><code>productKey</code>, <code>deviceKey</code>, and <code>assetId</code>: support arithmetic operators "=" and "in";</li>
            	<li><code>productType</code>: supports arithmetic operator "=", valid values are: "Device" and "Gateway";</li>
            	<li><code>deviceName</code>: supports fuzzy inquiry of specified language：
					<ul>
						<li><code>deviceName like ‘xxx’</code>: fuzzy inquiry of default name, Chinese name, and English name;</li>
						<li><code>deviceName.default like ‘xxx’</code>: fuzzy inquiry of default name;</li>
						<li><code>deviceName.zh_CN like ‘xxx’</code>: fuzzy inquiry of Chinese name, if no Chinese name, fuzzy inquiry of default name;</li>
						<li><code>deviceName.en_US like ‘xxx’</code>: fuzzy inquiry of English name, if no English name, fuzzy inquiry of default name</li>
					</ul>
				</li>
				<li><code>status</code>: upports arithmetic operator "=", valid values are: "inactive", "online", "offline", and "disable"</li>
				</ul>
<a href="/docs/api/en/latest/api_faqs.html#how-to-use-expression">How to use expression</a></td>
            </tr>
            <tr>
                <td>pagination</td>
                <td>False</td>
                <td>pagination request structure</td>
				<td>Random pagination. The default is to sort in descending order by <code>occurTime</code>, and the user can not specify the sorting field. The default pagination size is 10 pages. <a href="/docs/api/zh_CN/latest/overview.html#pagination-request-structure">Pagination Request Structure</a></td>
            </tr>
            <tr>
                <td>projection</td>
                <td>False</td>
                <td>Projection structure</td>
				<td>Describe the object projection to be returned in the interface request. For details, see <a href="/docs/api/en/latest/api_faqs.html#how-does-projection-crop-the-result-set">How does projection crop the result set?</a></td>
            </tr>

</table>


## Response Parameters

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

### Request Sample

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

### Return Sample

```json
responseBody:  {
	"code": 0,
	"msg": "OK",
	"requestId": "59ecd409-7baa-4726-ba10-c0bde35ffb09",
	"data": [{
		"orgId": "yourOrgId",
		"assetId": "7u4bfyO0",
		"modelId": "lxctimelooker",
		"modelIdPath": "/lxctimelooker",
		"productKey": "yourProductKey",
		"productName": {
			"defaultValue": "lxcpro",
			"i18nValue": {}
		},
		"productType": "Device",
		"dataFormat": "Json",
		"deviceKey": "yourDeviceKey",
		"deviceName": {
			"defaultValue": "time2dev11",
			"i18nValue": {}
		},
		"deviceSecret": "yourDeviceSecret",
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
		"orgId": "yourOrgId",
		"assetId": "Fi0HQ8FO",
		"modelId": "AlterTest0615",
		"modelIdPath": "/AlterTest0615",
		"productKey": "yourProductKey",
		"productName": {
			"defaultValue": "AlterTest0615_Product",
			"i18nValue": {}
		},
		"productType": "Device",
		"dataFormat": "Json",
		"deviceKey": "yourDeviceKey",
		"deviceName": {
			"defaultValue": "AlterTest0615",
			"i18nValue": {}
		},
		"deviceSecret": "yourDeviceSecret",
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
		"orgId": "yourOrgId",
		"assetId": "6FytqleL",
		"modelId": "AlterTest0614",
		"modelIdPath": "/AlterTest0614",
		"productKey": "yourProductKey",
		"productName": {
			"defaultValue": "AlterTest0614_Product",
			"i18nValue": {}
		},
		"productType": "Device",
		"dataFormat": "Json",
		"deviceKey": "yourDeviceKey",
		"deviceName": {
			"defaultValue": "AlterTest0614",
			"i18nValue": {}
		},
		"deviceSecret": "yourDeviceSecret",
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
		"orgId": "yourOrgId",
		"assetId": "V4TjS0n4",
		"modelId": "AlertTest0613",
		"modelIdPath": "/AAA100/AlertTest0613",
		"productKey": "yourProductKey",
		"productName": {
			"defaultValue": "AlertTest0613_Product",
			"i18nValue": {}
		},
		"productType": "Device",
		"dataFormat": "Json",
		"deviceKey": "yourDeviceKey",
		"deviceName": {
			"defaultValue": "AlertTest0613",
			"i18nValue": {}
		},
		"deviceSecret": "yourDeviceSecret",
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
		"orgId": "yourOrgId",
		"assetId": "wjIXsqTQ",
		"modelId": "zcmx---1",
		"modelIdPath": "/zcmx---1",
		"productKey": "yourProductKey",
		"productName": {
			"defaultValue": "zccp-----1",
			"i18nValue": {}
		},
		"productType": "Device",
		"dataFormat": "Json",
		"deviceKey": "yourDeviceKey",
		"deviceName": {
			"defaultValue": "zccp-----222",
			"i18nValue": {}
		},
		"deviceSecret": "yourDeviceSecret",
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

