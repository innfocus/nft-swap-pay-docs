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
    "tran_date": "20220726124728",
    "client_field1": "",
    "method": "",
    "client_field3": "",
    "user_update": "af40eee0-81ad-4e29-a8ea-87603b3f8282",
    "client_field2": "",
    "forward": "2a99662",
    "check_string": "5b793c76fcc516a15c559959b67c0408",
    "tran_id": "2207261207111111111111815975",
    "pay_times": "",
    "user_create": "af40eee0-81ad-4e29-a8ea-87603b3f8282",
    "update_date": 1658807248809,
    "acs": "0",
    "acsurl": null,
    "pa_req": null,
    "approve": "       ",
    "md": null,
    "id": "34c09841-28df-4842-ae65-013a7fb22417",
    "create_date": 1658807248809,
    "order_id": "20220726104722-132"
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