# Settlement - No 3DS

Make a payment by communicating with the card company.

## When making a payment using a token

## When paying with a member ID

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

`POST https://staging-api.swa-pay.com/api/v1/payment`

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

`POST https://staging-api.swa-pay.com/api/v1/payment_cancel`

### JSON Object Payload Parameters

Parameter | Required | Description
--------- | -------- | -----------
id | true | ID of the transaction 

# Settlement - 3DS-2 (support for the GMO Gateway and  the FinCode Gateway)

## 3DS-2 card number

```shell
curl --location --request POST 'https://staging-api.swa-pay.com/api/v1/payment' \
--header 'Authorization: meowmeowmeow.' \
--header 'Content-Type: application/json' \
--data-raw '{
    "id": "09e68717-391a-4b01-87cb-0ccd7305eb8e",
    "card_no": "4100000000000100",
    "expire": "12/25",
    "security_code": "123",
    "holder_name": "LYBIA SOFT"
}'
```

> The above command returns JSON structured like this:

```json
{
    "id": "09e68717-391a-4b01-87cb-0ccd7305eb8e",
    "pay_method": "0",
    "acs": "2",
    "acs_url": "https://3c80-2405-4802-9119-ab90-e86d-6d5a-d791-666c.ap.ngrok.io/gateway/3ds/09e68717-391a-4b01-87cb-0ccd7305eb8e/3b79e76d924d7bdd29b10e001e08d500",
    "md": "3b79e76d924d7bdd29b10e001e08d500"
}
```

This endpoint will help you to start payment for a transaction

### HTTP Request

`POST https://staging-api.swa-pay.com/api/v1/payment`

### JSON Object Payload Parameters

Parameter | Type | Description
--------- | -------- | -----------
id | UUID | ID of the transaction 
acs | String | 2 => (3DS2.0)
acs_url | String | 3DS password input screen URL
md | String | Transaction ID on GMO System
pay_method | String | 0 => (Credit card payment)


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

`POST https://staging-api.swa-pay.com/api/v1/payment`

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

`POST https://staging-api.swa-pay.com/api/v1/payment`

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
