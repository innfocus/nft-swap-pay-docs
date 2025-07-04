# Recurring billing

## Create a new Recurring billing


```shell
curl --location --request POST 'https://staging-api.swa-pay.com/api/v1/store/recurring_billing' \
--header 'Authorization: meowmeowmeow' \
--header 'Content-Type: application/json' \
--data-raw '{
    "pay_amount":5500,"pay_amount_in_month":1320,"currency":"JPY","subscribe_order_name":null,"user_id":"cbd1474e-a41c-4a1d-a6ce-b910157e95e2","date_start":"2024-09-25","date_end":"2024-12-18",
"first_payment_deadline": "2024-08-20",
"productions":
    [{"service_name":"service_test",
      "unit_price":100,
      "quantity":10,
      "tax_rate":"option_10",
      "sub_total":1100
      },
      {"service_name":"service_test_2",
       "unit_price":200,
        "quantity":20,
         "sub_total":4400,
         "tax_rate":"option_10"
       }
    ],
"initial":[{"service_name":"test_initial","unit_price":100,"quantity":12,"tax_rate":"option_10","sub_total":1320}],
"store_id":"955b8cc3-02dd-434e-927b-f718638536c1","invoice_number":"test","order_name":"test","monthly_payment_day":"12","description":"Description","date_payment":"2024-08-12","service_name_monthly":"service_test","service_name_initial":"test_initial"
}'

```

> The above command returns JSON structured like this:

