# Membership card

## Card registration

```shell
curl --location --request POST 'https://staging-api.swa-pay.com/api/v1/cards' \
--header 'Authorization: eyJhbGciOiJIUzI1NiJ9.eyJpYXQiOjE3MzY5MDk3MzF9.Tb4wsSMTITRLvV4PaHhgu_8QTPhGXuDktPIhd2pvmJM' \
--header 'Content-Type: application/json' \
--data-raw {
    "card_no": "5100 0000 0000 0115",
    "expire": "1231",
    "security_code": "123",
    "holder_name": "ta pham kim hieu",
    "user_id": "08f504d9-3cfc-4b78-bf61-8faddf42df15",
    "success_url": "https://swapay.co.jp/",
    "callback_url": "https://2446-115-78-15-4.ap.ngrok.io/gateway/receiving",
    "cancel_url": "https://swapay.co.jp/"
}
```

> The above command returns JSON structured like this:

```json
{
    "id": "ca0123b5-b402-47fb-bc04-2bf6fa71f1b3",
    "short_card_no": "*************115",
    "card_name": null,
    "expire": "12/31",
    "holder_name": "ta pham kim hieu",
    "card_type": "MASTER",
    "status": "ACTIVE",
    "security_code": null,
    "user_create": "08f504d9-3cfc-4b78-bf61-8faddf42df15",
    "create_date": "2025-10-22T04:44:38.231+00:00",
    "user_update": "08f504d9-3cfc-4b78-bf61-8faddf42df15",
    "update_date": "2025-10-22T04:44:38.231+00:00",
    "user": {
        "id": "08f504d9-3cfc-4b78-bf61-8faddf42df15",
        "first_name": null,
        "last_name": null,
        "email": null,
        "phone": null,
        "avatar": null,
        "confirmed": null,
        "role": "USER",
        "status": "NOT_YET",
        "affiliate_code": null,
        "parent_id": null,
        "display_name": null,
        "display_gateway": "GMO_GATEWAY",
        "address": null,
        "invoice_business_registration_number": null,
        "company_name": null,
        "representative_name": null,
        "account_number": null,
        "user_id": null
    },
    "selected": false,
    "store": null,
    "gateway": null,
    "card_gateway_id": null,
    "pre_authorization": false,
    "transaction": {
        "id": "f7106ca2-e635-471e-9944-3071dfe56008",
        "pay_amount": 10.0,
        "currency": "JPY",
        "customer_id": null,
        "customer_order_id": null,
        "status": "AUTHENTICATING_3DS",
        "update_date": "2025-10-22T04:44:40.985+00:00",
        "create_date": "2025-10-22T04:44:40.985+00:00",
        "pay_method": "0",
        "pay_times": null,
        "order_id_csv": null,
        "actual_payment_date": null,
        "confirmed_at": null,
        "acs": "2",
        "acs_url": "https://simulator.test.fincode.jp/payment/Tds2StubCallback.idPass?transId=77974614-110b-4fb0-b314-9c117e3726bd&t=a_cXKnXjgqT4ukDBY_fgVE4Q",
        "redirect_url": "https://staging-api.swa-pay.com/api/v1/fincode/secure/authentication/f7106ca2-e635-471e-9944-3071dfe56008",
        "user_payment": {
            "id": "08f504d9-3cfc-4b78-bf61-8faddf42df15",
            "first_name": null,
            "last_name": null,
            "email": null,
            "phone": null,
            "affiliate_code": null,
            "display_name": null,
            "address": null
        },
        "state": null
    },
    "error": null
}
```

This endpoint will help you register the card information with the specified member.

### HTTP Request

`POST /v1/cards`

Production environment
`https://api.swa-pay.com/api/v1/cards`

Staging environment
`https://staging-api.swa-pay.com/api/v1/cards`

### JSON Object Payload Parameters

|Parameter          | Required   | Description                               |
| ----------------- | ---------- |------------------------------------------|
| user_id           | true       | The SWAPay user id                       | 
| card_no           | true       | Credit card number                       |
| expire            | true       | Credit card expiration date - MMYY format |
| security_code     | true       | Security code - The 3- or 4-digit number printed on the card |
| holder_name       | true       | Credit card name                          |
| success_url       | false      | Redirect to `success_url` after successful payment |  
| cancel_url        | false      | Redirect to `cancel_url` when buyer cancels the order |
| callback_url      | false      | JSON-formatted `POST` notification message will be sent to `callback_url` when order status is changed. If the callback is empty, we can send information to merchant's email.  |


