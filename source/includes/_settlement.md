# Settlement

Make a payment by communicating with the card company.

## When making a payment using a token
## When paying with a member ID
If you omit tds_type or send a value other than "0", or the store has not enabled Pre-Authentication, the API will require 3DS2.

```shell
curl --location --request POST 'https://staging-api.swa-pay.com/api/v1/payment' \
--header 'Authorization: eyJhbGciOiJIUzI1NiJ9.eyJpYXQiOjE3MDUzMTU5NDV9.xT3EFN3SC51hORCMEaSDeoA1KEGwGm7cAXdIFQtxr28' \
--header 'Content-Type: application/json' \
--data-raw {
  "id": "644c7d8a-d01d-41c6-a63f-4afd88fe9687",
  "card_id": "9cd378b2-7086-4d69-b245-95b97f84f0da",
  "user_id": "02eecc89-5ac8-4969-9e8f-d183fc8c84a4"
}
```

> The above command returns JSON structured like this:

```json
{
    "id": "644c7d8a-d01d-41c6-a63f-4afd88fe9687",
    "pay_amount": 1200.0,
    "currency": "JPY",
    "customer_id": null,
    "customer_order_id": "20251019_1531",
    "status": "AUTHENTICATING_3DS",
    "update_date": "2025-10-19T08:33:09.913+00:00",
    "create_date": "2025-10-19T08:33:09.913+00:00",
    "pay_method": "0",
    "pay_times": null,
    "order_id_csv": null,
    "actual_payment_date": null,
    "confirmed_at": null,
    "acs": "2",
    "acs_url": "https://simulator.test.fincode.jp/payment/Tds2StubCallback.idPass?transId=86008da1-5d64-4605-bd1f-3dab3c84f6bf&t=a_Kw9Mm5zRTbeCpgCggcYTLA",
    "redirect_url": "https://staging-api.swa-pay.com/api/v1/fincode/secure/authentication/644c7d8a-d01d-41c6-a63f-4afd88fe9687",
    "user_payment": {
        "id": "02eecc89-5ac8-4969-9e8f-d183fc8c84a4",
        "first_name": "hieu",
        "last_name": "taphamkim",
        "email": "hieutaphamkim89+1750@gmail.com",
        "phone": null,
        "affiliate_code": null,
        "display_name": "taphamkim hieu",
        "address": null
    },
    "state": null
}
```

> tds_type = "0" → attempts No-3DS (gateway or risk policy may still require 3DS in rare cases).
If the store has Pre-Authentication enabled and the card was pre-authorized (3DS2) at registration, subsequent payments may proceed with No-3DS (or 3DS2) based on risk routing and your tds_type.

```shell
curl --location --request POST 'https://staging-api.swa-pay.com/api/v1/payment' \
--header 'Authorization: eyJhbGciOiJIUzI1NiJ9.eyJpYXQiOjE3MDUzMTU5NDV9.xT3EFN3SC51hORCMEaSDeoA1KEGwGm7cAXdIFQtxr28' \
--header 'Content-Type: application/json' \
--data-raw {
    "id": "{{order_id}}",
    "card_id": "{{card_id}}",
    "user_id": "02eecc89-5ac8-4969-9e8f-d183fc8c84a4",
    "tds_type": "0"
}

{
    "id": "22be11b0-d075-496d-9bae-615daf730cd1",
    "pay_amount": 1400.0,
    "currency": "JPY",
    "customer_id": null,
    "customer_order_id": "20251019_1731",
    "status": "COMPLETE",
    "update_date": "2025-10-19T08:16:32.526+00:00",
    "create_date": "2025-10-19T08:12:42.377+00:00",
    "pay_method": "0",
    "pay_times": null,
    "order_id_csv": null,
    "actual_payment_date": "2025-10-19T08:16:32.526+00:00",
    "confirmed_at": null,
    "acs": null,
    "acs_url": null,
    "redirect_url": null,
    "user_payment": {
        "id": "02eecc89-5ac8-4969-9e8f-d183fc8c84a4",
        "first_name": "hieu",
        "last_name": "taphamkim",
        "email": "hieutaphamkim89+1750@gmail.com",
        "phone": null,
        "affiliate_code": null,
        "display_name": "taphamkim hieu",
        "address": null 
        },
    "state": null
}

```

