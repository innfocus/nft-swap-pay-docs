# Errors

> The error response:

```json
{
    "code": "101",
    "message": "Missing amount",
    "errors": null
}
```

HTTP Status codes:

Status Code | Meaning
---------- | -------
400 | Bad Request -- Your request is invalid.
401 | Unauthorized -- Your API key is wrong.
403 | Forbidden -- The api requested is hidden for special roles.
404 | Not Found -- The endpoint could not be found.
500 | Internal Server Error -- We had a problem with our server. Try again later.
503 | Service Unavailable -- We're temporarily offline for maintenance. Please try again later.

The SWAPAY API Error code list

Error Code | Meaning
---------- | -------
101 | Missing amount
303 | The status of the order does not allow payment
304 | The payment request ID is invalid
401 | Incorrect password or email
403 | Invalid authorization code
500 | Internal error server

Credit card payment error code can be found at [GMO Mulpay Docs](https://gmopg_docs:PF%cwa$GmCC@docs.mul-pay.jp/payment/credit/errorcode).