```json
{
     "id": "8c646ba4-c7c5-4883-8d92-305ac9ca1da8",
    "pay_amount": 1320.0,
    "pay_next_month": null,
    "currency": "JPY",
    "customer_id": null,
    "customer_order_id": null,
    "description": "Description",
    "consumer_id": "cbd1474e-a41c-4a1d-a6ce-b910157e95e2",
    "store": {
        "id": "955b8cc3-02dd-434e-927b-f718638536c1",
        "store_name": "store fincode n3 ",
        "office_name": "1",
        "gateway": "FIN_CODE_GATEWAY",
        "address": "1",
        "address2": "1Registered address",
        "postal_code": "1",
        "merchant": {
            "id": "95969926-0272-4021-82a9-2c58db5daadb",
            "first_name": null,
            "last_name": null,
            "email": "admin@nft-swapay.com",
            "phone": null,
            "avatar": null,
            "confirmed": null,
            "role": "ADMIN",
            "status": "ACTIVE",
            "affiliate_code": null,
            "parent_id": null,
            "display_name": "admin@nft-swapay.com",
            "display_gateway": "GMO_GATEWAY",
            "address": "HCM city",
            "invoice_business_registration_number": "s2201",
            "company_name": null,
            "representative_name": null,
            "account_number": null
        },
        "waiting_complete": false
    },
    "merchant": {
        "id": "95969926-0272-4021-82a9-2c58db5daadb",
        "first_name": null,
        "last_name": null,
        "email": "admin@nft-swapay.com",
        "phone": null,
        "avatar": null,
        "confirmed": null,
        "role": "ADMIN",
        "status": "ACTIVE",
        "affiliate_code": null,
        "parent_id": null,
        "display_name": "admin@nft-swapay.com",
        "display_gateway": "GMO_GATEWAY",
        "address": "HCM city",
        "invoice_business_registration_number": "s2201",
        "company_name": null,
        "representative_name": null,
        "account_number": null
    },
    "agency": null,
    "subscribe": {
        "id": "7f4f941f-769b-43b3-8c06-721631e4986b",
        "subscribe_order_name": "test",
        "service_name_monthly": "service_test",
        "pay_amount": 5500.0,
        "service_name_initial": "test_initial",
        "initial_cost_amount": 1320.0,
        "date_start": "2024-09-25T00:00:00.000+00:00",
        "date_end": "2024-12-18T00:00:00.000+00:00",
        "pay_times": null,
        "monthly_payment_day": 12,
        "status": "TEMPORARY_SAVE",
        "consumer_name": "Hieu ta pham kim",
        "consumer_email": "hieutaphamkim89@gmail.com",
        "first_payment_deadline": "2024-08-20T00:00:00.000+00:00",
        "consumer_phone": "0964-47-7058"
    },
    "success_url": null,
    "cancel_url": null,
    "callback_url": null,
    "status": "WAITING_FOR_PAYMENT",
    "user_create": null,
    "create_date": "2024-09-25T08:10:12.180+00:00",
    "monthly_payment_date": "2024-08-20T00:00:00.000+00:00",
    "user_update": null,
    "update_date": "2024-09-25T08:10:12.180+00:00",
    "payment_url": "https://staging-user.swa-pay.com/payment/invoice?order=8c646ba4-c7c5-4883-8d92-305ac9ca1da8",
    "pay_method": null,
    "pay_times": null,
    "consumer_email": "hieutaphamkim89@gmail.com",
    "consumer_phone": null,
    "user_payment": null,
    "card_seq": null,
    "actual_payment_date": null,
    "confirmed_at": null,
    "pay_amount_fees": null,
    "actual_pay_amount": null,
    "card_type": null,
    "refunded_date": null,
    "fee_detail": null,
    "gmo_order_id": null,
    "error": null,
    "transaction_histories": null,
    "system_logs": null,
    "nft_evidence": null,
    "productions": [
        {
            "id": "a0ec2f11-2d22-43e7-84a3-aaa6664aa885",
            "order_id": "8c646ba4-c7c5-4883-8d92-305ac9ca1da8",
            "subscribe_order_id": "7f4f941f-769b-43b3-8c06-721631e4986b",
            "service_name": "test_initial",
            "unit_price": 100.0,
            "quantity": 12,
            "sub_total": 1320.0,
            "tax_rate": "option_10",
            "tax_value": "10",
            "sub_amount_untaxed": 1200.0,
            "flag_init": false
        }
    ],
    "tax_invoice": null,
    "order_name": "test",
    "expired_date": null,
    "consumer_name": null,
    "title": "test",
    "gateway": "FIN_CODE_GATEWAY",
    "authenticating_date": null,
    "status_request": null,
    "reason_request": null,
    "merchant_response": null,
    "date_request": null,
    "user_request": null,
    "date_response": null,
    "user_response": null,
    "store_qrhistory": null,
    "short_card_no": null,
    "nft": null,
    "issued_date": "2024-09-25T08:10:12.180+00:00",
    "invoice_number": null,
    "honorific_title": null,
    "amount_untaxed": null,
    "amount_taxed": null,
    "payment_app_url": "https://staging-api.swa-pay.com/gateway/payment/8c646ba4-c7c5-4883-8d92-305ac9ca1da8",
    "create_role": null,
    "payment_fees": null,
    "fee_tax": null,
    "tax_rate": null,
    "transaction_fee": null,
    "sales_processing_fee": null,
    "selected_payment_type": "SUBSCRIPTION",
    "selected_installment_term": null
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
first_payment_deadline| DateTime | false | processing date first payment

### Order Response Fields

Field | Type | Description
----- | ---- | -------
id | UUID |  Payment request ID on NFT SWAP System
pay_amount | Double | Total amount to be paid
currency | String | The currency used for payment. Default is JPY  
customer_id | String | The customer id on merchant system
user_id | String | false | SWAPay user id (if the user_id is submitted, the customer_id is not needed)  
customer_order_id | String | The order id on merchant systems
description | String | Description of the transaction 
store | Object Store|  
merchant | Object Merchant |  
success_url | String | Redirect to `success_url` after successful payment   
cancel_url | String | Redirect to `cancel_url` when buyer cancels the order 
callback_url | String | JSON-formatted `POST` notification message will be sent to `callback_url` when order status is changed. If the callback is empty, we can send information to merchant's email.  
status | String | Status of Payment request    
pay_method | String |  
payment_url | String | The customer will process the payment at this site.
pay_times | Number |    
update_date | DateTime |   
create_date  | DateTime | 
selected_payment_type | String | Enum: "SUBSCRIPTION"
selected_installment_term | String or null 

## Update a Recurring billing


```shell
curl --location --request PUT 'https://staging-api.swa-pay.com/api/v1/store/recurring_billing/b87395d6-e334-43be-bd72-800053c53283' \
--header 'Authorization: meowmeowmeow' \
--header 'Content-Type: application/json' \
--data-raw '{
    "monthly_payment_day": "6",
    "date_start": "2025-07-08",
    "date_end": "2027-07-03",
     "description": "Change payment day from 5 to 6 "
}'