> Store Pre-Authentication not enabled

```json
{
    "code": "E0429",
    "message": "Pre-Authentication is not enabled for this store. Please contact an administrator to enable it.",
    "errors": null
}
```

> Card not 3DS-authenticated at registration

```json
{
    "code": "E0430",
    "message": "This card was not 3DS-authenticated at registration.",
    "errors": null
}
```

### HTTP Request

`POST /v1/payment`

Production environment
`https://api.swa-pay.com/api/v1/payment`

Staging environment
`https://staging-api.swa-pay.com/api/v1/payment`

### JSON Object Payload Parameters
| Parameter | Required | Description                                               |
| --------- | -------- | --------------------------------------------------------- |
| id        | true     | Transaction/order ID                                      |
| card_id   | true     | Stored card ID on SWAPay                                  |
| user_id   | true     | Payer’s user ID                                           |
| tds_type  | false    |  "0": Do not use 3D Secure authentication. "2": Use 3D Secure 2.0 authentication (**default**)|


## When making a payment using a card number - No 3DS

```shell
curl --location --request POST 'https://staging-api.swa-pay.com/api/v1/payment' \
--header 'Authorization: meowmeowmeow.' \
--header 'Content-Type: application/json' \
--data-raw '{
    "id": "8405b5f8-0244-4bd5-97cb-748ddeac6b13",
    "card_no": "4100000000000100",
    "expire": "12/25",
    "security_code": "123",
    "holder_name": "LYBIA SOFT"
}'
```

> The above command returns JSON structured like this:

```json
{
    "id": "d1702c31-617a-4d51-afca-d135e7034f8a",
    "pay_amount": 1000.0,
    "currency": "JPY",
    "customer_id": "1000",
    "customer_order_id": "1001",
    "status": "COMPLETE",
    "update_date": null,
    "pay_method": null,
    "pay_times": null
}
```
> Abnormal

```json
{
    "code": "M01004014",
    "message": "Order ID is already part of a transaction requesting settlement",
    "errors": [
        {
            "errInfo": "E01050004",
            "errCode": "E01"
        },
        {
            "errInfo": "M01004014",
            "errCode": "M01"
        }
    ]
}
```

This endpoint will help you to payment for a transaction

### HTTP Request

`POST /v1/payment`

Production environment
`https://api.swa-pay.com/api/v1/payment`

Staging environment
`https://staging-api.swa-pay.com/api/v1/payment`

### JSON Object Payload Parameters

Parameter | Required | Description
--------- | -------- | -----------
id | true | ID of the transaction 
card_no | true | credit card number 
expire | true | Credit card expiration date - MMYY format
security_code | true | security code - The 3- or 4-digit number printed on the card
holder_name | true | Credit card name


## Cancel a payment

```shell
curl --location --request POST 'https://staging-api.swa-pay.com/api/v1/payment_cancel' \
--header 'Authorization: meowmeowmeow.' \
--header 'Content-Type: application/json' \
--data-raw '{
    "id": "048874d9-3029-4c0f-a738-93b16c66d948"
}'
```

> The above command returns JSON structured like this:

```json
{
    "id": "048874d9-3029-4c0f-a738-93b16c66d948",
    "pay_amount": 1000.0,
    "currency": "JPY",
    "customer_id": "1000",
    "customer_order_id": "1001",
    "description": "NFT",
    "consumer_id": null,
    "pay_method": "0",
    "success_url": "https://swapay.co.jp/",
    "cancel_url": "https://swapay.co.jp/",
    "callback_url": "https://149c-123-20-166-241.ap.ngrok.io/gateway/callback",
    "status": "REJECTED",
    "create_date": "2022-08-02T12:57:15.322+00:00",
    "update_date": "2022-08-02T12:57:18.066+00:00",
    "pay_method": null,
    "pay_times": null,
    "consumer_email": null,
    "payment_url": "/gateway/payment/048874d9-3029-4c0f-a738-93b16c66d948"
}
```
> Abnormal

