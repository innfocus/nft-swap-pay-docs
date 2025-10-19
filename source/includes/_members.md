# Users

## User registration


```shell
curl --location --request POST 'https://staging-api.swa-pay.com/api/v1/customers' \
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

`POST /v1/customers`

Production environment
`https://api.swa-pay.com/api/v1/customers`

Staging environment
`https://staging-api.swa-pay.com/api/v1/customers`

### JSON Object Payload Parameters

Parameter | Required | Description
--------- | -------- | -----------
customer_id | false | The customer id on merchant system 
first_name | false | The member's first name 
last_name | false | The member's last name 
email | true | The member's email. If the member uses the phone number. Then no need for email 
phone | true | The member's phone . If the member uses the mail. Then no need for phone
country_code | false | The member's country code. Default JP
address | false | The member's address 

### Error code list

Error Code | Meaning
---------- | -------
E0010 | Email is already used
E0019 | Customer ID is already used

### User Response Fields

Field | Type | Description
----- | ---- | -------
id | UUID |  User ID on SWAPay System
email | String | Email
first_name | String | First name  
last_name | String | Last name  
phone | String | Phone number
confirmed | Boolean | `true` if the customer's email is confirmed. `false` if the customer's email isn't confirmed  
phone_confirmed_at | DateTime | The time when the phone is confirmed. 
provider | String | `PHONE` if customer is registered with phone number. `EMAIL` if customer is registered with email address   
address | String | Address 
avatar | String | The avatar URL 
create_date  | DateTime | The time when customer is registered

## Get User profile

```shell
curl --location --request GET 'https://staging-api.swa-pay.com/api/v1/customers/b68904c8-cb4b-4685-a7fb-3ee0cd99f5c2' \
--header 'Authorization: meowmeowmeow'
```

> The above command returns JSON structured like this:

```json
{
    "id": "b68904c8-cb4b-4685-a7fb-3ee0cd99f5c2",
    "confirmed": false,
    "phone_confirmed_at": null,
    "username": null,
    "first_name": null,
    "last_name": null,
    "display_name": "lybiasoft@gmail.com",
    "phone": null,
    "address": null,
    "avatar": null,
    "email": "lybiasoft@gmail.com",
    "country_code": null,
    "phone_e164": null,
    "provider": "EMAIL",
    "customer_id": null,
    "create_date": "2022-09-10T23:55:55.003+00:00"
}
```

> Abnormal

```json
{
    "code": "E0208",
    "message": "User not found",
    "errors": null
}
```

This endpoint will help you get a user profile on SWAPAY system.

### HTTP Request

`POST /v1/customers/{id}`

Production environment
`https://api.swa-pay.com/api/v1/customers/{id}`

Staging environment
`https://staging-api.swa-pay.com/api/v1/customers/{id}`

### URL Parameters

Parameter | Description
--------- | -----------
id | The ID of the user

## Update User profile


```shell
curl --location --request POST 'https://staging-api.swa-pay.com/api/v1/customers/9af4f665-9869-4c95-99ca-51d14a32d50f' \
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
    "id": "b68904c8-cb4b-4685-a7fb-3ee0cd99f5c2",
    "confirmed": false,
    "phone_confirmed_at": null,
    "username": null,
    "first_name": "Phat 1",
    "last_name": "Lam",
    "display_name": "Phat 1 Lam",
    "phone": "+81973666666",
    "address": null,
    "avatar": null,
    "email": "lybiasoft@gmail.com",
    "country_code": null,
    "phone_e164": null,
    "provider": "EMAIL",
    "customer_id": null,
    "create_date": "2022-09-10T23:55:55.003+00:00"
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

This endpoint will help you update user profile on SWAPAY system.

### HTTP Request

`POST /v1/customers/{id}`

Production environment
`https://api.swa-pay.com/api/v1/customers/{id}`

Staging environment
`https://staging-api.swa-pay.com/api/v1/customers/{id}`

### URL Parameters

Parameter | Description
--------- | -----------
id | The ID of the user

### JSON Object Payload Parameters

Parameter | Required | Description
--------- | -------- | -----------
first_name | false | The member's first name 
last_name | false | The member's last name 
email | true | The member's email 
phone | true | The member's phone 
address | false | The member's address 

## Re-send verification message


