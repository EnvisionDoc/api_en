# Search Asset Path

*Note:  This documentation is in the progress of translation. Thanks for your visit!*

Query the eligible path on the asset tree. A path is a complete path from a superior asset node to a subordinate asset node, and can contain intermediate asset nodes.

## Request format

```
https://{apigw-address}/asset-tree-service/v2.1/asset-
paths?action=search
```

## Request parameters (URI)

| Name | Location (Path/Query) | Required or Not | Data Type | Description |
|---------------|------------------|----------|-----------|--------------|
| orgId         | Query            | true     | String    | Organization ID which the asset belongs to. [How to get orgId information](/docs/api/en/latest/api_faqs#how-to-get-orgid-information-orgid)                |
| treeId          | Query            | true     | String    | Asset tree ID |


## Request parameters (Body)

| Name | Required or Not | Data Type | Description |
|-----------------|---------------|-------------------|-----|
| pagination| false         |  Pagination request structure | Used to describe paging requirements in an interface request. By default, it is in the first page and the pagination size is 100. See [Pagination Request Structure](/docs/api/en/latest/overview.html?highlight=pagination#pagination)  |
| from | false         | From-to structure       | Represents the starting point condition of the asset path. If not provided, it represents the root node of the asset tree. See [From-to Structure](/docs/api/en/latest/asset_tree/search_asset_path.html#from-to-from-to-struc).                         |
| to            | false         | From-to structure           | Represents the ending point condition of the asset path. If not provided, it represents the child/leaf node of the asset tree. See [From-to Structure](/docs/api/en/latest/asset_tree/search_asset_path.html#from-to-from-to-struc) |
| projection| false         | String Array         | Used to describe the object projection to be returned in the interface request. Only eligible fields are returned for eligible searches, and all fields are returned by default if no search criterion is set. For details, see [How does projection crop the result set](/docs/api/en/latest/api_faqs.html#how-does-projection-crop-the-result-set)|
| pathProjection| false         | String                | It may be COMPLETE or END_NODE_ONLY. COMPLETE represents each asset node on the return path, which is set as COMPLETE by default; END_NODE_ONLY means only the start and end points of the path are returned  |


### From-to structure <from_to_struc>

| Name | Required or Not | Data Type | Description |
|-----------|---------------|----|-----------------------|
| rootModelIds| false   | String Array         | Root model id. You should provide multiple root model IDs if you want to query multiple root models  |
| modelIds   | false   | String Array         | Model ID which the asset belongs to. You should provide the list of multiple model IDs if you want to query multiple models. [How to get modelId information](/docs/api/en/latest/api_faqs.html#how-to-get-modeid-information-modeid)|
| assetIds        | false     | Array        | Asset ID, which supports querying multiple assets; multiple asset IDs are separated by commas. [How to Get assetId Information](/docs/api/en/latest/api_faqs.html#how-to-get-assetid-information-assetid) |



## Response parameters

| Name | Data Type | Description |
|-----------|------------------|------------------|
| assets     | Map  (Key is of String type, and the Value is of Asset type)| Asset data on the path  |
| assetPaths | String Array Array             | When the `pathProjection` parameter is COMPLETE, each of the String Arrays is the ID of each asset from the start node to the end node on the path, and the length is greater than or equal to 2.  When the `pathProjection` parameter is END_NODE_ONLY, each of the String Arrays is the asset IDs of the start node and the end node of the path, and the length is fixed at 2.  |


### Asset structure

| Name | Data Type | Description |
|------------------|-------------------|----------------------------------------|
| assetId     | String            | Asset ID               |
| name        | StringI18n  | Name of each language for this asset |
| description | String | Asset description|
| attributes  | Map               | Attributes of the model which the asset belongs to                  |
| timezone   | String            | Timezone                                   |
| modelId    | String            | Model ID which the asset belongs to |
| modelIdPath | String            | Model ID path                             |
| tags        | Tag structure         | User-customized tags                         |



## Sample 1

### Request sample

```
POST
https://{apigw-address}/asset-tree-service/v2.1/asset-paths?treeId=Ek72W8bS&action=search&orgId=1c499110e8800000
{
"pagination":{
"pageNo":1,
"pageSize":10
},
"projection":[
"assets.*.attributes",
"assetPaths"
]
} 
```

### Return sample

```json
{
    "code": 0,
    "msg": "OK",
    "requestId": "381ffc90-ee96-45a9-bbf4-8f82efed9823",
    "data": {
        "assets": {
            "rzjwQAHU": {
                "attributes": {
                    "starsystem": "sss",
                    "de001": 123
                }
            },
            "iQFjlwoH": {
                "attributes": {
                    
                }
            },
            "sDx0Uk2Z": {
                "attributes": {
                    
                }
            },
            "4uR3ZsqP": {
                "attributes": {
                    
                }
            }
        },
        "assetPaths": [
            [
                "4uR3ZsqP",
                "rzjwQAHU",
                "sDx0Uk2Z"
            ],
            [
                "4uR3ZsqP",
                "iQFjlwoH"
            ]
        ]
    },
    "pagination": {
        "sortedBy": null,
        "pageNo": 1,
        "pageSize": 10,
        "totalSize": 2
    }
}
```

## Sample 2

### Request sample

```
POST
https://{apigw-address}/asset-tree-service/v2.1/asset-paths?treeId=Ek72W8bS&action=search&orgId=1c499110e8800000
{
    "pagination": {
        "pageNo": 1,
        "pageSize": 10
    },
    "from": {
        "modelIds": [
            "extend_model"
        ]
    },
    "to": {
        "assetIds": [
            "MkblvAJ5"
        ]
    }
}
```

### Return sample 

```json
{
    "code": 0,
    "msg": "OK",
    "requestId": "94347fc1-4b3c-447b-b542-03fa68a1a88f",
    "data": {
        "assetPaths": [
            [
                "DWJdfX3D",
                "MkblvAJ5"
            ]
        ],
        "assets": {
            "DWJdfX3D": {
                "inValid": false,
                "assetId": "DWJdfX3D",
                "modelId": "extend_model",
                "modelIdPath": "/copy_model/extend_model",
                "name": {
                    "defaultValue": "hahha",
                    "i18nValue": {
                        "en_US": "hahha"
                    }
                },
                "timezone": "+09:00",
                "description": "eeeeee",
                "label": "1",
                "attributes": {
                    "invType": 1,
                    "capacity": 5.0
                },
                "tags": {
                    
                }
            },
            "MkblvAJ5": {
                "inValid": false,
                "assetId": "MkblvAJ5",
                "modelId": "planet",
                "modelIdPath": "/planet",
                "name": {
                    "defaultValue": "lkkkkk",
                    "i18nValue": {
                        "en_US": "lkkkkk"
                    }
                },
                "timezone": "+08:00",
                "description": "huyyyyy",
                "label": "1",
                "attributes": {
                    "starsystem": "yyyy",
                    "de001": 123
                },
                "tags": {
                    
                }
            }
        }
    },
    "pagination": {
        "sortedBy": null,
        "pageNo": 1,
        "pageSize": 10,
        "totalSize": 1
    }
}
```