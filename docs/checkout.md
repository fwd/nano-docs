## Nano Checkout

Free non-custodial Checkout API for the Nano blockchain.

```js
const axios = require('axios');

axios.post('https://rpc.nano.to', {
  "action": "checkout",
  "title": "Hello World",
  "address": "@faucet",
  "random": "true",
  "cancel_url": "https://example.com/cancel",
  "success_url": "https://example.com/success",
  "success_message": "{{title}} Units purchased for {{value}} NANO. Thanks, come again.",
  "plans": [
    {
      "title": "100 Units",
      "value": 100
    },
    {
      "title": "1,000,000 Units",
      "value": 1000000,
      "discount": 10
    }
  ],
  "webhook_url": "https://example/webhook/secret",
  "metadata": {
    "secret": "joe-doe"
  }
}).then((res) => {
  console.log(res.data);
});
```

**Response:**

```json
{
    "id": "CHECKOUT_ID",
    "browser": "https://nano.to/CHECKOUT_ID",
    "check": "https://api.nano.to/check/CHECKOUT_ID",
    "json": "https://api.nano.to/checkout/CHECKOUT_ID",
}
```

## NanoPay.js Support

NanoPay.js supports [Checkout API](/checkout) just pass the Checkout ```id```.

```js
// Pass the checkout.id to NanoPay.js
NanoPay.open({ 
    checkout: checkout.id,
    debug: true,
    qrcode: true, // always show qrcode
    success: (block) => {
        console.log(block)
    }
})
```

![](https://camo.githubusercontent.com/d2bdb483a89f85d5d2c9dc2a223e1732a468dd73dc22b7282e6d759333162951/68747470733a2f2f7062732e7477696d672e636f6d2f6d656469612f465f344b366636586f4141597450453f666f726d61743d6a7067266e616d653d6d656469756d)

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

## Unique Payments

If you'd like to create unique Checkouts, you have to options

- Unique Nano Address
- Unique Payment Amounts

When creating a Checkout add 'X' to the amount and the API will replace them with random numbers. 

```bash

curl -d '{
  "action": "checkout",
  "address": "@Development",
  "amount": "0.001000000XXXXXXXX"
}' \
-H "Content-Type: application/json" \
"https://rpc.nano.to"

```

```json
{
  "id": "8c1eb40e",
  "amount": "0.00100000084648542"
  ...
}
```

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
