# Membership card

## Card registration


```shell
curl --location --request POST 'https://staging-api.swa-pay.com/api/v1/cards' \
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

`POST /v1/cards`

Production environment
`https://api.swa-pay.com/api/v1/cards`

Staging environment
`https://staging-api.swa-pay.com/api/v1/cards`

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

## Response Fields

Field | Type | Description
----- | ---- | -------
id | UUID |  Card ID on SWAPay System
card_seq | String | Card registration serial number 
expire | String | Card expiration date (format MM/YY)
status | String | card status
holder_name | String | card holder
short_card_no | String | the masked value card number
card_type | String | card type 

