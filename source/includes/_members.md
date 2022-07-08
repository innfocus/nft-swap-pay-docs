# Members

## Membership registration


```shell
curl --location --request POST 'https://nft-swap-test.azurewebsites.net/api/v1/payment/member' \
--header 'Authorization: meowmeowmeow' \
--header 'Content-Type: application/json' \
--data-raw '{
    "customer_id": "{{customer_id}}"
}'
```

> The above command returns JSON structured like this:

```json
{
    "id": "88ff14fb-d3ea-4537-9009-9596a5c9052d",
    "customer_id": "thanhphat",
    "name": null,
    "email": null,
    "phone": null,
    "address": null,
    "delete_flag": "0"
}
```

This endpoint will help you register a member on SWAPAY system.

### HTTP Request

`POST https://nft-swap-test.azurewebsites.net/api/v1/payment/member`

### JSON Object Payload Parameters

Parameter | Required | Description
--------- | -------- | -----------
customer_id | true | The customer id on merchant system 
name | false | The member's name 
email | false | The member's email 
phone | false | The member's phone 
address | false | The member's address 
