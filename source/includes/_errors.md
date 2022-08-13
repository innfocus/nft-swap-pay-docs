# Errors

> The error response:

```json
{
    "code": "101",
    "message": "Missing amount",
    "errors": null
}
```

### HTTP Status codes:

Status Code | Meaning
---------- | -------
400 | Bad Request -- Your request is invalid.
401 | Unauthorized -- Your API key is wrong.
403 | Forbidden -- The api requested is hidden for special roles.
404 | Not Found -- The endpoint could not be found.
500 | Internal Server Error -- We had a problem with our server. Try again later.
503 | Service Unavailable -- We're temporarily offline for maintenance. Please try again later.

### The SWAPAY API Error code list

Error Code | Meaning
---------- | -------
101 | Missing amount
303 | The status of the order does not allow payment
304 | The payment request ID is invalid
401 | Incorrect password or email
403 | Invalid authorization code
500 | Internal error server
E0001 | Passwords do not match 
E0002 | Change passwords do not succeeded  
E0003 | Password and New Password is same  
E0004 | Password not correct  
E0005 | Date format not correct  
E0006 | User does not have permission to access 
E0007 | Merchant does not exists 
E0008 | Password confirmation cannot be empty  
E0009 | Passwords do not match  
E0010 | Email is already used  
E0011 | User register not success
E0012 | User does not active  
E0013 | User does not exists  
E0014 | Email or password not correct  
E0015 | Email is required 
E0016 | Username is required 
E0017 | Merchant contract is existed 
E0018 | An error occurred, register merchant contract is not success 
E0019 | Customer ID is already used  
E0020 | Delete merchant contract failed  
E0021 | Merchant Contract does not exist 
E0022 | Merchant isn't activated 
E0013 | Merchants don't own store 
E0100 | Regenerate token store do not succeeded 
E0101 | The store is not found 
E0102 | Update store is failed 
E0103 | Store has deleted, can not update. 
E0104 | Delete store is failed 
E0105 | Active store is failed  
E0106 | Store isn't activated  
E0107 | Store id required  
E0108 | Store is active, merchant is not permission not update  
E0200 | Update status order is not success  
E0201 | Order status not change  
E0202 | Missing pay times  
E0203 | Missing amount   
E0204 | Missing user ID  
E0205 | Invalid user ID  
E0206 | Transaction is not continuous payment  
E0207 | Create order is failed
  
### Credit card payment error code 

You can check at [GMO Mulpay Docs](https://gmopg_docs:PF%cwa$GmCC@docs.mul-pay.jp/payment/credit/errorcode).