# Store information
```shell
curl --location --request GET '{{server}}/api/v1/store/detail' \
--header 'Authorization: eyJhbGciOiJIUzI1NiJ9.eyJpYXQiOjE3NjA1ODk5MTJ9.oDn9osvEp9jPoz05cQbXoTWV5HsnixLUTlDmk37dkew'
The above command returns JSON structured like this:
{
    "id": "d228a8e2-b6eb-4c1c-8fa7-ea2e53cf2655",
    "store_name": "storeC",
    "office_name": null,
    "representative": null,
    "postal_code": null,
    "province": null,
    "address": null,
    "address2": null,
    "phone": null,
    "token_store": "eyJhbGciOiJIUzI1NiJ9.eyJpYXQiOjE3NTUwODAwODl9.N15bEeIu4uU-QmrIgIWYY7MTrO-1WoeKjyEpcehiAWQ",
    "logos": null,
    "status": "active",
    "create_date": "2025-08-13T10:14:49.090+00:00",
    "update_date": "2025-10-20T03:02:46.796+00:00",
    "merchant": null,
    "operation_agency": null,
    "owner": {
        "id": "3e7a4538-8a84-4963-9586-6b0b8dd6262b",
        "first_name": null,
        "last_name": null,
        "email": "agency@nft-swapay.com",
        "phone": null,
        "avatar": null,
        "confirmed": null,
        "role": "OPERATION_AGENCY",
        "status": "ACTIVE",
        "affiliate_code": null,
        "parent_id": null,
        "display_name": "agency@nft-swapay.com",
        "display_gateway": "GMO_GATEWAY",
        "address": null,
        "invoice_business_registration_number": null,
        "company_name": null,
        "representative_name": null,
        "account_number": null,
        "user_id": null 
        },
    "contract": {
        "id": "00ac55ca-748c-46e8-bf6c-ac825d7b682f",
        "status": "ACTIVE",
        "corporate_number": "1",
        "company_name": "1",
        "company_name_phonetic": "1",
        "post_code": "1",
        "registered_address": "1",
        "phone_number": "1",
        "fax": "1",
        "representative_name": "1",
        "name_of_representative_furigana": "1",
        "date_of_birth_of_representative": "Fri Dec 22 2023 00:00:00 GMT+0700 (Indochina Time)",
        "representative_address_postal_code": "1",
        "representative_address": "1",
        "online_shop_name": "1",
        "online_shop_url": "1",
        "product_service_details": "1",
        "average_spend_per_customer": "1",
        "handling_product_minimum_unit_price": "1",
        "products_handled_maximum_unit_price": "1"
        },
    "api_key": null,
    "publishable_key": null,
    "alpha_id": null,
    "alpha_pass": null,
    "amount": 0.0,
    "flag_amount": false,
    "trading_type": "REGULAR_PAYMENT",
    "payment_methods": [
        "CREDIT_CARD"
    ],
    "credit_card_types": [
        "VISA_CARD",
        "MASTER_CARD",
        "JCB_CARD",
        "AMEX_CARD",
        "DINERS_CARD"
    ],
    "site_id": null,
    "site_pass": null,
    "shop_id": null,
    "shop_pass": null,
    "public_key": null,
    "public_key_hash": null,
    "gateway_type": "FIN_CODE_GATEWAY",
    "merchant_ccid": null,
    "merchant_secret_key": null,
    "token_api_key": null,
    "td_flag": null,
    "tenant": null,
    "min_amount": 1.0,
    "max_amount": 9999999.0,
    "limit_amount": false,
    "shop_name": null,
    "shop_name_kana": null,
    "parent_shop_id": null,
    "parent_shop_name": null,
    "shop_type": null,
    "back_account_list": null,
    "transfer_destination": "DIRECT_MERCHANT",
    "methods": [
        "ONE_TIME"
    ],
    "receipt_enabled": true,
    "send_payment_success_email": true,
    "keywords": null,
    "pre_authentication": true
}
Abnormal

{
  "code": "E0401",
  "message": "Invalid authorization code",
  "errors": null
}

```

The API returns the current store’s configuration and profile (e.g., name, status, payment gateway, enabled payment methods, amount limits, etc.).

 HTTP Request

`GET /v1/store/detail`

Production environment
`https://api.swa-pay.com/api/v1/store/detail`

