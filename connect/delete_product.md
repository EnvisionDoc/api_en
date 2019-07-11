# Delete Product



Delete products.

## Request format

```
https://{apigw-address}/connect-service/v2.1/products?action=delete
```

## Request parameters (URI)

| Name | Location (Path/Query) | Required or Not | Data Type | Description |
|---------------|------------------|----------|-----------|--------------|
| orgId         | Query            | true     | String    | Organization ID which the asset belongs to. [How to get orgId information](/docs/api/en/latest/api_faqs#how-to-get-orgid-information-orgid)                |
| productKey         | Query            | true     | String    | Product Key |




## Response parameters

| Name | Data Type | Description |
|-------------|---------------------------|-----------------------------|
| data | String                           | Key of the deleted product               |


## Error codes

| Code| Data Type | Description |
|-------------|-----------------------------------|-----------------------------|
| 11651|                       |Productkey does not exist              |
| 11619|                       |There are devices under the deleted product             |

## Sample 1

### Request sample

```
POST:  /connect-service/v2.1/products?action=delete&orgId=xxx&productKey=xxx
```

### Return sample

```json
{
	"code":0,
	"msg":"OK",
	"requestId":"ef6a7fbb-0834-45fb-b1d4-6bd2dc25796f",
	"data":"atC41UIe"
}

```

