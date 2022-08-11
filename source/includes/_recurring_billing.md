# Recurring billing

## Create a new Recurring billing


```shell
curl --location --request POST 'https://nft-swap-test.azurewebsites.net/api/v1/store/recurring_billing' \
--header 'Authorization: meowmeowmeow' \
--header 'Content-Type: application/json' \
--data-raw '{
    "pay_amount": 1000,
    "pay_amount_in_month": 700,
    "currency": "JPY",
    "date_payment": "2022-08-09T17:00:00.000Z",
    "date_start": "2022-08-01T17:00:00.000Z"
    "description": "Recurring Billing",
    "success_url": "https://swapay.co.jp/",
    "callback_url": "https://swapay.co.jp/",
    "cancel_url": "https://swapay.co.jp/"
}'

```

> The above command returns JSON structured like this:

```json
{
    "id": "3e8cba26-c349-49ca-b2e7-4416577994f2",
    "pay_amount": 700.0,
    "pay_next_month": 1000.0,
    "currency": "JPY",
    "customer_id": null,
    "customer_order_id": null,
    "description": "Recurring Billing",
    "consumer_id": null,
    "store": {
        "id": "eba99e3f-84bc-4b92-a215-e0289a5fdcb2",
        "store_name": "NFT SWAP STORE",
        "office_name": "NFT SWAP STORE"
    },
    "merchant": {
        "id": "af40eee0-81ad-4e29-a8ea-87603b3f8282",
        "display_name": "merchant@nft-swapay.com"
    },
    "success_url": null,
    "cancel_url": null,
    "callback_url": null,
    "status": "WAITING_FOR_PAYMENT",
    "user_create": null,
    "create_date": "2022-08-11T22:57:07.625+00:00",
    "monthly_payment_date": null,
    "user_update": null,
    "update_date": "2022-08-11T22:57:07.625+00:00",
    "payment_url": "https://nft-swap-test.azurewebsites.net/gateway/payment/3e8cba26-c349-49ca-b2e7-4416577994f2",
    "pay_method": null,
    "pay_times": null,
    "consumer_email": null,
    "user_id": null,
    "subscribe": {
        "id": "21eb7788-45b3-428f-856a-440ba060ce38",
        "description": "Recurring Billing",
        "pay_amount": 1000.0,
        "pay_amount_in_month": 700.0,
        "currency": "JPY",
        "customer_id": null,
        "status": "WAITING_FOR_PAYMENT",
        "date_payment": "2022-08-11T22:57:07.538+00:00",
        "date_start": "2022-08-01T10:00:00.000+00:00",
        "date_end": null,
        "date_cancel": null,
        "user_create": null,
        "create_date": "2022-08-11T22:57:07.538+00:00",
        "user_update": null,
        "update_date": "2022-08-11T22:57:07.538+00:00"
    }
}
```

> Abnormal

```json
{
    "code": "101",
    "message": "Missing amount",
    "errors": null
}
```

This endpoint will help you to start a recurring transaction

### HTTP Request

`POST {{server}}/api/v1/store/recurring_billing`

### JSON Object Payload Parameters

Parameter | Type  | Required | Description
--------- | ----- | -------- | -----------
pay_amount | Double | true | Recurring payment amount 
pay_amount_in_month | Double | true | The amount paid in the first period (in current month) 
currency | String | false | The currency used for payment. Default is JPY  
description | String | false | Description of the transaction 
customer_id | String | false | The customer id on merchant system 
user_id | String | false | SWAPay user id (if the user_id is submitted, the customer_id is not needed) 
customer_order_id | String | false | The order id on merchant systems 
date_payment | DateTime | false | 
date_start | DateTime | false | 
success_url | String | false | Redirect to `success_url` after successful payment 
callback_url | String | false | JSON-formatted `POST` notification message will be sent to `callback_url` when order status is changed. If the callback is empty, we can send information to merchant's email. 
cancel_url | String | false | Redirect to `cancel_url` when buyer cancels the order	