Staging environment
`https://staging-api.swa-pay.com/api/v1/store/detail`

Store Response Fields

| Field                      | Type            | Description                         |
| -------------------------- | --------------- | ------------------------------------|
| id                         | `UUID`          | Store ID on SWAPay                  |
| store_name                 | `String`        | Store name                          |
| token_store                | `String`        | Store-scoped token (sensitive)      |
| status                     | `String`        | Store status (`request_active`,`active`, `request_delete`, `deleted`)|
| create_date                | `DateTime`      | Store creation time                 |
| update_date                | `DateTime`      | Last updated time                   |
| owner                      | `Object`        | Owner info (see **Owner Fields**)   |
| contract                   | `Object`        | Store’s signed contract info (see **Contract Fields**) |
| amount                     | `Number`        | Verification amount threshold (if used)   |
| flag_amount                | `Boolean`       | Whether `amount` rule is enabled   |
| trading_type               | `String`        | Operation method (`REGULAR_PAYMENT`, `ESCROW_PAYMENT`, `TEMPORARY_SALES_PAYMENT`)   |
| payment_methods            | `Array<String>` | Enabled payment methods (e.g., `CREDIT_CARD`, `PAYPAY`, `LINEPAY`, `APPLEPAY`, `GOOGLE_PAY`)|
| credit_card_types          | `Array<String>` | Accepted card brands (`VISA_CARD`, `MASTER_CARD`, `JCB_CARD`, `AMEX_CARD`, `DINERS_CARD`)               |
| gateway_type               | `String`        | Configured gateway (e.g., `FIN_CODE_GATEWAY`, `ALPHA_NOTE_GATEWAY`, `GMO_GATEWAY`) |
| min_amount                 | `Number`        | Minimum allowed payment amount       |
| max_amount                 | `Number`        | Maximum allowed payment amount       |
| limit_amount               | `Boolean`       | Whether min/max amount limits are enforced       |
| transfer_destination       | `String`        | Settlement destination policy (e.g., `DIRECT_MERCHANT`)      |
| methods                    | `Array<String>` | Allowed billing types (`ONE_TIME`, `INSTALLMENT`, `REVOLVING`, `SUBSCRIPTION`)              |
| receipt_enabled            | `Boolean`       | Whether receipt issuance is enabled   |
| send_payment_success_email | `Boolean`       | Whether to send payment-success emails |
| pre_authentication         | `Boolean`       | Require **3DS2 pre-authentication** at **card registration** (¥10 test charge → auto-refund on success) |


Owner Fields

| Field                 | Type     | Description                                     |
| --------------------- | -------- | ----------------------------------------------- |
| id                    | `UUID`   | Owner user ID                                   |
| email                 | `String` | Owner email                                     |
| role                  | `String` | Owner role (e.g., `OPERATION_AGENCY`, `MERCHANT`)           |
| status                | `String` | Owner account status (e.g., `ACTIVE`)           |
| display_name          | `String` | Owner display name                              |
| display_gateway       | `String` | Preferred display gateway (e.g., `GMO_GATEWAY`) |

Contract Fields

| Field                               | Type     | Description                        |
| ----------------------------------- | -------- | ---------------------------------- |
| id                                  | `UUID`   | Contract ID                        |
| status                              | `String` | Contract status (e.g., `ACTIVE`)   |
| corporate_number                    | `String` | Corporate number                   |
| company_name                        | `String` | Company name                       |
| company_name_phonetic               | `String` | Company name (phonetic)            |
| post_code                           | `String` | Company postal code                |
| registered_address                  | `String` | Registered corporate address       |
| phone_number                        | `String` | Company phone number               |
| fax                                 | `String` | Company fax                        |
| representative_name                 | `String` | Legal representative name          |
| name_of_representative_furigana     | `String` | Representative name (furigana)     |
| date_of_birth_of_representative     | `String` | Representative’s DOB (as provided) |
| representative_address_postal_code  | `String` | Representative postal code         |
| representative_address              | `String` | Representative address             |
| online_shop_name                    | `String` | Online shop name                   |
| online_shop_url                     | `String` | Online shop URL                    |
| product_service_details             | `String` | Description of products/services   |
| average_spend_per_customer          | `String` | Average spend per customer         |
| handling_product_minimum_unit_price | `String` | Minimum unit price handled         |
| products_handled_maximum_unit_price | `String` | Maximum unit price handled         |
