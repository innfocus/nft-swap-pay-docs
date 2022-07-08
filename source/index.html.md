---
title: API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - shell

toc_footers:
  - <a href='https://staging-console.nft-swapay.com/' target="_blank">Start here</a>

includes:
  - errors

search: true

code_clipboard: true

meta:
  - name: description
    content: Documentation for the Kittn API
---

# Introduction

Welcome to the SWAPAY API!

The SWAPAY API endpoint is [https://nft-swap-test.azurewebsites.net](https://nft-swap-test.azurewebsites.net).


# Authentication

> To authorize, use this code:


```shell
# With shell, you can just pass the correct header with each request
curl "https://nft-swap-test.azurewebsites.net" \
  -H "Authorization: meowmeowmeow"
```

> Make sure to replace `meowmeowmeow` with your API key.

SWAPAY uses API keys to allow access to the API. You can register a new SWAPAY API key at our [merchant console](https://staging-merchant.nft-swapay.com/).

SWAPAY expects for the API key to be included in all API requests to the server in a header that looks like the following:

`Authorization: meowmeowmeow`

<aside class="notice">
You must replace <code>meowmeowmeow</code> with your personal API key.
</aside>

# Orders

## Get All Orders

```shell
curl --location --request GET 'https://nft-swap-test.azurewebsites.net/api/v1/store/orders' \
--header 'Authorization: meowmeowmeow'
```

> The above command returns JSON structured like this:

```json
[
    {
        "id": "893f3980-06d0-4abc-a3f8-0ed97f5ce6f8",
        "pay_amount": 1000.0,
        "currency": "USD",
        "customer_id": "1000",
        "customer_order_id": "1001",
        "description": "NFT",
        "consumer_id": null,
        "success_url": null,
        "cancel_url": null,
        "callback_url": null,
        "status": "WAITING_FOR_PAYMENT",
        "user_create": "af40eee0-81ad-4e29-a8ea-87603b3f8282",
        "create_date": "2022-07-07T13:56:17.696+00:00",
        "user_update": "af40eee0-81ad-4e29-a8ea-87603b3f8282",
        "update_date": "2022-07-07T13:56:17.696+00:00",
        "payment_url": "/gateway/payment/893f3980-06d0-4abc-a3f8-0ed97f5ce6f8"
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


## Create a new Order


```shell
curl --location --request POST 'https://nft-swap-test.azurewebsites.net/api/v1/order' \
--header 'Authorization: meowmeowmeow' \
--header 'Content-Type: application/json' \
--data-raw '{
    "pay_amount": 1000.0,
    "description": "Sample order"
}'
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

This endpoint will help you to start a transaction

### HTTP Request

`POST https://nft-swap-test.azurewebsites.net/api/v1/order`

### Body Request Parameters

Parameter | Required | Description
--------- | -------- | -----------
pay_amount | true | Amount of the transaction 
description | false | Description of the transaction 
customer_id | false | The customer id on merchant system 
customer_order_id | false | The order id on merchant systems 

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

