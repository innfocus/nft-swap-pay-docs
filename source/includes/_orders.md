# Orders

## Create a new Order


```shell
curl --location --request POST 'https://staging-api.swa-pay.com/api/v1/order' \
--header 'Authorization: meowmeowmeow' \
--header 'Content-Type: application/json' \
--data-raw '{
    "pay_amount": 1000.0,
    "currency": "JPY",
    "customer_id": "1000",
    "customer_order_id": "1001",
    "description": "NFT",
    "success_url": "https://swapay.co.jp/",
    "callback_url": "https://swapay.co.jp/",
    "cancel_url": "https://swapay.co.jp/",
    "selected_payment_type": "INSTALLMENT",
    "selected_installment_term": 6
}'
```

> The above command returns JSON structured like this:

```json
{
    "id": "8405b5f8-0244-4bd5-97cb-748ddeac6b13",
    "pay_amount": 1000.0,
    "currency": "JPY",
    "customer_id": "1000",
    "customer_order_id": "1001",
    "description": null,
    "consumer_id": null,
    "store": {
        "id": "0d630192-d7f3-4c05-8540-19d91f2aaa4b",
        "store_name": "NFT SWAP STORE 3",
        "office_name": "NFT SWAP STORE"
    },
    "merchant": {
        "id": "af40eee0-81ad-4e29-a8ea-87603b3f8282",
        "display_name": "Kenji Umemura"
    },
    "success_url": "https://swapay.co.jp/",
    "cancel_url": "https://swapay.co.jp/",
    "callback_url": "https://swapay.co.jp/",
    "status": "WAITING_FOR_PAYMENT",
    "user_create": null,
    "create_date": "2022-07-25T05:34:31.631+00:00",
    "user_update": null,
    "update_date": null,
    "payment_url": "https://staging-api.swa-pay.com/gateway/payment/8405b5f8-0244-4bd5-97cb-748ddeac6b13",
    "pay_method": null,
    "pay_times": null,
    "selected_payment_type": "INSTALLMENT",
    "selected_installment_term": 6
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

This endpoint will help you to start a transaction

### HTTP Request

`POST /v1/order`

Production environment
`https://api.swa-pay.com/api/v1/order`

Staging environment
`https://staging-api.swa-pay.com/api/v1/order`

### JSON Object Payload Parameters

Parameter | Type  | Required | Description
--------- | ----- | -------- | -----------
pay_amount | Double | true | Amount of the transaction 
currency | String | false | The currency used for payment. Default is JPY  
description | String | false | Description of the transaction 
customer_id | String | false | The customer id on merchant system 
customer_order_id | String | false | The order id on merchant systems 
success_url | String | false | Redirect to `success_url` after successful payment 
callback_url | String | false | JSON-formatted `POST` notification message will be sent to `callback_url` when order status is changed. If the callback is empty, we can send information to merchant's email. 
cancel_url | String | false | Redirect to `cancel_url` when buyer cancels the order	
user_id | String | false | The customer ID on SWAPay system (Returned in the user registration api)
consumer_email | String | false | Email of customer	
consumer_phone | String | false | Phone of consumer
selected_payment_type | String or null | false | Enum: "ONE_TIME" "INSTALLMENT" "REVOLVING" ONE_TIME: One-time payment (default), INSTALLMENT: Installment payment, REVOLVING: Revolving payment
selected_installment_term | String or null | false | Enum: "3" "5" "6" "10" "12" "15" "18" "20" "24" (For installments) Number of payments

System will send confirmation message after payment with contact information registered with `user_id`.  
If there is no `user_id`, you can send `consumer_email` or `consumer_phone`. So that the system can send a confirmation message after payment

## Order Response Fields

Field | Type | Description
----- | ---- | -------
id | UUID |  Payment request ID on NFT SWAP System
pay_amount | Double | Total amount to be paid
currency | String | The currency used for payment. Default is JPY  
customer_id | String | The customer id on merchant system
user_id | String | false | SWAPay user id (if the user_id is submitted, the customer_id is not needed)  
customer_order_id | String | The order id on merchant systems
description | String | Description of the transaction 
store | |  
merchant | |  
success_url | String | Redirect to `success_url` after successful payment   
cancel_url | String | Redirect to `cancel_url` when buyer cancels the order 
callback_url | String | JSON-formatted `POST` notification message will be sent to `callback_url` when order status is changed. If the callback is empty, we can send information to merchant's email.  
status | String | Status of Payment request    
pay_method | String |  
payment_url | String | The customer will process the payment at this site.
pay_times | Number |    
update_date | DateTime |   
create_date  | DateTime | 
selected_payment_type | String or null | Enum: "ONE_TIME" "INSTALLMENT" "REVOLVING" 
selected_installment_term | String or null | Enum: "3" "5" "6" "10" "12" "15" "18" "20" "24" (For installments) Number of payments

