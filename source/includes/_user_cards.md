# Membership card

## Card registration


```shell
curl --location --request POST 'https://nft-swap-test.azurewebsites.net/api/v1/cards' \
--header 'Authorization: meowmeowmeow' \
--header 'Content-Type: application/json' \
--data-raw '{
    "user_id": "9af4f665-9869-4c95-99ca-51d14a32d50f",
    "card_no": "4100000000000100",
    "expire": "1225",
    "security_code": "123",
    "holder_name": "LYBIA SOFT"
}'
```

> The above command returns JSON structured like this:

```json
{
    "id": "35f7282f-c5c5-4d24-9c56-e5495f07cab4",
    "card_seq": "3",
    "short_card_no": "*************100",
    "card_name": null,
    "expire": null,
    "holder_name": null,
    "forward": "2a99662"
}
```

This endpoint will help you register the card information with the specified member.

### HTTP Request

`POST https://nft-swap-test.azurewebsites.net/api/v1/cards`

### JSON Object Payload Parameters

Parameter | Required | Description
--------- | -------- | -----------
user_id | false | The SWAPay user id 
card_no | true | credit card number 
expire | true | Credit card expiration date - MMYY format
security_code | true | security code - The 3- or 4-digit number printed on the card
holder_name | true | Credit card name

## Response Fields

Field | Type | Description
----- | ---- | -------
id | UUID |  Card ID on SWAPay System
card_seq | String | Card registration serial number 
forward | String | Destination code 
short_card_no | String | the masked value card number  

