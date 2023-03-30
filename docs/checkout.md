## Nano.to Checkout

![line](https://github.com/fwd/n2/raw/master/.github/line.png)

Non-custodial Checkout API hosted on Github. Alerts your applications and/or infrastructure when configured. 

![line](https://github.com/fwd/n2/raw/master/.github/line.png)

**Nano Address:**
```python
https://nano.to/:ADDRESS
```

**Nano.to Username:**
```python
https://nano.to/Fosse
```

![line](https://github.com/fwd/n2/raw/master/.github/line.png)


### Single Panel

```python
https://nano.to/@Fosse?amount=50
```

<img src="https://github.com/fwd/nano/raw/master/dist/images/single-ui.png" alt="Single Panel UI" />

![line](https://github.com/fwd/n2/raw/master/.github/line.png)

### Double Panel

```python
https://nano.to/@Moon?plans=Tip:0.133,Small:1,Medium:10,Large:20,Gigantic:100
```

<img src="https://github.com/fwd/nano/raw/master/dist/images/double-ui.png" alt="Single Panel UI" />

![line](https://github.com/fwd/n2/raw/master/.github/line.png)

## Customize Colors

```python
https://nano.to/@Keeri
?background=$0057b7:$ffd700
&color=$FFF:$000
&highlight=white
&vanity=$0057b7
&qrcode=white:$0057b7
&logo=https://nano.to/dist/logo/cyber.png
```

<img src="https://github.com/fwd/nano/raw/master/dist/images/slava-ui.png" alt="Single Panel UI" />

![line](https://github.com/fwd/n2/raw/master/.github/line.png)

### Available Options

- **amount** (number) : Single panel with price. No plans.
- **plans** (string) : Plans separated by commas. Ex. Tip:30,Small:5
- **selected** (string) : Title of Plan to select by default.
- **goal** (string) : Show a funding meter based off balance.
- **image** (image/url) : Display Image. Image URL.
- **color** (string) : Text color. Ex red:blue
- **background** (string) : Background color. Ex white:gray
- **highlight** (string) : Box backgrounds value. Ex blue:red
- **qrcode** (string) : Replace QR Code color. Ex white:black
- **logo** (image/url) : Replace QR Code logo. Image URL.
- **cancel** (string) : Redirect URL when pressed 'Cancel'
- **redirect** (string) : Redirect URL on success.
- **currency** (string) : ISO Currency Symbol. Ex JPY

![line](https://github.com/fwd/n2/raw/master/.github/line.png)

### Funding UI

Easily show a meter of progress for any Nano fundraiser. 

```python
https://nano.to/@Basedlemahieu?goal=100:Funding Goal
```

<img src="https://github.com/fwd/nano/raw/master/dist/images/funding.png" alt="Single Panel UI" />

![line](https://github.com/fwd/n2/raw/master/.github/line.png)

### Checkout with POST

```js
const axios = require('axios');

axios.post('https://api.nano.to', {
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

**Webhook:**

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

## Nano.to Support

- Email: support@nano.to
- Twitter: [@nano2dev](https://twitter.com/nano2dev)
- @nano2dev on [Nano's Discord](https://discord.com/invite/RNAE2R9) 

![line](https://github.com/fwd/n2/raw/master/.github/line.png)


## License

**Limited Commercial Use:**

- ✅ Personal & Open Source
- ✅ Nano.to Usernames / Checkout UI is a means to an end.
- ❌ Nano.to Usernames / Checkout UI is re-branded, monetized.

Contact [@nano2dev](mailto:support@nano.to) for Usage/Licensing questions.
