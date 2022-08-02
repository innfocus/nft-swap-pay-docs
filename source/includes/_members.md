# Users

## User registration


```shell
curl --location --request POST 'https://nft-swap-test.azurewebsites.net/api/v1/customers' \
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
    "first_name": "Phat",
    "last_name": "Lam",
    "email": "thanhphat@gmail.com",
    "phone": null,
    "address": null
}
```

This endpoint will help you register a user on SWAPAY system.

### HTTP Request

`POST https://nft-swap-test.azurewebsites.net/api/v1/customers`

### JSON Object Payload Parameters

Parameter | Required | Description
--------- | -------- | -----------
customer_id | false | The customer id on merchant system 
first_name | false | The member's first name 
last_name | false | The member's last name 
email | true | The member's email 
phone | true | The member's phone 
address | false | The member's address 
