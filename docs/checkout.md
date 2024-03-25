# Checkout API

Free, non-custodial Checkout API for the Nano blockchain.

Build elaborate business applications with Nano.

## Simple Usage

```html
<script src="https://unpkg.com/axios/dist/axios.min.js"></script>

<script>
axios.post('https://rpc.nano.to', {
  "action": "checkout",
  "address": "@faucet",
  "amount": "0.1330000XXXX"
}).then((res) => {
  console.log(res.data)
})
</script>
```

**Response:**

```json
{
  "id": "CHECKOUT_ID",
  "browser": "https://nano.to/CHECKOUT_ID",
  "json": "https://api.nano.to/checkout/CHECKOUT_ID",
  "check": "https://api.nano.to/confirm/CHECKOUT_ID",
  "address": "YOUR_ADDRESS",
  "amount": "0.13300004758",
  "amount_raw": "133000047580000000000000000000",
  "link": "nano:YOUR_ADDRESS?amount=133000047580000000000000000000",
  "qrcode": "data:image/png;base64.."
}
```

## Confirm Payment

> Perform a GET request on ```check``` URL to confirm payment.

**Payment Found:**

```json
{
    "id": "35c89c84",
    "success": true,
    "block": "8CE82716B4B431A229...50174F2444E7B24EFD",
    "amount": "0.0133001831",
    "amount_raw": "13300183100000000000000000000",
    "address": "PAYER_ADDRESS",
    "nanolooker": "https://nanolooker.com/block/8CE82716B4B431A229...50174F2444E7B24EFD",
    "json": "https://api.nano.to/checkout/35c89c84"
}
```

**Payment Not Found**

```json
{ 
  "error": 404,
  "message":"Payment not found."
}
```

## Back-End Usage

```js
const axios = require('axios');

axios.post('https://rpc.nano.to', {
  "action": "checkout",
  "title": "Hello World",
  "address": "@faucet",
  "currency": "USD", // default is NANO
  "plans": [
    { "title": "100 Units", "value": "100.00XXXX" },
    { "title": "1,000,000 Units", "value": "1000.00XXX" } 
  ],
  "webhook_url": "https://example/webhook/secret",
  "metadata": { "secret": "leroy-jenkins" }
})
```

**Response:**

```js
{
  "id": "CHECKOUT_ID",
  "browser": "https://nano.to/CHECKOUT_ID",
  "json": "https://api.nano.to/checkout/CHECKOUT_ID",
  "check": "https://api.nano.to/confirm/CHECKOUT_ID",
  "address": "YOUR_ADDRESS",
  "plans": [
    {
      "title": "100 Units",
      "value": "100.001845",
      "value_raw": "100001845000000000000000000000000",
      "link": "nano:YOUR_ADDRESS?amount=100001845000000000000000000000000",
      "qrcode": "data:image/png;base64..."
    },
    {
      "title": "1,000,000 Units",
      "value": "1000.00763",
      "value_raw": "1000007630000000000000000000000000",
      "link": "nano:YOUR_ADDRESS?amount=1000007630000000000000000000000000",
      "qrcode": "data:image/png;base64.."
    }
  ]
}
```

## Confirm Payment

> Perform a GET request on ```check``` URL to confirm payment.

**Payment Found:**

```json
{
    "id": "35c89c84",
    "success": true,
    "block": "8CE82716B4B431A229...50174F2444E7B24EFD",
    "address": "PAYER_ADDRESS",
    "nanolooker": "https://nanolooker.com/block/8CE82716B4B431A229...50174F2444E7B24EFD",
    "json": "https://api.nano.to/checkout/35c89c84",
    "amount": "1.001845",
    "amount_raw": "0018450000000000000000000000000",
    "plan": {
        "title": "100 Units",
        "value": "1.001845",
        "discount": false,
        "value_raw": "0018450000000000000000000000000"
    }
}
```

## Private Webhook

```json
{
    "block": {
        "hash": "786DD3F82BFEAF80A668EB87498531DE114F1A9BB7AF30558B4136AB69F5133E",
        "account": "PAYER_ADDRESS",
        "amount": "1.06239",
        "amount_raw": "1062390000000000000000000000000"
    },
    "plan": {
        "title": "100 Units",
        "value": "1.06239",
        "discount": false,
        "value_raw": "1062390000000000000000000000000"
    },
    "metadata": {
        "secret": "joe-doe"
    },
    "checkout": "https://api.nano.to/checkout/CHECKOUT_ID"
}
```

## NanoPay Support

