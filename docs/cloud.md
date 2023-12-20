# Nano Cloud Wallets

**Custodial, Ephemeral (*temporary*) Nano Cloud Wallets.** 

The goal of this API is to expedite Nano Development & Prototyping.

Examples below are in cURL, but you can use any HTTP library that supports POST. 

**After 90 days, wallets expire and all funds are sent to  ```refund_address```.**

## Get Started

**Create Wallet:**

```bash
curl -d '{
  "action": "cloud_wallet",
  "refund_address": "@faucet"
}' \
-H "Content-Type: application/json" \
"https://rpc.nano.to"
```

**Response:**

```json
{
  "balance": 0,
  "address": "nano_1cxmn9dzx8kmkbcpedwi...4bzoh3pafk9grxndk88inkbe",
  "api_key": "NANO-WALLET-API-KEY-67353C9E78A34474A977....591AAD07D37FB94F84C",
  "refund_address": "nano_1faucet7b6xjy...ska8kwopzf1ecbfmn35d1zey3ys",
  "expiration": "in 3 months",
  "expiration_unix": 1710873173
}
```

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

## Security

- Seed is *only* provided during creation, if ```seed``` field is present.
- Provide ```approved``` (array or string) to limits accounts which can be sent to. 
- Provide ```expiration``` (number or string) field to reduce expiration time. In days. Max 90.

```bash
curl -d '{
  "action": "cloud_wallet",
  "refund_address": "@faucet", 
  "seed": "true",
  "approved": [ "@bank", "@faucet", "nano_1c3fdz..." ],
  "expiration": 30
}' \
-H "Content-Type: application/json" \
"https://rpc.nano.to"
```

## Nano.to Support

- Email: support@nano.to
- Discord: [Nano.to Discord](https://discord.gg/DG7UEyp4gX)
- Twitter: [twitter.com/@nano2dev](https://twitter.com/nano2dev)
- Mastodon: [xno.social/@nano2dev](https://xno.social/nano2dev)