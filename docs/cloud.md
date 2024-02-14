# Cloud Wallets (Beta)

Secure programmatic wallets for the Nano blockchain. 

## Usage Pricing

<table>
    <thead>
        <tr>
            <th>Monthly API Calls</th>
            <th>Cost Per Send</th>
        </tr>
    </thead>
    <tbody>
        <tr> <td> 0 - 1K </td> <td> FREE </td> </tr>
        <tr> <td> 1K - 10K </td> <td> 0.0001 NANO </td> </tr>
        <tr> <td> 10K - 100K </td> <td> 0.0005 NANO </td> </tr>
        <tr> <td> 100K - 1M </td> <td> 0.001 NANO </td> </tr>
    </tbody>
</table>

> A commercial-grade, high-capacity version (>1M) of this API is in development, expected Q2 2025.

## Get Started

```bash
curl -d '{
  "action": "cloud_wallet",
  "vanity": "1temp",
  "refund_address": "YOUR_ADDRESS",
  "expire": "5 minutes"
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
  "expiration_unix": 1710873173,
  "encryption": "AES-256"
}
```

## All Options

- **```balance```:** (*string or bool*) get account balance and pending. Requires *api_key*. Returns object. 
- **```receive```:** (*string or bool*) receive *all* pending blocks. Requires *api_key*. Returns array of blocks.
- **```send```:** (string, *@username or address*) Send funds. Requires *api_key*. Returns object with hash.
- **```public```** (*string or bool*) Hide *api_key* from response. For use with [NanoPay.js](https://blog.nano.to/NanoPay).
- **```seed```:** (*string or bool*) Return *privateKey* with first response. Provided only once.
- **```vanity```:** (*string or bool*) Generate custom address. Up to 5 characters.
- **```delete```:** (*string or bool*) Manually expire address. Requires *api_key*.
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
  "key": "NANO-WALLET-API-KEY-67353C9E78A34474A977....591AAD07D37FB94F84C",
  "password": "my-secret-passphrase"
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
  "key": "NANO-WALLET-API-KEY-67353C9E78A34474A977....591AAD07D37FB94F84C",
  "password": "my-secret-passphrase"
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
  "key": "NANO-WALLET-API-KEY-67353C9E78A34474A977....591AAD07D37FB94F84C",
  "password": "my-secret-passphrase"
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
  "key": "NANO-WALLET-API-KEY-67353C9E78A34474A977....591AAD07D37FB94F84C",
  "password": "my-secret-passphrase"
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
