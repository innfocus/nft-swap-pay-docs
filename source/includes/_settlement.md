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
    "id": "764acfd2-18dc-45ca-9596-fcd5ec4ddcc6",
    "cardNo": "4111111111111111",
    "expire": "2512",
    "securityCode": "123",
    "holderName": "LYBIA SOFT"
}'
```

> The above command returns JSON structured like this:

```json
{
    "tranID": "2207051607111111111111810098",
    "acs": "0",
    "method": "",
    "orderID": "1657005480384",
    "payTimes": "",
    "forward": "2a99662",
    "approve": "0000000",
    "clientField3": "",
    "checkString": "1087da9fb0ac329dbda9e1db81d3c7a4",
    "tranDate": "20220705161802",
    "clientField1": "",
    "clientField2": ""
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
This endpoint will help you register a member on SWAPAY system.

### HTTP Request

`POST https://nft-swap-test.azurewebsites.net/api/v1/payment/member`

### JSON Object Payload Parameters

Parameter | Required | Description
--------- | -------- | -----------
customer_id | true | The customer id on merchant system 
name | false | The member's name 
email | false | The member's email 
phone | false | The member's phone 
address | false | The member's address 
