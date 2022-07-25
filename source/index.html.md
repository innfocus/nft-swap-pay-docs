---
title: SWAPAY API

language_tabs: # must be one of https://git.io/vQNgJ
  - shell

toc_footers:
  - <a href='https://staging-console.nft-swapay.com/' target="_blank">Start here</a>

includes:
  - orders
  - settlement
  # - members
  - errors

search: true

code_clipboard: true

meta:
  - name: description
    content: Documentation for SWAPAY API
---

# Introduction

Welcome to the SWAPAY API!

The SWAPAY API endpoint is [https://nft-swap-test.azurewebsites.net](https://nft-swap-test.azurewebsites.net).


# Authentication

> To authorize, use this code:


```shell
# With shell, you can just pass the correct header with each request
curl "https://nft-swap-test.azurewebsites.net" \
  -H "Authorization: meowmeowmeow"
```

> Make sure to replace `meowmeowmeow` with your API key.

SWAPAY uses API keys to allow access to the API. You can register a new SWAPAY API key at our [merchant console](https://staging-merchant.nft-swapay.com/).

SWAPAY expects for the API key to be included in all API requests to the server in a header that looks like the following:

`Authorization: meowmeowmeow`

<aside class="notice">
You must replace <code>meowmeowmeow</code> with your personal API key.
</aside>

