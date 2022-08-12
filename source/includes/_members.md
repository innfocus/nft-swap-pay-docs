# Users

## User registration


```shell
curl --location --request POST 'https://nft-swap-test.azurewebsites.net/api/v1/customers' \
--header 'Authorization: meowmeowmeow' \
--header 'Content-Type: application/json' \
--data-raw '{
    "phone": "+81973666666",
    "email": "thanhphat@gmail.com",
    "first_name": "Phat",
    "last_name": "Lam"
}'
```

> The above command returns JSON structured like this:

```json
{
    "id": "9b377f6c-6b83-42ac-866a-5a9a9171ca88",
    "active": false,
    "confirmed": false,
    "username": null,
    "first_name": "Phat",
    "last_name": "Lam",
    "email": "thanhphat@gmail.com",
    "phone": "+81973666666",
    "address": null
}
```

> Abnormal

```json
{
    "code": "E0010",
    "message": "Email is already used",
    "errors": null
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

### Error code list

Error Code | Meaning
---------- | -------
E0010 | Email is already used
E0019 | Customer ID is already used

## User Response Fields

Field | Type | Description
----- | ---- | -------
id | UUID |  User ID on SWAPay System
email | String | Email
first_name | String | First name  
last_name | String | Last name  
phone | String | Phone number
address | String | Address 
avatar | String | The avatar URL 
update_date | DateTime |   
create_date  | DateTime | 

## Update User profile


```shell
curl --location --request POST 'https://nft-swap-test.azurewebsites.net/api/v1/customers/9af4f665-9869-4c95-99ca-51d14a32d50f' \
--header 'Authorization: meowmeowmeow' \
--header 'Content-Type: application/json' \
--data-raw '{
    "phone": "+81973666666",
    "email": "thanhphat@gmail.com",
    "first_name": "Phat 1",
    "last_name": "Lam"
}'
```

> The above command returns JSON structured like this:

```json
{
    "id": "9af4f665-9869-4c95-99ca-51d14a32d50f",
    "active": false,
    "confirmed": false,
    "username": null,
    "first_name": "Phat 1",
    "last_name": "Lam",
    "email": "thanhphat@gmail.com",
    "phone": "+81973666666",
    "address": null
}
```

> Abnormal

```json
{
    "code": "E0010",
    "message": "Email is already used",
    "errors": null
}
```

This endpoint will help you register a user on SWAPAY system.

### HTTP Request

`POST https://nft-swap-test.azurewebsites.net/api/v1/customers/{id}`

### URL Parameters

Parameter | Description
--------- | -----------
id | The ID of the order

### JSON Object Payload Parameters

Parameter | Required | Description
--------- | -------- | -----------
first_name | false | The member's first name 
last_name | false | The member's last name 
email | true | The member's email 
phone | true | The member's phone 
address | false | The member's address 