[NanoPay.js](/nanopay) is a client-side Javascript library for easily adding Nano payments to any website.

Simply pass the Checkout ```id```. 

```html
<script src="https://pay.nano.to/latest.js"></script>

<script>
  // Pass the checkout.id to NanoPay.js
  NanoPay.open({ 
      checkout: checkout.id, // checkount from backe-end
      success: (block) => {
        console.log(block)
      }
  })
</script>
```

![](https://camo.githubusercontent.com/d2bdb483a89f85d5d2c9dc2a223e1732a468dd73dc22b7282e6d759333162951/68747470733a2f2f7062732e7477696d672e636f6d2f6d656469612f465f344b366636586f4141597450453f666f726d61743d6a7067266e616d653d6d656469756d)

## Unique Payments

If you'd like to receive payments that don't collide with other payments, you have to options:

- [Unique Payment Amount](#unique-amount)
- [Unique Nano Address](#unique-address)

## Unique Amount

Simply add 'X' to ```amount``` and the API will replace them with random numbers. 

```bash
curl -d '{
  "action": "checkout",
  "address": "@Development",
  "amount": "0.001000000XXXXXXXX"
}' \
-H "Content-Type: application/json" \
"https://rpc.nano.to"
```

**Response:**
```js
{
  "id": "8c1eb40e",
  "amount": "0.00100000084648542"
  // ...
}
```

## Unique Address

Unique payment address allow for simple payment amounts. To generate your own addresses locally, see [Developer Tools](https://hub.nano.org/developer-tools)

Nano.to [Cloud Wallets](/cloud) makes programmatic wallets easy. 

```js
const axios = require('axios');

axios.post('https://rpc.nano.to', {
  "action": "cloud_wallet",
  "refund_address": "YOUR_ADDRESS", // required
  "vanity": "1temp", // optional (slower)
  "expire": "5 minutes",
  "key": "NANO-TO-WALLET-API-KEY", // required
}).then((wallet) => {

  console.log(wallet.data);

  // {
  //   "balance": 0,
  //   "address": "nano_1temp9dzx8kmkbcpedwi...4bzoh3pafk9grxndk88inkbe",
  //   "refund_address": "YOUR_ADDRESS",
  //   "expiration": "in 5 minutes",
  //   "expiration_unix": 1710873173,
  // }

  axios.post('https://rpc.nano.to', {
    "action": "checkout",
    "address": wallet.data.address, // Cloud Wallet Address
    "random": false,
    "amount": 1 // Single digit amount
  }).then((checkout) => {

    console.log(checkout.data);

  });

});
```

## Payment Notifications 

**HTTP Webhook:**
```js
const axios = require('axios');

axios.post('https://rpc.nano.to', {
  "action": "checkout",
  "address": "@esteban",
  "amount": "0.133",
  "webhook": "https://example.com/secret/webhook",
  "metadata": { "note": 'Purchase', "userId": 123456789 }
}).then((res) => {
  console.log(res.data);
});
```

**Email Alerts:**
```js
const axios = require('axios');

axios.post('https://rpc.nano.to', {
  "action": "checkout",
  "address": "@esteban",
  "random": "true",
  "note": "Hello World",
  "notify": "john@apple.com",
}).then((res) => {
  console.log(res.data);
});
```

<img src="https://github.com/fwd/nano-docs/raw/master/images/email.jpeg" alt="line" style="
    height: auto;
    max-width: 510px;
">

**Discord Alerts:**
```js
const axios = require('axios');

axios.post('https://rpc.nano.to', {
  "action": "checkout",
  "address": "@esteban",
  "note": "Hello World",
  "notify": "https://discord.com/api/webhooks/11165660...",
}).then((res) => {
  console.log(res.data);
});
```

<img src="https://github.com/fwd/nano-docs/raw/master/images/discord.jpeg" alt="line" style="
    height: auto;
    max-width: 510px;
">

## Dedicated Support

- Email: business@nano.to
- Twitter: [@nano2dev](https://twitter.com/nano2dev)
- @nano2dev on [Nano's Discord](https://discord.com/invite/RNAE2R9) 

![line](https://github.com/fwd/n2/raw/master/.github/line.png)

## License

**Limited Commercial Use:**

- ✅ Personal & Open Source
- ✅ Commercial use where Nano.to Usernames / Checkout is a means.
- ❌ Commercial use where Nano.to Usernames / Checkout is re-sold.

Contact [@nano2dev](mailto:support@nano.to) for Usage/Licensing questions.