## Update a order

```shell
curl --location --request PUT 'https://staging-api.swa-pay.com/api/v1/store/orders/c2b5512c-7ef2-4590-bfb7-3eb2874b2187' \
--header 'Authorization: meowmeowmeow' \
--header 'Content-Type: application/json' \
--data-raw '{
    "pay_amount": 1000
}'

```

> The above command returns JSON structured like this:

```json
{
    "id": "ed2b2b6c-f88a-468a-a94e-7585925e4e83",
    "pay_amount": 1000.0,
    "pay_next_month": 1000.0,
    "currency": "JPY",
    "customer_id": "1000",
    "customer_order_id": "1001",
    "description": "NFT",
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
    "success_url": "https://swapay.co.jp/",
    "cancel_url": "https://swapay.co.jp/",
    "callback_url": "https://3c80-2405-4802-9119-ab90-e86d-6d5a-d791-666c.ap.ngrok.io/gateway/receiving",
    "status": "WAITING_FOR_PAYMENT",
    "user_create": null,
    "create_date": "2022-08-13T02:14:41.314+00:00",
    "monthly_payment_date": null,
    "user_update": null,
    "update_date": "2022-08-13T02:14:41.314+00:00",
    "payment_url": "https://149c-123-20-166-241.ap.ngrok.io/gateway/payment/ed2b2b6c-f88a-468a-a94e-7585925e4e83",
    "pay_method": null,
    "pay_times": null,
    "consumer_email": null,
    "user_id": null,
    "subscribe": null,
    "selected_payment_type": "ONE_TIME",
    "selected_installment_term": null
}
```

This endpoint will help you to change the payment details of transactions.

### HTTP Request

`PUT /v1/store/orders/{id}`

Production environment
`https://api.swa-pay.com/api/v1/store/orders/{id}`

Staging environment
`https://staging-api.swa-pay.com/api/v1/store/orders/{id}`

### JSON Object Payload Parameters

Parameter | Type  | Required | Description
--------- | ----- | -------- | -----------
pay_amount | Double | false | Recurring payment amount 
description | String | false | Description of the transaction  
date_payment | DateTime | false | 

## Get All Orders

```shell
curl --location --request GET 'https://staging-api.swa-pay.com/api/v1/store/orders' \
--header 'Authorization: meowmeowmeow'
```

> The above command returns JSON structured like this:

```json
[
    {
        "id": "8405b5f8-0244-4bd5-97cb-748ddeac6b13",
        "pay_amount": 1000.0,
        "currency": "JPY",
        "customer_id": "1000",
        "customer_order_id": "1001",
        "description": null,
        "consumer_id": null,
        "store": {
            "id": "0d630192-d7f3-4c05-8540-19d91f2aaa4b",
            "store_name": "NFT SWAP STORE 3",
            "office_name": "NFT SWAP STORE"
        },
        "merchant": {
            "id": "af40eee0-81ad-4e29-a8ea-87603b3f8282",
            "display_name": "Kenji Umemura"
        },
        "success_url": "https://swapay.co.jp/",
        "cancel_url": "https://swapay.co.jp/",
        "callback_url": "https://swapay.co.jp/",
        "status": "WAITING_FOR_PAYMENT",
        "user_create": null,
        "create_date": "2022-07-25T05:34:31.631+00:00",
        "user_update": null,
        "update_date": null,
        "payment_url": "https://staging-api.swa-pay.com/gateway/payment/8405b5f8-0244-4bd5-97cb-748ddeac6b13",
        "pay_method": null,
        "pay_times": null
    }
]
```

This endpoint retrieves all Orders.

### HTTP Request

`GET /v1/store/orders`

Production environment
`https://api.swa-pay.com/api/v1/store/orders`

Staging environment
`https://staging-api.swa-pay.com/api/v1/store/orders`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
page | 1 | 
per_page | 30 | 


## Get status a Order

```shell
curl --location --request GET "https://staging-api.swa-pay.com/api/v1/store/orders/5c73f272-ebc8-4428-8a84-36e3d0230910" \
--header 'Authorization: meowmeowmeow'
```

> The above command returns JSON structured like this:

```json
{
    "id": "5c73f272-ebc8-4428-8a84-36e3d0230910",
    "pay_amount": 1000.0,
    "currency": null,
    "customer_id": null,
    "customer_order_id": null,
    "description": "Sample order",
    "consumer_id": null,
    "success_url": null,
    "cancel_url": null,
    "callback_url": null,
    "status": "WAITING_FOR_PAYMENT",
    "user_create": "af40eee0-81ad-4e29-a8ea-87603b3f8282",
    "create_date": "2022-07-08T07:43:02.612+00:00",
    "user_update": "af40eee0-81ad-4e29-a8ea-87603b3f8282",
    "update_date": "2022-07-08T07:43:02.612+00:00",
    "payment_url": "/gateway/payment/764acfd2-18dc-45ca-9596-fcd5ec4ddcc6"
}
```

This endpoint get a specific order information.

### HTTP Request

`GET /v1/store/orders/{id}`

Production environment
`https://api.swa-pay.com/api/v1/store/orders/{id}`

Staging environment
`https://staging-api.swa-pay.com/api/v1/store/orders/{id}`

### URL Parameters

Parameter | Description
--------- | -----------
id | The ID of the order


## Order Status

Status Code | Meaning
---------- | -------
TEMPORARY_SAVE| The temporary save status of the order.
WAITING_FOR_PAYMENT | The Waiting for payment status means that we still are waiting for payment. 
OTP_CONFIRMING | Waiting for OTP confirming from Email/SMS. 
OTP_TIMEOUT | Cannot confirm OTP after 30 minutes. 
AUTHENTICATING_3DS | Waiting for 3DS Authentication. 
TIMEOUT_3DS | 3DS timeout after 30 minutes. 
PROCESSING | The transaction is paid and waiting to be confirmed.  
COMPLETE | The transaction was successfully. 
REFUNDED | The transaction is refunded.  
CANCEL | This payment has been canceled while the transaction status was "TEMPORARY_SAVE" or "WAITING_FOR_PAYMENT" and was canceled by the user or merchant. 
ERROR |  An error occurred during the payment process.


## Payment Method of order

Name | Value | Meaning
---- | ----- | -------
CREDIT_CARD | 0 | Credit card payment
CASH | 1 | Cash payment
PAYPAY | 2 | Paypay payment
FAMIPAY | 3 | Famipay payment
LINEPAY | 4 | Linepay payment
APPLEPAY | 5 | Applepay payment

## Pay Type Method for payment

Name | Value | Meaning
---- | ----- | -------
ONE_TIME | ONE_TIME | One Time payment
INSTALLMENT | INSTALLMENT | INSTALLMENT type payment
REVOLVING | REVOLVING | REVOLVING type payment

## Callback Response Message

> Each JSON-formatted `POST` notification message like this:

```json
{
  "id": "0125709b-8837-42fa-a11d-d8f57ebc6e0f",
  "pay_amount": 4000,
  "currency": "JPY",
  "customer_id": null,
  "customer_order_id": "20250324_1460",
  "status": "PROCESSING",
  "update_date": 1742803936591,
  "create_date": 1742803923044,
  "pay_method": "0",
  "pay_times": null,
  "actual_payment_date": 1742803936591,
  "confirmed_at": null,
  "authenticating_date": 1742803936591,
  "user_payment": {
    "id": "4f301013-4e7f-4d5c-8254-f1dc8200bd77",
    "first_name": "Hieu",
    "last_name": "ta pham kim",
    "email": "hieutaphamkim89@gmail.com",
    "phone": "0964-11-1111",
    "affiliate_code": null,
    "display_name": "ta pham kim Hieu",
    "address": "Ho Chi Minh"
  }
}
```

We'll let you know when a transaction changes status via `callback_url`.

### Callback Response Fields

Field | Type | Description
----- | ---- | -----------
id | UUID | Unique identifier of the payment request
pay_amount | Double | Payment amount
currency | String | Currency code (e.g., "JPY", "USD")
customer_id | String or null | Customer identifier (nullable)
customer_order_id | String | ID of the order from the customer system
status | String | Status of the payment request (e.g., PROCESSING, COMPLETE)
update_date | Timestamp (epoch millis) | Last updated time of the transaction
create_date | Timestamp (epoch millis) | Created time of the transaction
pay_method | String | Payment method code (e.g., "0")
pay_times | Int or null | Number of payment installments (nullable)
actual_payment_date | Timestamp (epoch millis) | Time the payment was actually made
confirmed_at | Timestamp (epoch millis) or null | Time the transaction was confirmed
authenticating_date | Timestamp (epoch millis) | Authentication time of the transaction
user_payment | Object | Info of the user who made the payment (see below)

#### user_payment object fields

Field | Type | Description
----- | ---- | -----------
id | UUID | User ID
first_name | String | User's first name
last_name | String | User's last name
email | String | User's email
phone | String | User's phone number
affiliate_code | String or null | Affiliate code if any
display_name | String | Display name of the user
address | String | User's address

