---
title: SWAPAY API

language_tabs: # must be one of https://github.com/rouge-ruby/rouge/wiki/List-of-supported-languages-and-lexers
  - shell

toc_footers:
  - <a href='https://staging-console.swa-pay.com/' target="_blank">Start here</a>

includes:
  - orders
  - settlement
  - members
  - user_cards
  - recurring_billing
  - errors

search: true

code_clipboard: true

meta:
  - name: description
    content: Documentation for SWAPAY API
---

# Introduction

Welcome to the SWAPAY API!

The Sandbox SWAPAY API endpoint is [https://staging-api.swa-pay.com](https://staging-api.swa-pay.com).  
The Production SWAPAY API endpoint is [https://api.swa-pay.com](https://api.swa-pay.com). 


# Authentication

> To authorize, use this code:


```shell
# With shell, you can just pass the correct header with each request
curl "https://staging-api.swa-pay.com" \
  -H "Authorization: meowmeowmeow"
```

> Make sure to replace `meowmeowmeow` with your API key.

SWAPAY uses API keys to allow access to the API. You can register a new SWAPAY API key at our [merchant console](https://staging-merchant.nft-swapay.com/).

SWAPAY expects for the API key to be included in all API requests to the server in a header that looks like the following:

`Authorization: meowmeowmeow`

<aside class="notice">
You must replace <code>meowmeowmeow</code> with your personal API key.
</aside>