```

> The above command returns JSON structured like this:

```json
{
    "id": "4a03c284-e139-4f62-94a6-6e04f5208c85",
    "subscribe_order_name": null,
    "service_name_monthly": null,
    "pay_amount": 8000.0,
    "service_name_initial": null,
    "initial_cost_amount": null,
    "first_payment_deadline": null,
    "date_start": "2025-07-04T10:00:00.000+00:00",
    "date_end": "2027-07-03T00:00:00.000+00:00",
    "pay_times": null,
    "monthly_payment_day": 6,
    "status": "WAITING_FOR_PAYMENT",
    "consumer_name": null,
    "consumer_email": null,
    "consumer_phone": null,
    "store": {
        "id": "955b8cc3-02dd-434e-927b-f718638536c1",
        "store_name": "store fincode n3",
        "office_name": "1",
        "gateway": "FIN_CODE_GATEWAY",
        "address": "1",
        "address2": "1Registered address",
        "postal_code": "1",
        "merchant": {
            "id": "95969926-0272-4021-82a9-2c58db5daadb",
            "first_name": "Admin",
            "last_name": "",
            "email": "admin@nft-swapay.com",
            "phone": null,
            "avatar": null,
            "confirmed": null,
            "role": "ADMIN",
            "status": "ACTIVE",
            "affiliate_code": "Abcd1234",
            "parent_id": null,
            "display_name": "Admin",
            "display_gateway": "GMO_GATEWAY",
            "address": "HCM city",
            "invoice_business_registration_number": "s2203",
            "company_name": null,
            "representative_name": null,
            "account_number": null
        },
        "trading_type": "REGULAR_PAYMENT",
        "receipt_enabled": true,
        "send_payment_success_email": true
    },
    "user": {
        "id": "4f301013-4e7f-4d5c-8254-f1dc8200bd77",
        "first_name": "Hieu",
        "last_name": "ta pham kim",
        "email": "hieutaphamkim89@gmail.com",
        "phone": "0964477058",
        "avatar": null,
        "confirmed": null,
        "role": "USER",
        "status": "ACTIVE",
        "affiliate_code": null,
        "parent_id": null,
        "display_name": "ta pham kim Hieu",
        "display_gateway": "GMO_GATEWAY",
        "address": "Ho Chi Minh",
        "invoice_business_registration_number": null,
        "company_name": null,
        "representative_name": null,
        "account_number": null
    },
    "merchant": {
        "id": "95969926-0272-4021-82a9-2c58db5daadb",
        "first_name": "Admin",
        "last_name": "",
        "email": "admin@nft-swapay.com",
        "phone": null,
        "avatar": null,
        "confirmed": null,
        "role": "ADMIN",
        "status": "ACTIVE",
        "affiliate_code": "Abcd1234",
        "parent_id": null,
        "display_name": "Admin",
        "display_gateway": "GMO_GATEWAY",
        "address": "HCM city",
        "invoice_business_registration_number": "s2203",
        "company_name": null,
        "representative_name": null,
        "account_number": null
    },
    "currency": "JPY",
    "create_date": "2025-07-02T12:19:51.454+00:00",
    "description": "Change payment day from 5 to 6 ",
    "productions": null,
    "initial": null,
    "tax_invoice": null,
    "amount_untaxed": null,
    "amount_taxed": null,
    "tax_invoice_initial": null,
    "amount_untaxed_initial": null,
    "amount_taxed_initial": null,
    "date_cancel": null
}
```

This endpoint will help you to change the payment details of transactions.

### HTTP Request

`PUT /v1/store/recurring_billing/{id}`

Production environment
`https://api.swa-pay.com/api/v1/store/recurring_billing/{id}`