### Card Response Fields
| Field             | Type       | Description                              |
| ----------------- | ---------- |------------------------------------------|
| id                | `UUID`     | Card ID on SWAPay                        |
| short_card_no     | `String`   | Masked card number (last digits only).   |
| card_name         | `String`   | Custom card label set by user (nullable) |
| expire            | `String`   | Expiry in `MM/YY` format                 |
| holder_name       | `String`   | Cardholder name (as registered)                                                                    |
| card_type         | `String`   | Card brand (`VISA`, `MASTER`, `JCB`, `AMEX`, `DINERS`, …)|
| status            | `String`   | Card status (`ACTIVE`, `DELETED`)        |
| user_create       | `UUID`     | Creator user ID                          |
| create_date       | `DateTime` | Created time                             |
| user_update       | `UUID`     | Last updater user ID                     |
| update_date       | `DateTime` | Last updated time                        |
| user              | `Object`   | Owner user info                          |
| selected          | `Boolean`  | `true` if this is the consumer’s default/selected card  |
| store             | `Object`   | Store info *(nullable)                   |
| gateway           | `Object`   | Gateway info *(nullable)*                |
| card_gateway_id   | `String`   | Gateway-side card identifier *(nullable)*|
| pre_authorization | `Boolean`  | `true` if this card was **successfully 3DS2 pre-authenticated** at registration; `false` otherwise |
|transaction        |`Object`    | Present only when Pre-Authentication is enabled. Contains the 3DS2 authentication transaction to complete card registration (e.g., id, status, pay_amount = 10, acs, acs_url, redirect_url, timestamps, user_payment). Use redirect_url (recommended) or acs_url to complete the 3DS2 challenge. (nullable) |
|error.             |`Object`    | Additional error payload when registration encounters an issue. Follows the standard error format { code, message, errors }. null on success. If not null, handle this instead of proceeding with transaction. (nullable)


Transaction Field

| Field               | Type       | Description      |
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

Notes
Raw PAN/CVV are not stored and are never returned by the API.
If Pre-Authentication is enabled, the system will create a temporary order for ¥10, attempt a 3DS2 authentication + payment, and auto-refund that order on success.
Cards that passed the initial 3DS2 pre-auth can later be used with either 3DS2 or No-3DS, depending on risk/routing settings.


### Client flow (high level)

1. **Register card** via `POST /v1/cards`.
2. If the store has **Pre-Authentication** enabled, the API returns an **`AUTHENTICATING_3DS`** payload.
3. **Redirect** the user to **`redirect_url`** *(recommended)*, or directly to **`acs_url`**, to complete the **3DS2 challenge**.
4. On success, the temporary order (**¥10**) is **paid** and then **auto-refunded**.
5. The card appears in `GET /v1/store/consumers/{consumer_id}/cards` with `pre_authorization = true`.
### Tips
* Use **`success_url`** / **`cancel_url`** to return the browser to your site after 3DS2.
* Use **`callback_url`** for **server-to-server** confirmation if you want to finalize the UI without relying on browser redirects.


## Card Remove

```shell
curl --location --request DELETE 'https://staging-api.swa-pay.com/api/v1/cards/{id}' \
--header 'Authorization: {store_token}' \
--header 'Content-Type: application/json' \
--data-raw '{
    "id": "06d43140-51d8-40a7-b457-221f46d74c23"
}'
```

> The above command returns JSON structured like this:

```json
{
    "id": "06d43140-51d8-40a7-b457-221f46d74c23",
    "short_card_no": "*************100",
    "card_name": null,
    "expire": "12/25",
    "holder_name": "LYBIA SOFT",
    "card_type": "VISA",
    "status": "DELETE",
    "security_code": null,
    "create_date": "2024-05-23T04:29:47.751+00:00",
    "update_date": "2024-05-27T05:50:38.670+00:00",
}
```

Remove card by card_id

### HTTP Request

`DELETE /v1/cards/{id}`

Production environment
`https://api.swa-pay.com/api/v1/cards/{id}`

Staging environment
`https://staging-api.swa-pay.com/api/v1/cards/{id}`

### JSON Object Payload Parameters

Parameter | Required | Description
--------- | -------- | -----------
id | true | The SWAPay card id (UUID)

### Response Fields

Field | Type | Description
----- | ---- | -------
id | UUID |  Card ID on SWAPay System
card_seq | String | Card registration serial number 
expire | String | Card expiration date (format MM/YY)
status | String | card status
holder_name | String | card holder
short_card_no | String | the masked value card number
card_type | String | card type 


## Get a list of cards

