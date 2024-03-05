# Cloud Wallets

Secure programmatic wallets for the Nano blockchain.

Build demanding Nano applications with ease.

> Nano.to [API KEY](https://rpc.nano.to) required.

## Get Started

```bash
curl -d '{
  "action": "cloud_wallet",
  "vanity": "1temp",
  "refund_address": "YOUR_ADDRESS",
  "expire": "5 minutes",
  "key": "WALLET-API-KEY",
}' \
-H "Content-Type: application/json" \
"https://rpc.nano.to"
```

**Response:**

```json
{
  "balance": 0,
  "address": "nano_1temp9dzx8kmkbcpedwi...4bzoh3pafk9grxndk88inkbe",
  "refund_address": "YOUR_ADDRESS",
  "expiration": "in 10 minutes",
  "expiration_unix": 1710873173
}
```

> Provided ```api_key``` is used to authenticate future API calls. Optionally, you can use ```seed``` to return the privateKey. Or use ```public``` when client-side to omit ```api_key``` from response.

## All Options

- **```balance```:** (*string or bool*) get account balance and pending. 
- **```receive```:** (*string or bool*) receive *all* pending blocks. 
- **```send```:** (string, *@username or address*) Send funds. 
- **```delete```:** (*string or bool*) Manually expire address. 
- **```vanity```:** (*string or bool*) Generate custom address. Up to 5 characters.
- **```seed```:** (*string or bool*) Return *privateKey* with first response. Provided only once.
- **```refund_address```** (*array or string*) account(s) that receive funds on expiration. 
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
  "account": "nano_1temp9dzx8kmkbcpedwi...4bzoh3pafk9grxndk88inkbe",
  "key": "WALLET-API-KEY",
}' \
-H "Content-Type: application/json" \
"https://rpc.nano.to"
```

**Response:**

```json
[
  {
    "hash": "533A1D3F0DD7B4138493...7085DDE0DE175ACCCA6412",
    "amount": "1000000000000000000000000000000",
    "amount_nano": "1",
    "source": "nano_1bank1q3q7x8ri....8kggtfaosg8kyr51qsdkm8g45",
    "username": "@bank"
  }
]
```

## Balance

```bash
curl -d '{
  "action": "cloud_wallet",
  "balance": "true",
  "account": "nano_1temp9dzx8kmkbcpedwi...4bzoh3pafk9grxndk88inkbe",
  "key": "WALLET-API-KEY",
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
  "account": "nano_1temp9dzx8kmkbcpedwi...4bzoh3pafk9grxndk88inkbe",
  "key": "WALLET-API-KEY",
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
  "account": "nano_1temp9dzx8kmkbcpedwi...4bzoh3pafk9grxndk88inkbe",
  "key": "WALLET-API-KEY",
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

## Profit Sharing API

Refund_address accepts an array. When address expires, funds are sent equally between configured accounts. 

```bash
curl -d '{
  "action": "cloud_wallet",
  "refund_address": ["@faucet", "@bank"],
  "expire": "5 minutes",
  "key": "WALLET-API-KEY",
}' \
-H "Content-Type: application/json" \
"https://rpc.nano.to"
```

> Support for split percentages coming soon.

## Dedicated Support

- Email: support@nano.to
- Discord: [Nano.to Discord](https://discord.gg/DG7UEyp4gX)
- Twitter: [twitter.com/@nano2dev](https://twitter.com/nano2dev)
- Mastodon: [xno.social/@nano2dev](https://xno.social/nano2dev)