Staging environment
`https://staging-api.swa-pay.com/api/v1/store/recurring_billing/{id}`


### JSON Object Payload Parameters

Parameter | Type  | Required | Description
--------- | ----- | -------- | -----------
date_start | DateTime | false | Start date of the recurring payment period.
date_end | DateTime | false | End date of the recurring payment period.
monthly_payment_day| Number | false | Day of the month when payment is charged.
description | String | false | Optional description of the recurring plan.

### Order Response Fields
Field | Type | Description
----- | ---- | -------
id | UUID | ID of the subscription order.
subscribe_order_name | String | Name of the subscription order.
service_name_monthly | String | Name of the monthly service.
pay_amount | Double | Amount to be paid monthly.
service_name_initial | String | Name of the initial service or setup.
initial_cost_amount | Double | 	Initial setup cost or one-time fee.
first_payment_deadline | DateTime | Deadline for the first payment.
date_start | DateTime | Start date of the recurring payment period.
date_start | DateTime | End date of the recurring payment period.
currency | String | The currency used for payment. Default is JPY  
user | Object User Paymment | false | Payment user information. (Optional)
description | String | Description of the transaction (e.g. purpose or subscription details).
store | Object Store| Store information.
merchant | Object Merchant | Merchant information.
monthly_payment_day | Number | Day of the month when the payment is charged.
status | String | Status of the subscription order.
consumer_name | String | Name of the consumer.
consumer_email | String | Email address of the consumer.
consumer_phone | String | Phone number of the consumer.   
update_date | DateTime | Date when the record was last updated.
create_date  | DateTime | Date when the record was created.
productions | Object productions | Information about the subscribed products or services.
tax_invoice | Double | Tax amount (monthly).
amount_untaxed | Double | Monthly payment amount before tax.
amount_taxed | Double | Monthly payment amount including tax.
tax_invoice_initial | Double | Tax amount of the initial cost.
amount_untaxed_initial | Double | Initial cost before tax.
amount_taxed_initial | Double | Initial cost including tax.
date_cancel | DateTime | Date when the subscription was canceled.

## Subscription order Status

Status Code | Meaning
---------- | -------
TEMPORARY_SAVE| The subscription order has been temporarily saved but not yet submitted for payment.
WAITING_FOR_PAYMENT | The initial payment was completed, and the subscription is active. The system is now waiting for the upcoming recurring payments (e.g., monthly billing).
COMPLETE | The recurring billing cycle has finished. All scheduled payments have been completed, and the subscription is now closed. 
CANCEL | The subscription order was canceled by the user or merchant before payment was completed (i.e., while in TEMPORARY_SAVE or WAITING_FOR_PAYMENT status).
ERROR | A failure occurred during the payment process, and the transaction could not be completed.

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

### JSON Object Payload Parameters (Payment with new card)

Parameter | Required | Description
--------- | -------- | -----------
id | true | ID of the transaction
card_no | true | credit card number 
expire | true | Credit card expiration date - MMYY format
security_code | true | security code - The 3- or 4-digit number printed on the card
holder_name | true | Credit card name 
user_id | true | The ID of the customer who will be the purchaser. 


### JSON Object Payload Parameters (Payment with member)

Parameter | Required | Description
--------- | -------- | -----------
id | true | ID of the transaction
card_id | true | The ID of the card used for this payment.
user_id | true | The ID of the customer who will be the purchaser.

##  Termination of subscription
> Discontinue the subscription specified by ID and stop billing.

```shell
curl --location --request DELETE 'https://staging-api.swa-pay.com/api/v1/store/recurring_billing/9346119c-2a27-4697-ada9-bab6873c3d69' \
--header 'Authorization: meowmeowmeow' \
--header 'Content-Type: application/json'

```