```shell
curl --location --request POST 'https://staging-api.swa-pay.com/api/v1/customers/b68904c8-cb4b-4685-a7fb-3ee0cd99f5c2/resend_verification' \
--header 'Authorization: meowmeowmeow'
```

> The above command returns JSON structured like this:

```json
{
    "id": "b68904c8-cb4b-4685-a7fb-3ee0cd99f5c2",
    "confirmed": false,
    "phone_confirmed_at": null,
    "username": null,
    "first_name": null,
    "last_name": null,
    "display_name": "lybiasoft@gmail.com",
    "phone": null,
    "address": null,
    "avatar": null,
    "email": "lybiasoft@gmail.com",
    "country_code": null,
    "phone_e164": null,
    "provider": "EMAIL",
    "customer_id": null,
    "create_date": "2022-09-10T23:55:55.003+00:00"
}
```

> Abnormal

```json
{
    "code": "E0035",
    "message": "The customer is confirmed",
    "errors": null
}
```

This endpoint will help you resend the verification message to user.

### HTTP Request

`POST /v1/customers/{id}/resend_verification`

Production environment
`https://api.swa-pay.com/api/v1/customers/{id}/resend_verification`

Staging environment
`https://staging-api.swa-pay.com/api/v1/customers/{id}/resend_verification`

### URL Parameters

Parameter | Description
--------- | -----------
id | The ID of the user

## Verify user with phone number

```shell
curl --location --request POST 'https://staging-api.swa-pay.com/api/v1/verify' \
--header 'Content-Type: application/json' \
--data-raw '{
    "phone": "09078115642",
    "country_code": "JP",
    "code": "881495"
}'
```

> The above command returns JSON structured like this:

```json
{
    "id": "9af4f665-9869-4c95-99ca-51d14a32d50f",
    "active": false,
    "confirmed": false,
    "username": null,
    "first_name": null,
    "last_name": null,
    "email": null,
    "phone": "+819078115642",
    "address": null,
    "phone_confirmed_at": "2022-08-13T09:13:33.745+00:00"
}
```

This endpoint will help the customers verify their phone number. SWAPay system will send an OTP code via SMS. The customers need check the new SMS and input OTP.

### HTTP Request

`POST /v1/verify`

Production environment
`https://api.swa-pay.com/api/v1/verify`

Staging environment
`https://staging-api.swa-pay.com/api/v1/verify`

### JSON Object Payload Parameters

Parameter | Required | Description
--------- | -------- | -----------
phone | false | The member's phone number
country_code | false | The member's country code. Default JP
code | true | The OTP code was send vis SMS 

### JSON Object Response

Parameter | Description
--------- | -----------
id | The SWAPay user id
phone | The member's phone number
country_code | The member's country code. Default JP
phone_confirmed_at | The time when the phone is confirmed. 