```json
{
    "code": "303",
    "message": "The status of the order does not allow this action",
    "errors": null
}
```

This endpoint will help you to payment for a transaction

### HTTP Request

`POST /v1/payment_cancel`

Production environment
`https://api.swa-pay.com/api/v1/payment_cancel`

Staging environment
`https://staging-api.swa-pay.com/api/v1/payment_cancel`

### JSON Object Payload Parameters

Parameter | Required | Description
--------- | -------- | -----------
id | true | ID of the transaction 


# Settlement - 3DS-2 (support for the GMO Gateway, the FinCode Gateway and the Alpha note gateway)

## 3DS-2 card number

```shell
curl --location --request POST 'https://staging-api.swa-pay.com/api/v1/payment' \
--header 'Authorization: meowmeowmeow.' \
--header 'Content-Type: application/json' \
--data-raw '{
    "id": "79ec92ea-e4fe-4b02-ae3d-b1aa962bae66",
    "card_no": "4100 0000 0000 5000",
    "expire": "1229",
    "security_code": "123",
    "holder_name": "LYBIA SOFT"
}'
```

> The above command returns JSON structured like this:

```json
{
    "pay_amount": 1000.0,
    "currency": "JPY",
    "customer_id": "102",
    "customer_order_id": null,
    "status": "AUTHENTICATING_3DS",
    "update_date": "2025-08-13T07:03:39.080+00:00",
    "create_date": "2025-08-13T07:03:39.080+00:00",
    "pay_method": "0",
    "pay_times": null,
    "order_id_csv": null,
    "actual_payment_date": null,
    "confirmed_at": null,
    "acs": "2",
    "acs_url": "https://simulator.test.fincode.jp/payment/Tds2StubCallback.idPass?transId=63c06889-d237-4bcc-9e7b-dfe4bc05beae&t=a_akfQCPrfR4yazH6cedT1RA",
    "redirect_url": "https://staging-api.swa-pay.com/api/v1/fincode/secure/authentication/79ec92ea-e4fe-4b02-ae3d-b1aa962bae66",
    "user_payment": null,
    "state": null
}
```

This endpoint will help you to start payment for a transaction

### HTTP Request

`POST /v1/payment`

Production environment
`https://api.swa-pay.com/api/v1/payment`

Staging environment
`https://staging-api.swa-pay.com/api/v1/payment`

### JSON Object Payload Parameters

| Parameter            | Type   | Description |
|----------------------|--------|-------------|
| `id`                 | UUID   | ID of the transaction. |
| `pay_amount`         | Double | Amount of the transaction. |
| `currency`           | String | The currency used for payment. Default is `JPY`. |
| `customer_id`        | String | The customer ID in the merchant system. |
| `customer_order_id`  | String | The order ID in the merchant system. |
| `status`             | String | Status of the payment request. |
| `acs`                | String | Indicates whether to use 3D Secure authentication.<br>`0`: Do not use 3D Secure authentication (default).<br>`2`: Use 3D Secure 2.0 authentication. |
| `acs_url`            | String | URL of the 3D Secure authentication page returned directly from the payment gateway. Used only when your system implements the entire 3D Secure authentication process. |
| `redirect_url`       | String | 3D Secure authentication URL provided by Swapay. This URL is customized to simplify integration and can be used as an alternative to `acs_url` if you prefer Swapay to handle part or all of the 3D Secure authentication flow. |
| `pay_method`         | String | Payment method.<br>`0`: Credit card payment. |
| `state`              | String | Payment result status.<br>`1`: Payment successful.<br>`2`: Payment failed.<br>`3`: 3D Secure authentication required.<br>*Only applicable for the Alphanote payment gateway.* |

  

# Settlement - PAYPAY (support for the GMO Gateway and  the FinCode Gateway)

## Payment with PayPay method 