```shell
curl --location --request GET '{{server}}/api/v1/store/consumers/{consumer_id}/cards' \
--header 'Authorization: eyJhbGciOiJIUzI1NiJ9.eyJpYXQiOjE3MDUzMTU5NDV9.xT3EFN3SC51hORCMEaSDeoA1KEGwGm7cAXdIFQtxr28'

> The above command returns JSON structured like this:
[
  {
    "id": "4cdfaa39-61e3-4cc4-8f68-a0d02bc91319",
    "short_card_no": "****************007",
    "card_name": null,
    "expire": "12/31",
    "holder_name": "ta pham kim hieu",
    "card_type": "MASTER",
    "status": "ACTIVE",
    "security_code": null,
    "user_create": "02eecc89-5ac8-4969-9e8f-d183fc8c84a4",
    "create_date": "2025-10-19T06:10:15.774+00:00",
    "user_update": "02eecc89-5ac8-4969-9e8f-d183fc8c84a4",
    "update_date": "2025-10-19T06:10:15.774+00:00",
    "user": {
      "id": "02eecc89-5ac8-4969-9e8f-d183fc8c84a4",
      "first_name": "hieu",
      "last_name": "taphamkim",
      "email": "hieutaphamkim89+1750@gmail.com",
      "phone": null,
      "avatar": null,
      "confirmed": null,
      "role": "USER",
      "status": "ACTIVE",
      "affiliate_code": null,
      "parent_id": null,
      "display_name": "taphamkim hieu",
      "display_gateway": "GMO_GATEWAY",
      "address": null,
      "invoice_business_registration_number": null,
      "company_name": null,
      "representative_name": null,
      "account_number": null,
      "user_id": null
    },
    "selected": true,
    "store": null,
    "gateway": null,
    "card_gateway_id": null,
    "pre_authorization": true
  },
  {
    "id": "9cd378b2-7086-4d69-b245-95b97f84f0da",
    "short_card_no": "****************000",
    "card_name": null,
    "expire": "12/31",
    "holder_name": "ta pham kim hieu",
    "card_type": "VISA",
    "status": "ACTIVE",
    "security_code": null,
    "user_create": "02eecc89-5ac8-4969-9e8f-d183fc8c84a4",
    "create_date": "2025-10-19T06:10:48.553+00:00",
    "user_update": "02eecc89-5ac8-4969-9e8f-d183fc8c84a4",
    "update_date": "2025-10-19T06:10:48.553+00:00",
    "user": {
      "id": "02eecc89-5ac8-4969-9e8f-d183fc8c84a4",
      "first_name": "hieu",
      "last_name": "taphamkim",
      "email": "hieutaphamkim89+1750@gmail.com",
      "phone": null,
      "avatar": null,
      "confirmed": null,
      "role": "USER",
      "status": "ACTIVE",
      "affiliate_code": null,
      "parent_id": null,
      "display_name": "taphamkim hieu",
      "display_gateway": "GMO_GATEWAY",
      "address": null,
      "invoice_business_registration_number": null,
      "company_name": null,
      "representative_name": null,
      "account_number": null,
      "user_id": null
    },
    "selected": false,
    "store": null,
    "gateway": null,
    "card_gateway_id": null,
    "pre_authorization": true
  }
]
> Abnormal
{
    "code": "E0208",
    "message": "User not found",
    "errors": null
}
```
This endpoint returns all saved cards of a given consumer within the current store context.


### HTTP Request
`GET /v1/store/consumers/{consumer_id}/cards`

Production environment
`https://api.swa-pay.com/api/v1/store/consumers/{consumer_id}/cards`

Staging environment
`https://staging-api.swa-pay.com/api/v1/store/consumers/{consumer_id}/cards`

URL Parameters

| Parameter   | Description            |
| ----------- | ---------------------- |
| consumer_id | The ID of the consumer |

Error code list

| Error Code | Meaning                                          |
| ---------- | ------------------------------------------------ |
| E0401      | Unauthorized (missing/invalid token)             |
| E0403      | Forbidden (no permission to this store/consumer) |
| E0208      | User not found (invalid `consumer_id`)           |

### Card Response Fields
| Field             | Type       | Description                              |
| ----------------- | ---------- |------------------------------------------|
| id                | `UUID`     | Card ID on SWAPay                        |
| short_card_no     | `String`   | Masked card number (last digits only).   |
| card_name         | `String`   | Custom card label set by user (nullable) |
| expire            | `String`   | Expiry in `MM/YY` format                 |
| holder_name       | `String`   | Cardholder name (as registered)                                                                    |
| card_type         | `String`   | Card brand (`VISA`, `MASTER`, `JCB`, `AMEX`, `DINERS`, …)|
| status            | `String`   | Card status (`ACTIVE`, `DELETED`)        |
| user_create       | `UUID`     | Creator user ID                          |
| create_date       | `DateTime` | Created time                             |
| user_update       | `UUID`     | Last updater user ID                     |
| update_date       | `DateTime` | Last updated time                        |
| user              | `Object`   | Owner user info                          |
| selected          | `Boolean`  | `true` if this is the consumer’s default/selected card  |
| store             | `Object`   | Store info *(nullable)                   |
| gateway           | `Object`   | Gateway info *(nullable)*                |
| card_gateway_id   | `String`   | Gateway-side card identifier *(nullable)*|
| pre_authorization | `Boolean`  | `true` if this card was **successfully 3DS2 pre-authenticated** at registration; `false` otherwise |