> The above command returns JSON structured like this:

```json
{
    "id": "9346119c-2a27-4697-ada9-bab6873c3d69",
    "subscribe_order_name": "test",
    "service_name_monthly": "test",
    "pay_amount": 1100.0,
    "service_name_initial": "test init",
    "initial_cost_amount": 5500.0,
    "first_payment_deadline": "2024-10-19T17:00:00.000+00:00",
    "date_start": "2024-11-24T00:00:00.000+00:00",
    "date_end": null,
    "pay_times": null,
    "monthly_payment_day": 24,
    "status": "CANCEL",
    "consumer_name": "ta pham kim Hieu",
    "consumer_email": "hieutaphamkim89@gmail.com",
    "consumer_phone": "0964-47-7058",
    "store": {
        "id": "955b8cc3-02dd-434e-927b-f718638536c1",
        "store_name": "store fincode n3",
        "office_name": "1",
        "gateway": "FIN_CODE_GATEWAY",
        "address": "1",
        "address2": "1Registered address",
        "postal_code": "1",
        "merchant": {
            "id": "95969926-0272-4021-82a9-2c58db5daadb",
            "first_name": null,
            "last_name": null,
            "email": "admin@nft-swapay.com",
            "phone": null,
            "avatar": null,
            "confirmed": null,
            "role": "ADMIN",
            "status": "ACTIVE",
            "affiliate_code": null,
            "parent_id": null,
            "display_name": "admin@nft-swapay.com",
            "display_gateway": "GMO_GATEWAY",
            "address": "HCM city",
            "invoice_business_registration_number": "s2201",
            "company_name": null,
            "representative_name": null,
            "account_number": null
        },
        "trading_type": "TEMPORARY_SALES_PAYMENT"
    },
    "user": {
        "id": "4f301013-4e7f-4d5c-8254-f1dc8200bd77",
        "first_name": "Hieu",
        "last_name": "ta pham kim",
        "email": "hieutaphamkim89@gmail.com",
        "phone": "0964-47-7058",
        "avatar": null,
        "confirmed": null,
        "role": "USER",
        "status": "ACTIVE",
        "affiliate_code": null,
        "parent_id": null,
        "display_name": "ta pham kim Hieu",
        "display_gateway": "GMO_GATEWAY",
        "address": "Ho Chi Minh",
        "invoice_business_registration_number": null,
        "company_name": null,
        "representative_name": null,
        "account_number": null
    },
    "merchant": {
        "id": "95969926-0272-4021-82a9-2c58db5daadb",
        "first_name": null,
        "last_name": null,
        "email": "admin@nft-swapay.com",
        "phone": null,
        "avatar": null,
        "confirmed": null,
        "role": "ADMIN",
        "status": "ACTIVE",
        "affiliate_code": null,
        "parent_id": null,
        "display_name": "admin@nft-swapay.com",
        "display_gateway": "GMO_GATEWAY",
        "address": "HCM city",
        "invoice_business_registration_number": "s2201",
        "company_name": null,
        "representative_name": null,
        "account_number": null
    },
    "currency": "JPY",
    "create_date": "2024-10-24T15:00:58.483+00:00",
    "description": "test",
    "productions": null,
    "initial": null,
    "tax_invoice": null,
    "amount_untaxed": null,
    "amount_taxed": null,
    "tax_invoice_initial": null,
    "amount_untaxed_initial": null,
    "amount_taxed_initial": null
}
```

This endpoint will help you to change the payment details of transactions.

### HTTP Request

`DELETE /v1/store/recurring_billing/{id}`

Production environment
`https://api.swa-pay.com/api/v1/store/recurring_billing/{id}`

Staging environment
`https://staging-api.swa-pay.com/api/v1/store/recurring_billing/{id}`

### JSON Object Payload Parameters

Parameter | Type  | Required | Description
--------- | ----- | -------- | -----------
id | UUID | true | ID of the transaction

