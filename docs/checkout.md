# Checkout API

Free, non-custodial Checkout API for the Nano blockchain.

Build elaborate Nano currency checkouts with ease.

```js
const axios = require('axios');

axios.post('https://rpc.nano.to', {
  "action": "checkout",
  "title": "Hello World",
  "address": "@faucet",
  "cancel_url": "https://example.com/cancel",
  "success_url": "https://example.com/success",
  "success_message": "{{title}} Units purchased for {{value}} NANO. Thanks, come again.",
  "currency": "USD", // Default is NANO
  "plans": [
    { 
      "title": "100 Units", 
      "value": "100.00XXXX"
    },
    { 
      "title": "1,000,000 Units", 
      "value": "1000.00XXX"
    }
  ],
  "webhook_url": "https://example/webhook/secret",
  "metadata": { "secret": "joe-doe" }
})
```

**Response:**

```js
{
    "id": "CHECKOUT_ID",
    "browser": "https://nano.to/CHECKOUT_ID",
    "check": "https://api.nano.to/check/CHECKOUT_ID",
    "json": "https://api.nano.to/checkout/CHECKOUT_ID"
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

[NanoPay.js](/nanopay) is a client-side Javascript library for secure Nano payments.

It supports Checkouts by simply passing the ```id```. 

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

Simply add 'X' to the ```amount``` and the API will replace them with random numbers. 

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

[Cloud Wallets](/cloud) makes generating unique payment addresses easy. 

```js
const axios = require('axios');

axios.post('https://rpc.nano.to', {
  "action": "cloud_wallet",
  "refund_address": "YOUR_ADDRESS",
  "expire": "5 minutes"
}).then((cloudWallet) => {

  console.log(cloudWallet.data);

  // {
  //   "balance": 0,
  //   "address": "nano_1temp9dzx8kmkbcpedwi...4bzoh3pafk9grxndk88inkbe",
  //   "api_key": "NANO-WALLET-API-KEY-67353C9E78A34474A977....591AAD07D37FB94F84C",
  //   "refund_address": "YOUR_ADDRESS",
  //   "expiration": "in 5 minutes",
  //   "expiration_unix": 1710873173,
  // }

  axios.post('https://rpc.nano.to', {
    "action": "checkout",
    "address": cloudWallet.data.address, // Cloud Wallet Address
    "random": "true",
    "amount": "1" // Simple payment amount
  }).then((checkout) => {

    console.log(checkout.data);

  });

});
```

> To generate addresses locally, see [Developer Tools](https://hub.nano.org/developer-tools).

## Payment Alerts 

```js
const axios = require('axios');

axios.post('https://rpc.nano.to', {
  "action": "checkout",
  "address": "@esteban",
  "random": "true",
  "note": "Nano Bird Feeder",
  "notify": "john@apple.com",
}).then((res) => {
  console.log(res.data);
});
```

<img src="https://github.com/fwd/nano-docs/raw/master/images/email.jpeg" alt="line" style="
    height: auto;
    max-width: 510px;
">

```js
const axios = require('axios');

axios.post('https://rpc.nano.to', {
  "action": "checkout",
  "address": "@esteban",
  "random": "true",
  "note": "Nano Pizza App",
  "notify": "https://discord.com/api/webhooks/11165660...",
}).then((res) => {
  console.log(res.data);
});
```

<img src="https://github.com/fwd/nano-docs/raw/master/images/discord.jpeg" alt="line" style="
    height: auto;
    max-width: 510px;
">

## Nano.to Support

- Email: support@nano.to
- Twitter: [@nano2dev](https://twitter.com/nano2dev)
- @nano2dev on [Nano's Discord](https://discord.com/invite/RNAE2R9) 

![line](https://github.com/fwd/n2/raw/master/.github/line.png)

## License

**Limited Commercial Use:**

- ✅ Personal & Open Source
- ✅ Commercial use where Nano.to Usernames / Checkout is a means.
- ❌ Commercial use where Nano.to Usernames / Checkout is re-sold.

Contact [@nano2dev](mailto:support@nano.to) for Usage/Licensing questions.
