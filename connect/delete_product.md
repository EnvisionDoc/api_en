# Delete Product



Delete products.

## Request Format

```
https://{apigw-address}/connect-service/v2.1/products?action=delete
```

## Request Parameters (URI)

| Name | Location (Path/Query) | Required or Not | Data Type | Description |
|---------------|------------------|----------|-----------|--------------|
| orgId         | Query            | true     | String    | Organization ID which the asset belongs to. [How to get orgId](/docs/api/en/latest/api_faqs#how-to-get-organization-id-orgid-orgid)                |
| productKey         | Query            | true     | String    | Product Key |




## Response Parameters

| Name | Data Type | Description |
|-------------|---------------------------|-----------------------------|
| data | String                           | Key of the deleted product               |


## Error Codes

| Code| Data Type | Description |
|-------------|-----------------------------------|-----------------------------|
| 11651|                       |Productkey does not exist              |
| 11619|                       |There are devices under the deleted product             |

## Sample 1

### Request Sample

```
POST:  /connect-service/v2.1/products?action=delete&orgId=xxx&productKey=xxx
```

### Return Sample

```json
{
	"code":0,
	"msg":"OK",
	"requestId":"ef6a7fbb-0834-45fb-b1d4-6bd2dc25796f",
	"data":"atC41UIe"
}

```

