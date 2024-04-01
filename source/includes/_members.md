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

`POST https://staging-api.swa-pay.com/api/v1/customers`

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

## User Response Fields

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

`POST https://staging-api.swa-pay.com/api/v1/customers/{id}`

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

`POST https://staging-api.swa-pay.com/api/v1/customers/{id}`

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

`POST https://staging-api.swa-pay.com/api/v1/customers/{id}/resend_verification`

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

`POST https://staging-api.swa-pay.com/api/v1/verify`

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