## Obtain a list of Consumer
```shell
curl --location --request GET '{{server}}/api/v1/store/consumers?page_no=1&page_size=10' \
--header 'Authorization: meowmeowmeow'
The above command returns JSON structured like this:
{
  "data": [
    {
      "id": "02eecc89-5ac8-4969-9e8f-d183fc8c84a4",
      "display_name": "taphamkim hieu",
      "phone": null,
      "email": "hieutaphamkim89+1750@gmail.com",
      "role": "USER",
      "country_code": null,
      "provider": "EMAIL",
      "phone_e164": null,
      "operation_agency": null,
      "merchant": null,
      "owner": { "id": "af40eee0-81ad-4e29-a8ea-87603b3f8282", "display_name": "Merchant" },
      "store": { "id": "6a02b419-c8a4-4e85-bff2-2242686826f9", "store_name": "テスト", "office_name": "155" },
      "customer_id": null,
      "create_date": "2024-01-15T10:52:44.614+00:00",
      "gmo_status": "REGISTERED",
      "delete_flg": null,
      "first_name": "hieu",
      "last_name": "taphamkim",
      "user_name": null,
      "status": "ACTIVE",
      "order_id": null,
      "order_name": null,
      "user_wallet_address": null,
      "honorific_title": null
    },
    {
        "id": "c4a7e68b-c84c-459f-a3ed-3d2137d007e0",
        "display_name": "Ta Pham Kim Hieu",
        "phone": null,
        "email": "hieutaphamkim89+20240523_1@gmail.com",
        "role": "USER",
        "country_code": null,
        "provider": "EMAIL",
        "phone_e164": null,
        "operation_agency": null,
        "merchant": null,
        "owner": {"id": "af40eee0-81ad-4e29-a8ea-87603b3f8282","display_name": "Merchant"},
        "store": {"id": "6a02b419-c8a4-4e85-bff2-2242686826f9","store_name": "テスト","office_name": "155"},
        "customer_id": "hieutaphamkim89+20240527_1302@gmail.com",
        "create_date": "2024-05-23T03:21:54.259+00:00",
        "gmo_status": "REGISTERED",
        "delete_flg": null,
        "first_name": "Hieu",
        "last_name": "Ta Pham Kim",
        "user_name": null,
        "status": "ACTIVE",
        "order_id": null,
        "order_name": null,
        "user_wallet_address": null,
        "honorific_title": null
    },
    {
        "id": "065d6f2b-7310-4e92-b521-7707362c94ae",
        "display_name": null,
        "phone": null,
        "email": null,
        "role": "USER",
        "country_code": null,
        "provider": "CONSUMER",
        "phone_e164": null,
        "operation_agency": null,
        "merchant": null,
        "owner": {"id": "af40eee0-81ad-4e29-a8ea-87603b3f8282","display_name": "Merchant"},
        "store": {
            "id": "6a02b419-c8a4-4e85-bff2-2242686826f9",
            "store_name": "テスト",
            "office_name": "155"},
        "customer_id": "hieutaphamkim89+20240523_2@gmail.com",
        "create_date": "2024-05-23T06:55:11.356+00:00",
        "gmo_status": "REGISTERED",
        "delete_flg": null,
        "first_name": null,
        "last_name": null,
        "user_name": null,
        "status": "NOT_YET",
        "order_id": null,
        "order_name": null,
        "user_wallet_address": null,
        "honorific_title": null
    },
  ],
  "page_no": 1,
  "page_size": 10,
  "total_elements": 3,
  "total_pages": 1,
  "last": true
}
Abnormal

{
  "code": "E0401",
  "message": "Unauthorized",
  "errors": null
}
This endpoint returns a paginated list of consumers that belong to the current store context.
```
### HTTP Request
`GET /v1/store/consumers`
Production environment
`https://api.swa-pay.com/api/v1/store/consumers`

Staging environment
`https://staging-api.swa-pay.com/api/v1/store/consumers`

Query Parameters
### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
page_no | 1 | 
page_size | 10 | 
keyword | | Keyword to search consumers by user_id, email, phone (and related identifiers). Partial match supported.

### Consumer Response Fields
| Field               | Type     | Description                                              |
| ------------------- | -------- | -------------------------------------------------------- |
| id                  | UUID     | Consumer ID on SWAPay                                    |
| display_name        | String   | Display name (nullable)                                  |
| phone               | String   | Phone number (nullable)                                  |
| email               | String   | Email (nullable)                                         |
| role                | String   | User role (e.g., `USER`)                                 |
| country_code        | String   | Country code (e.g., `JP`)                                |
| provider            | String   | Registration provider (`EMAIL`, `PHONE`, `CONSUMER`)     |
| phone_e164          | String   | E.164 formatted phone (nullable)                         |
| owner               | Object   | Owner info `{ id, display_name }`                        |
| store               | Object   | Store info `{ id, store_name, office_name }`             |
| customer_id         | String   | Customer ID on merchant system (nullable)                |
| create_date         | DateTime | Created time (ISO-8601)                                  |
| gmo_status          | String   | GMO registration status (`REGISTERED`, `NOT_REGISTERED`) |
| status              | String   | Consumer status (`ACTIVE`, `NOT_YET`, …)                 |
| order_id            | String   | Latest order ID (nullable)                               |
| order_name          | String   | Latest order name/label (nullable)                       |
| user_wallet_address | String   | Wallet address (nullable)                                |
| honorific_title     | String   | Honorific title (nullable)                               |
| delete_flg          | Boolean  | Deleted flag (nullable)                                  |
| first_name          | String   | First name (nullable)                                    |
| last_name           | String   | Last name (nullable)                                     |
| user_name           | String   | Username (nullable)                                      |

