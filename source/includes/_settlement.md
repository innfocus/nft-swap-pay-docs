# Settlement

Make a payment by communicating with the card company.

## When making a payment using a token

## When paying with a member ID

## When making a payment using a card number

```shell
curl --location --request POST 'https://nft-swap-test.azurewebsites.net/api/v1/payment' \
--header 'Authorization: meowmeowmeow.' \
--header 'Content-Type: application/json' \
--data-raw '{
    "id": "8405b5f8-0244-4bd5-97cb-748ddeac6b13",
    "card_no": "4100000000000100",
    "expire": "2512",
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