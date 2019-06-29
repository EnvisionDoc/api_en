# Search Asset Path

*Note: This documentation is in the progress of translation. Thanks for your visit!*

查询资产树上符合条件的路径，路径是从一个上级资产节点到一个下级资产节点的完整路径，可以包含中间经过的资产节点。

## 请求格式

```
https://{apigw-address}/asset-tree-service/v2.1/asset-
paths?action=search
```

## 请求参数（URI）

| 名称          | 位置（Path/Query） | 是否必须 | 数据类型 | 描述      |
|---------------|------------------|----------|-----------|--------------|
| orgId         | Query            | true     | String    | 资产所属的组织ID。[如何获取orgId信息](/docs/api/en/latest/api_faqs#orgid-orgid)  |
| treeId          | Query            | true     | String    | 资产树ID |


## 请求参数（Body）

| 名称          | 是否必须 | 数据类型 | 描述      |
|-----------------|---------------|-------------------|-----|
| pagination| false         |Pagination请求结构体  | 用于在接口请求中描述分页要求。默认第一页，分页大小为100条记录，见[Pagination请求结构体](/docs/api/en/latest/overview.html?highlight=pagination#pagination)   |
| from | false         | From-to结构体       | 表示资产路径的起始点条件。如果不提供，则表示资产树的根节点。[参见From-to结构体](/docs/api/en/latest/asset_tree/search_asset_path.html#from-to-from-to-struc)。                        |
| to            | false         | From-to结构体         | 表示资产路径的终止点条件。如果不提供，则表示资产树的叶子节点。[参见From-to结构体](/docs/api/en/latest/asset_tree/search_asset_path.html#from-to-from-to-struc) |
| projection| false         | String Array         | 用于在接口请求中描述待返回的对象projection。对于符合条件的搜索仅返回符合条件的字段，不设置则默认返回全部fields。详见[projection参数如何对结果集做裁剪](/docs/api/en/latest/api_faqs.html#projection)|
| pathProjection| false         | String                | 可填COMPLETE、END_NODE_ONLY。COMPLETE表示返回路径上的每个资产节点，默认为COMPLETE；END_NODE_ONLY表示只返回路径的起始点和终结点  |


### From-to结构体<from_to_struc>

| 名称       | 是否必须  | 数据类型 | 描述      |
|-----------|---------------|----|-----------------------|
| rootModelIds| false   | String Array         | 根模型id，如果希望查询多个根模型就提供多个根模型id  |
| modelIds   | false   | String Array         | 资产所属模型ID。如果想查询多个模型，就提供多个模型ID组成的List。[如何获取modelId信息](/docs/api/en/latest/api_faqs.html#modeid-modeid)  |
| assetIds    | false          | Array          | 资产ID，支持查询多个资产，多个资产ID之间用英文逗号隔开。[如何获取assetId信息](/docs/api/en/latest/api_faqs.html#assetid-assetid) |



## 响应参数

| 名称 |数据类型  | 描述 |
|-----------|------------------|------------------|
| assets     | Map（Key为String，Value为Asset） | 路径上的资产数据  |
| assetPaths | String Array Array             | 当`pathProjection`参数为COMPLETE时，其中每一个String Array为路径上起始到终止节点的每个资产Id，长度大于等于2。 当`pathProjection`参数为END_NODE_ONLY时，其中每一个String Array为路径的起始与终止节点的资产Id，长度固定为2。 |


### Asset结构体

| 名称 |数据类型  | 描述 |
|------------------|-------------------|----------------------------------------|
| assetId     | String            | 资产ID               |
| name        | StringI18n  | 该资产的各语言名称 |
| description | String            | 资产描述                               |
| attributes  | Map               | 资产所属的模型属性                  |
| timezone   | String            | 时区                                   |
| modelId    | String            | 资产所属模型ID |
| modelIdPath | String            | 模型id路径                             |
| tags        | Tag结构体         | 用户自定义标签                         |



## 示例 1

### 请求示例

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

### 返回示例

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

## 示例 2

### 请求示例

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

### 返回示例 

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