# Orders

## Create a new Order


```shell
curl --location --request POST 'https://nft-swap-test.azurewebsites.net/api/v1/order' \
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
    "cancel_url": "https://swapay.co.jp/"
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
    "payment_url": "https://nft-swap-test.azurewebsites.net/gateway/payment/8405b5f8-0244-4bd5-97cb-748ddeac6b13",
    "pay_method": null,
    "pay_times": null
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

`POST https://nft-swap-test.azurewebsites.net/api/v1/order`

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

## Order Response Fields

Field | Type | Description
----- | ---- | -------
id | UUID |  Payment request ID on NFT SWAP System
pay_amount | Double | Total amount to be paid
currency | String | The currency used for payment. Default is JPY  
customer_id | String | The customer id on merchant system  
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


## Get All Orders

```shell
curl --location --request GET 'https://nft-swap-test.azurewebsites.net/api/v1/store/orders' \
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
        "payment_url": "https://nft-swap-test.azurewebsites.net/gateway/payment/8405b5f8-0244-4bd5-97cb-748ddeac6b13",
        "pay_method": null,
        "pay_times": null
    }
]
```

This endpoint retrieves all Orders.

### HTTP Request

`GET https://nft-swap-test.azurewebsites.net/api/v1/store/orders`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
page | 1 | 
per_page | 30 | 


## Get status a Order

```shell
curl --location --request GET "https://nft-swap-test.azurewebsites.net/api/v1/orders/2" \
--header 'Authorization: meowmeowmeow'
```

> The above command returns JSON structured like this:

```json
{
    "id": "764acfd2-18dc-45ca-9596-fcd5ec4ddcc6",
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

`GET https://nft-swap-test.azurewebsites.net/api/v1/orders/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the order


## Order Status

Status Code | Meaning
---------- | -------
WAITING_FOR_PAYMENT | The Waiting for payment status means that we still are waiting for payment. 
PROCESSING | 
COMPLETE | Transaction was successfully. 
REFUNDED | 
ON_HOLD | 
REJECTED | The payment has been declined either by your payment operator or due to security reasons by our system.  


## Callback Response Message

> Each JSON-formatted `POST` notification message like this:

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

We'll let you know when a transaction changes status via `callback_url`.

### Callback Response Fields

Field | Type | Description
----- | ---- | -------
id | |  
pay_amount |  | 
currency | |   
customer_id | |  
customer_order_id |  | 
status | |    
pay_method |  |   
pay_times | |    
update_date | |  
create_date  | | 

