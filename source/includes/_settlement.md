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

`POST https://staging-api.swa-pay.com/api/v1/payment`

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
    "acs": "2",
    "acs_url": "https://3c80-2405-4802-9119-ab90-e86d-6d5a-d791-666c.ap.ngrok.io/gateway/3ds/09e68717-391a-4b01-87cb-0ccd7305eb8e/3b79e76d924d7bdd29b10e001e08d500",
    "md": "3b79e76d924d7bdd29b10e001e08d500"
}
```

This endpoint will help you to start payment for a transaction

### HTTP Request

`POST https://staging-api.swa-pay.com/api/v1/payment`

### JSON Object Payload Parameters

Parameter | Required | Description
--------- | -------- | -----------
id | true | ID of the transaction 
acs | true | 2 => (3DS2.0)
acs_url | true | 3DS password input screen URL
md | true | Transaction ID on GMO System


# Settlement - PAYPAY (support for the GMO Gateway and  the FinCode Gateway)

## Payment with PayPay method 

```shell
curl --location --request POST 'https://staging-api.swa-pay.com/api/v1/payment' \
--header 'Authorization: {store_token}' \
--header 'Content-Type: application/json' \
--data-raw '{
    "id": "09e68717-391a-4b01-87cb-0ccd7305eb8e",
    "payment_method": "paypay"
}'
```

> The above command returns JSON structured like this:

```json
{
    "id": "09e68717-391a-4b01-87cb-0ccd7305eb8e",
    "acs": "2",
    "acs_url": "https://3c80-2405-4802-9119-ab90-e86d-6d5a-d791-666c.ap.ngrok.io/gateway/3ds/09e68717-391a-4b01-87cb-0ccd7305eb8e/3b79e76d924d7bdd29b10e001e08d500",
    "md": "3b79e76d924d7bdd29b10e001e08d500"
}
```

This endpoint will help you to start payment for a transaction

### HTTP Request

`POST https://staging-api.swa-pay.com/api/v1/payment`

### JSON Object Payload Parameters

Parameter | Required | Description
--------- | -------- | -----------
id | true | ID of the transaction 
acs | true | 2 => (3DS2.0)
acs_url | true | 3DS password input screen URL
md | true | Transaction ID on GMO System

