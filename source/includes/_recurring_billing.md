# Recurring billing

## Create a new Recurring billing


```shell
curl --location --request POST 'https://staging-api.swa-pay.com/api/v1/store/recurring_billing' \
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
    "payment_url": "https://staging-api.swa-pay.com/gateway/payment/3e8cba26-c349-49ca-b2e7-4416577994f2",
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

`POST /v1/store/recurring_billing`

Production environment
`https://api.swa-pay.com/api/v1/store/recurring_billing`

Staging environment
`https://staging-api.swa-pay.com/api/v1/store/recurring_billing`

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
date_payment | DateTime | false | When to make payment for the first time  
date_start | DateTime | false | Time to start the recurring payment  
date_end | DateTime | false | when you want to stop paying in the future  
success_url | String | false | Redirect to `success_url` after successful payment 
callback_url | String | false | JSON-formatted `POST` notification message will be sent to `callback_url` when order status is changed. If the callback is empty, we can send information to merchant's email. 
cancel_url | String | false | Redirect to `cancel_url` when buyer cancels the order	

## Update a Recurring billing


```shell
curl --location --request PUT 'https://staging-api.swa-pay.com/api/v1/store/recurring_billing/b87395d6-e334-43be-bd72-800053c53283' \
--header 'Authorization: meowmeowmeow' \
--header 'Content-Type: application/json' \
--data-raw '{
    "pay_amount": 1000
}'

```

> The above command returns JSON structured like this:

```json
{
    "id": "b87395d6-e334-43be-bd72-800053c53283",
    "description": "Recurring Billing",
    "pay_amount": 1000.0,
    "pay_amount_in_month": 700.0,
    "currency": "JPY",
    "card_seq": null,
    "short_card_no": null,
    "success_url": "https://swapay.co.jp/",
    "cancel_url": "https://swapay.co.jp/",
    "callback_url": "https://3c80-2405-4802-9119-ab90-e86d-6d5a-d791-666c.ap.ngrok.io/gateway/receiving",
    "customer_id": null,
    "status": "WAITING_FOR_PAYMENT",
    "date_payment": "2022-08-13T02:17:04.635+00:00",
    "date_start": "2022-08-01T10:00:00.000+00:00",
    "date_end": null,
    "date_cancel": null,
    "user_create": null,
    "create_date": "2022-08-13T02:17:04.635+00:00",
    "user_update": null,
    "update_date": "2022-08-13T02:17:04.635+00:00",
    "file_path": null,
    "file_path_history": null
}
```

This endpoint will help you to change the payment details of transactions.

### HTTP Request

`PUT https://staging-api.swa-pay.com/api/v1/store/recurring_billing/{id}`

### JSON Object Payload Parameters

Parameter | Type  | Required | Description
--------- | ----- | -------- | -----------
pay_amount | Double | false | Recurring payment amount 
description | String | false | Description of the transaction  
date_payment | DateTime | false | 

## Making a payment using a card number

```shell
curl --location --request POST 'https://staging-api.swa-pay.com/api/v1/store/recurring_billing/payment' \
--header 'Authorization: meowmeowmeow.' \
--header 'Content-Type: application/json' \
--data-raw '{
    "id": "c2b5512c-7ef2-4590-bfb7-3eb2874b2187",
    "card_no": "4111111111111111",
    "expire": "1225",
    "security_code": "123",
    "holder_name": "LYBIA SOFT",
    "user_id": "af40eee0-81ad-4e29-a8ea-87603b3f8282"
}'
```

> The above command returns JSON structured like this:

```json
{
    "id": "c2b5512c-7ef2-4590-bfb7-3eb2874b2187",
    "pay_amount": 700.0,
    "currency": "JPY",
    "customer_id": null,
    "customer_order_id": null,
    "status": "COMPLETE",
    "update_date": "2022-08-12T14:13:27.735+00:00",
    "create_date": "2022-08-12T14:13:22.283+00:00",
    "pay_method": null,
    "pay_times": null,
    "order_id_csv": "c45f6d4f-9551-43ce-85db-ff9dd839706e"
}
```
> Abnormal

```json
{
    "code": "303",
    "message": "The status of the transaction does not allow this action",
    "errors": null
}
```

This endpoint will help you to payment for a recurring transaction. 

<aside class="notice">
The payment flow same as one time order. 
</aside>


### HTTP Request

`POST /v1/store/recurring_billing/payment`

Production environment
`https://api.swa-pay.com/api/v1/store/recurring_billing/payment`

Staging environment
`https://staging-api.swa-pay.com/api/v1/store/recurring_billing/payment`

### JSON Object Payload Parameters

Parameter | Required | Description
--------- | -------- | -----------
id | true | ID of the transaction 
card_no | true | credit card number 
expire | true | Credit card expiration date - MMYY format
security_code | true | security code - The 3- or 4-digit number printed on the card
holder_name | true | Credit card name 
user_id | true | SWAPAY user ID 

## Export CSV

```shell
curl --location --request POST 'https://staging-api.swa-pay.com/api/v1/store/recurring_billing/export' \
--header 'Authorization: meowmeowmeow' \
--header 'Content-Type: application/json' \
--data-raw '{
    "start_date": "2022-08-01",
    "end_date": "2022-08-12"
}'

```

> The above command returns CSV content file


This endpoint will help you to download list recurring billings

### HTTP Request

`POST /v1/store/recurring_billing/export`

Production environment
`https://api.swa-pay.com/api/v1/store/recurring_billing/export`

Staging environment
`https://staging-api.swa-pay.com/api/v1/store/recurring_billing/export`

### JSON Object Payload Parameters

Parameter | Type  | Required | Description
--------- | ----- | -------- | -----------
start_date | Date | false | Start date filter 
end_date | Date | false | End date filter 

### CSV Format

Parameter | Type | Description
--------- | ---- | -----------
User ID | UUID | SWAPay user ID 
Recurring billing ID | UUID | Recurring billing ID 
Order ID | UUID | SWAPay order ID 
Pay amount | Number | Recurring billing pay amount 
Date Payment | Date | Recurring billing date payment in month 
Card Seq | String | Card registration serial number  
Status | String | Recurring billing status 

## Upload CSV

```shell
curl --location --request POST 'https://staging-api.swa-pay.com/api/v1/store/recurring_billing/export' \
--header 'Authorization: meowmeowmeow' \
--header 'Content-Type: application/json' \
--data-raw '{
    "start_date": "2022-08-01",
    "end_date": "2022-08-12"
}'

```

> The above command returns CSV content file


This endpoint will help you to upload list recurring billings. You can export list CSV, update pay amount or date payment. Then re-upload to the system. This endpoint will help you to update recurring invoices in bulk 

### HTTP Request

`POST /v1/store/recurring_billing/import`

Production environment
`https://api.swa-pay.com/api/v1/store/recurring_billing/import`

Staging environment
`https://staging-api.swa-pay.com/api/v1/store/recurring_billing/import`

### Form data parameters

Parameter | Type  | Required | Description
--------- | ----- | -------- | -----------
file | File | true | CSV file data 