```shell
curl --location --request POST 'https://staging-api.swa-pay.com/api/v1/payment' \
--header 'Authorization: {store_token}' \
--header 'Content-Type: application/json' \
--data-raw '{
    "id": "1c2705ce-4eed-47eb-a753-0e6b0d6c151a",
    "payment_method": "paypay"
}'
```

> The above command returns JSON structured like this:

```json
{
    "id": "1c2705ce-4eed-47eb-a753-0e6b0d6c151a",
    "pay_amount": 2600.0,
    "currency": "JPY",
    "customer_id": null,
    "customer_order_id": "689190",
    "status": "WAITING_FOR_PAYMENT",
    "update_date": "2024-05-27T08:10:47.261+00:00",
    "create_date": "2024-05-27T08:10:47.261+00:00",
    "pay_method": "2",
    "pay_times": null,
    "order_id_csv": null,
    "actual_payment_date": null,
    "confirmed_at": null,
    "acs": null,
    "acs_url": null,
    "redirect_url": "https://staging-api.swa-pay.com/api/v1/gmo/paypay/start/1c2705ce-4eed-47eb-a753-0e6b0d6c151a"
}
```

This endpoint will help you to start payment for a transaction


### HTTP Request

`POST /v1/payment`

Production environment
`https://api.swa-pay.com/api/v1/payment`

Staging environment
`https://staging-api.swa-pay.com/api/v1/payment`

### JSON Object Payload Parameters

Parameter | Required | Description
--------- | -------- | -----------
id | true | ID of the transaction 
payment_method | true | value: paypay
customer_id | false | The customer id on merchant system

### JSON Object Payload Parameters

Parameter | Type | Description
--------- | -------- | -----------
id | UUID | ID of the transaction
pay_amount | Double | Amount of the transaction
currency | String | The currency used for payment. Default is JPY
customer_id | String | The customer id on merchant system
customer_order_id | String | The order id on merchant systems
status | String | Status of Payment request
redirect_url | String | Redirect URL for payment with PayPay
pay_method | String | 2 => (Paypay payment)


# Settlement - LinePay (support for the GMO Gateway)

## Payment with LinePay method 

```shell
curl --location --request POST 'https://staging-api.swa-pay.com/api/v1/payment' \
--header 'Authorization: {store_token}' \
--header 'Content-Type: application/json' \
--data-raw '{
    "id": "09e68717-391a-4b01-87cb-0ccd7305eb8e",
    "payment_method": "linepay"
}'
```

> The above command returns JSON structured like this:

```json
{
    "id": "6cce744b-4122-44e8-992f-2ef6a53e2835",
    "pay_amount": 2600.0,
    "currency": "JPY",
    "customer_id": null,
    "customer_order_id": "3780402",
    "status": "WAITING_FOR_PAYMENT",
    "update_date": "2024-05-28T03:00:44.037+00:00",
    "create_date": "2024-05-28T03:00:44.037+00:00",
    "pay_method": "4",
    "pay_times": null,
    "order_id_csv": null,
    "actual_payment_date": null,
    "confirmed_at": null,
    "acs": null,
    "acs_url": null,
    "redirect_url": "https://staging-api.swa-pay.com/api/v1/gmo/linepay/start/6cce744b-4122-44e8-992f-2ef6a53e2835"
}
```

This endpoint will help you to start payment for a transaction


### HTTP Request

`POST /v1/payment`

Production environment
`https://api.swa-pay.com/api/v1/payment`

Staging environment
`https://staging-api.swa-pay.com/api/v1/payment`

### JSON Object Payload Parameters

Parameter | Required | Description
--------- | -------- | -----------
id | true | ID of the transaction 
payment_method | true | value: paypay
customer_id | false | The customer id on merchant system

### JSON Object Payload Parameters

Parameter | Type | Description
--------- | -------- | -----------
id | UUID | ID of the transaction
pay_amount | Double | Amount of the transaction
currency | String | The currency used for payment. Default is JPY
customer_id | String | The customer id on merchant system
customer_order_id | String | The order id on merchant systems
status | String | Status of Payment request
redirect_url | String | Redirect URL for payment with Linepay
pay_method | String | 4 => (linepay payment)
