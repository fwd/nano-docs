# NanoPay.js

Non-custodial web payment library for the Nano blockchain. 

Easily create elaborate payment flows.

![](https://camo.githubusercontent.com/d2bdb483a89f85d5d2c9dc2a223e1732a468dd73dc22b7282e6d759333162951/68747470733a2f2f7062732e7477696d672e636f6d2f6d656469612f465f344b366636586f4141597450453f666f726d61743d6a7067266e616d653d6d656469756d)

## Live Demo

[https://pay.nano.to](https://pay.nano.to)

## Edit on CodePen

[https://codepen.io/nano2dev/pen/VwRQypE](https://codepen.io/nano2dev/pen/VwRQypE)

## Installation

**CDN:**
```html
<script src="https://pay.nano.to/latest.js"></script>
```

**Local:**
```html
<script src="/NanoPay.js"></script>
```

Download [latest](https://pay.nano.to/latest.js) version.

## Simple Usage

Payment buttons can be created with basic HTML. No javascript code required. 

```html
<a 
data-title="Tip @Nano2Dev" 
data-amount="0.133" 
data-address="@development" 
data-button="Open Natrium" 
data-position="bottom">
Tip 0.133 NANO</a>
```

## JavaScript API

Configure and open popup programmatically with *NanoPay.open()* method.

```javascript
NanoPay.open({ 
  title: "Demo",
  address: '@development', // Username or Nano Address
  notify: 'support@nano.to', // get an email receipt
  contact: true, // user's email
  shipping: 10, // user's shipping address, use 'true' for free shipping
  currency: 'EUR', // converts prices EUR, default USD
  // amount: 30, // not used if using line_items
  line_items: [
    { name: "Shirt (X-Small)", price: 50 }, 
    { name: "Mens Shoes (9.5)", price: 20 }
  ],
  success: (block) => {
      console.log(block)
      // {
      //     "hash": "D16FF348B634CDB3DF8...9D6F5B180CCD3B93F99A4D15203",
      //     "amount": "NANO_AMOUNT_PAID",
      //     "address": "PAYEE_NANO_ADDRESS",
      //     "username": "PAYEE_USERNAME",
      //     "height": "PAYEE_BLOCK_HEIGHT",
      //     "shipping": "PAYEE_SHIPPING_ADDRESS",
      //     "email": "PAYEE_EMAIL_ADDRESS",
      //     "nanolooker": "https://nanolooker.com/block/D16FF348B634CDB3DF8...9D6F5B180CCD3B93F99A4D15203"
      //     "checkout": "https://api.nano.to/checkout/93be1ab9",
      // }
  },
  cancel: () => {
      console.log("User cancelled")
  },
})
```

## All Options

- ```title```: (*string*) Show custom title shown in popup.
- **address**: (*string*) Nano address or Nano.to @Username.
- **contact**: (*string*) User's email address.
- **shipping**: (*number or bool*) User's mailing address. 'true' for free shipping.
- **position**: (*string*) Control popup position (top, center, bottom).
- **wallet**: (*string*) Custom wallet icon: natrium, nault, nautilus, cake
- **button**: (*string*) Custom button text, default "Open Natrium".
- **symbol**: (*string*) Custom NANO symbol, default "NANO".
- **random**: (*bool*) Use unique payment amounts, default true.
- **notify**: (*string*) Send email notification to admin, default false.
- **amount**: (*string*) Custom popup amount, used for simple payments.
- **line_items**: (*array*) List of products user is buying, replaces amount.
- **currency**: (*string*) Fiat currency for Nano price conversion, default "USD".
- **note**: (*string*) Custom note shown in admin email, default false.
- **qrcode**: (*string*) Always show QR Code, default desktop only.
- **checkout**: (*string*) Nano.to Checkout ID. [Read More](/checkout).
- **email**: (*string*) Pre-configure user's email
- **expiration**: (*number*) Duration for completion in milliseconds.
- **mailing_address**: (*string*) Pre-configure user's shipping address
- **success**: (*function*) Called when payment is successful.
- **cancel**: (*function*) Called when popup is cancelled.
- **expired**: (*function*) Called when popup has expired.


## Checkout Support

NanoPay.js supports [Checkout API](/checkout). Securely create Checkouts in the back-end, then pass the Checkout ID to NanoPay.js 

```js
// Create a checkout (ideally in a secure back-end)
var checkout = (await axios.post('https://rpc.nano.to', { 
    action: 'checkout',
    description: "Invoice #284", // recommended
    notify: 'support@nano.to', // optional
    plans: [
        { "title": "200 Sky Coins", "value": "0.13300000XXXX" },
        { "title": "200 Sky Coins", "value": "0.13300000XXXX" },
    ],
    address: '@bank', // your_address
    domain: 'my_vue_app', // app_name
    webhook: 'http://secret_endpoint.com/webhook' // optional
})).data

// Pass the checkout.id to NanoPay.js
NanoPay.open({ 
    checkout: checkout.id,
    qrcode: true, // always show qrcode
    success: (block) => {
        console.log(block)
    }
})
```

> [Read Checkout API Docs](/checkout)

## Timed Checkout

By default, NanoPay does not limit Checkout time. If you'd like to, you can use ```expiration``` and ```expired```. A countdown will be shown next to ```description```.

```js
function showNanoPay() {
  NanoPay.open({ 
    address: '@bank', // Your App's Address
    amount: "0.13300XXXX", // Amount with random decimals
    description: "Checkout",
    expiration: 5 * 60, // 5 minutes in ms
    currency: 'USD',
    expired: () => {
      showNanoPay() // call again to reset
    },
    success: (block) => {
        // {
        //     "hash": "D16FF348B634CDB3DF8...9D6F5B180CCD3B93F99A4D15203",
        //     "address": "PAYEE_NANO_ADDRESS",
        //     "username": "PAYEE_USERNAME",
        //      ...
        // }
        console.log("Hello:", block.username || block.address)
    }
  })
}

showNanoPay() // call initially
```

## Login with Nano

NanoPay makes Login with Nano easy. 

```js
NanoPay.open({ 
  title: "Login",
  address: '@bank', // Your App's Address
  amount: 0.0001, // Small Amount
  success: (block) => {
      // {
      //     "hash": "D16FF348B634CDB3DF8...9D6F5B180CCD3B93F99A4D15203",
      //     "address": "PAYEE_NANO_ADDRESS",
      //     "username": "PAYEE_USERNAME",
      //      ...
      // }
      console.log("Hello:", block.username || block.address)
  }
})
```

## HTML Content Paywall

![](../images/nano-blog/hero-small.jpg)

NanoPay includes an easy way to monetize any website client-side. 

> Please note, this method does not use a back-end, it's not for keeping secrets from public. Google bots can still crawl content.

```html
<style>
/* This css prevents flash of content on page load */
.premium { display: none; } 
</style>
<article class="premium">
  Lorem ipsum dolor sit, amet consectetur, adipisicing elit. Amet tenetur ab reprehenderit temporibus, illum recusandae nostrum iusto omnis repellendus id quae ullam reiciendis dolorem aliquam fuga, tempora iste animi.
</article>
```

```js
NanoPay.wall({ 
    element: '.premium',
    title: 'Read Story',
    button: 'Unlock Story', 
    free: true, // Allow free reading
    amount: 0.001, // Cost of Article
    address: '@development', // Your Nano Address or Username
    success: (block) => {
      // do stuff like render highlight.js
      console.log("Thanks for reading:", block.username || block.address)
    }
})
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

![](https://github.com/fwd/nano-docs/raw/master/images/email.jpeg)


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

![](https://github.com/fwd/nano-docs/raw/master/images/discord.jpeg)

## eCommerce Intergration

- **Shopify: In Development**
- **Wordpress: TBD**

**I work on Nano part-time. Please consider helping fund this kind of work.**

[Nano.to/Development](https://nano.to/development)

## Nano.to Support

Bugs, Questions & Installation Support:

- Github: [Source Code](https://github.com/fwd/nano-pay)
- Issues: [Issues](https://github.com/fwd/nano-pay/issues)
- Support: [support@nano.to](mailto:support@nano.to)
- Twitter: [@nano2dev](https://twitter.com/nano2dev)
- Mastodon: [Xno.Social](https://xno.social/@nano2dev)
- @nano2dev on [Nano's Discord](https://discord.com/invite/RNAE2R9) 
