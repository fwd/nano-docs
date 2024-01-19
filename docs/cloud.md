# Cloud Wallets

Secure programmatic wallets for the Nano blockchain. 

***Wallets have limited lifespan. After expiration, all funds are sent to refund_address.*** 

This API is free, no fees are added to your transactions. **Rate limited to 30 requests per minute.** 

A commercial-grade, high-throughput version of this API is in development.

## Get Started

```bash
curl -d '{
  "action": "cloud_wallet",
  "vanity": "1temp",
  "refund_address": "YOUR_ADDRESS",
  "expire": "10 minutes"
}' \
-H "Content-Type: application/json" \
"https://rpc.nano.to"
```

**Response:**

```json
{
  "balance": 0,
  "address": "nano_1temp9dzx8kmkbcpedwi...4bzoh3pafk9grxndk88inkbe",
  "api_key": "NANO-WALLET-API-KEY-67353C9E78A34474A977....591AAD07D37FB94F84C",
  "refund_address": "YOUR_ADDRESS",
  "expiration": "in 10 minutes",
  "expiration_unix": 1710873173
}
```

## Available Params

- **```balance```:** (*string or bool*) get account balance and pending. Requires ```api_key```. Returns object. 
- **```receive```:** (*string or bool*) receive *all* pending blocks. Requires ```api_key```. Returns array of hashes.
- **```send```:** (string, *@username or address*) Send funds. Requires ```api_key```. Returns object with hash.
- **```refund_address```** (*array or string*) account(s) that receive funds on expiration. 
    - If array, funds are split evenly between accounts. 
- **```approved```** (*array or string*) Limit accounts which can be sent to. 
- **```public```** (*string or bool*) Hide ```api_key``` from initial response. Ideal for client-side use.
- **```seed```:** (*string or bool*) Return ```privateKey``` in initial response. Only provided once.
- **```vanity```:** (*string or bool*) Generate custom address. Up to 5 characters. Requires ```api_key```. 
- **```delete```:** (*string or bool*) Manually expire address. Requires ```api_key```.
- **```expire```** (*number or string*) Control when the address expires. Min 5 minutes. Max 90 days.
    - 5 minutes
    - 1 hour
    - 1 day
    - 3 months

---

## Receive

```bash
curl -d '{
  "action": "cloud_wallet",
  "receive": "all",
  "key": "NANO-WALLET-API-KEY-67353C9E78A34474A977....591AAD07D37FB94F84C"
}' \
-H "Content-Type: application/json" \
"https://rpc.nano.to"
```

**Response:**

```json
[
  {
    "hash": "533A1D3F0DD7B4138493...7085DDE0DE175ACCCA6412",
    "amount": "100000000000000000000000000",
    "source": "nano_1bank1q3q7x8ri....8kggtfaosg8kyr51qsdkm8g45"
  }
]
```

## Balance

```bash
curl -d '{
  "action": "cloud_wallet",
  "balance": "true",
  "key": "NANO-WALLET-API-KEY-67353C9E78A34474A977....591AAD07D37FB94F84C"
}' \
-H "Content-Type: application/json" \
"https://rpc.nano.to"
```

**Response:**

```json
{
  "balance": "90000000000000000000000000",
  "pending": "0",
  "receivable": "0",
  "balance_nano": "0.00009",
  "pending_nano": "0",
  "receivable_nano": "0",
  "address": "nano_1cxmn9dzx8kmkbcpedwi...4bzoh3pafk9grxndk88inkbe",
  "expiration": "in 3 months",
  "expiration_unix": 1710873173,
  "nanolooker": "https://nanolooker.com/account/nano_1cxmn9dzx8kmkbcpedwi...4bzoh3pafk9grxndk88inkbe"
}
```

## Send

```bash
curl -d '{
  "action": "cloud_wallet",
  "send": "@bank",
  "amount": "0.00001",
  "key": "NANO-WALLET-API-KEY-67353C9E78A34474A977....591AAD07D37FB94F84C"
}' \
-H "Content-Type: application/json" \
"https://rpc.nano.to"
```

**Response:**

```json
{ 
  "hash": "652B9EFBE95C8E5495E1604E5...ECEE337CE27514B2226"
}
```

## Delete

Manually trigger expiration.

```bash
curl -d '{
  "action": "cloud_wallet",
  "delete": "true",
  "key": "NANO-WALLET-API-KEY-67353C9E78A34474A977....591AAD07D37FB94F84C"
}' \
-H "Content-Type: application/json" \
"https://rpc.nano.to"
```

**Response:**

```json
{ 
  "deleted": true
}
```

## Public

**For use client-side. No secret API key is returned.**

```bash
curl -d '{
  "action": "cloud_wallet",
  "public": "true",
  "refund_address": ["@faucet", "@bank"],
  "expire": "5 minutes"
}' \
-H "Content-Type: application/json" \
"https://rpc.nano.to"
```

**Response:**

```json
{
  "balance": 0,
  "address": "nano_1cxmn9dzx8kmkbcpedwi...4bzoh3pafk9grxndk88inkbe",
  "refund_address": ["nano_1faucet7b6xjy...ska8kwopzf1ecbfmn35d1zey3ys", "nano_1bank7b6xjy...ska8kwopzf1ecbfmn35d1zey3ys"],
  "expiration": "in 5 minutes",
  "expiration_unix": 1710873173
}
```

## Dedicated Support

- Email: support@nano.to
- Discord: [Nano.to Discord](https://discord.gg/DG7UEyp4gX)
- Twitter: [twitter.com/@nano2dev](https://twitter.com/nano2dev)
- Mastodon: [xno.social/@nano2dev](https://xno.social/nano2dev)
