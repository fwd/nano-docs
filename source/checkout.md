# Checkout UI

Free hosted checkout pages, for your Nano Address and Nano.to Username.


![](images/checkout.png)

## Basic Usage

```
https://nano.to/:YOUR_ADDRESS
```

**Optional:**

- https://nano.to/@moon
- https://xno.to/@moon?price=100
- https://ӿ.to/YOUR_ADDRESS

> Just need the QR Code? See [QR Code API](/qrcode).

```
GET https://nano.to/NANO_ADDRESS_OR_USERNAME?title=Coffee
```

Live Demo: [https://xno.to/Moon](https://nano.to/Moon?title=Coffee&price=5&image=https://media-cldnry.s-nbcnews.com/image/upload/t_nbcnews-fp-1200-630,f_auto,q_auto:best/newscms/2019_33/2203981/171026-better-coffee-boost-se-329p.jpg)

***HTML***

```html
<a href="https://nano.to/Moon?title=Coffee&price=5&image=https://media-cldnry.s-nbcnews.com/image/upload/t_nbcnews-fp-1200-630,f_auto,q_auto:best/newscms/2019_33/2203981/171026-better-coffee-boost-se-329p.jpg">https://nano.to/Moon</a>
```

***Markdown***

```markdown
Live Demo: [https://nano.to/Moon](https://nano.to/Moon?title=Coffee&price=5&image=https://media-cldnry.s-nbcnews.com/image/upload/t_nbcnews-fp-1200-630,f_auto,q_auto:best/newscms/2019_33/2203981/171026-better-coffee-boost-se-329p.jpg)
```

## Options

```bash
https://nano.to/Moon?title=Donate
&price=50
&donate=false
&color=white
&currency=USD
&background=blue,red
&image=https://media3.giphy.com/media/cnuNz0fTBIUGnx4F9T/giphy.gif
&description=<p>HTML allowed 😎</p>
&suggest=Basic:30,Premium:50
&success_url=https://mywebsite.com/success
&cancel_url=https://mywebsite.com/
```

> ***Note:*** When using **GET**, CSS colors with hashtags ex. #000000 are supported, but replace the **#** with a **$** symbol. This is a URL limitation. This is not an issue with POST requests. See below. 

***HTML***

```html
<a href="https://nano.to/ADDRESS_OR_USERNAME">Donate with Nano</a>
```

***Markdown***

```
[Tip me $5](https://nano.to/Moon?price=5)
```

Demo: [Tip me in Nano](https://nano.to/Moon)

## Customize More

More advanced and sensitive data can be passed in the body of a POST request. 

```
POST: https://nano.to/NANO_ADDRESS_OR_USERNAME
```

```javascript
// npm install axios
const axios = require('axios')

axios.post('https://nano.to/NANO_ADDRESS_OR_USERNAME', {
    "title": "New Order",
    "currency": "USD", // any valid ISO string
    "plans": [
        { "name": "Fries", "price": 5 },
        { "name": "Burger", "price": 10 },
        { "name": "Happy Meal", "price": 15 },
        { "name": "Cookies 🍪", "price": 3 }
    ],
    "business": {
        "name": "McDonalds",
        "logo": "https://www.tailorbrands.com/wp-content/uploads/2020/07/mcdonalds-logo.jpg"
    },
    "image": "https://files.muzli.space/2d7af141fab097859ef66de8d7c50932.jpeg", 
    "color": "black,white",
    "background": "#00000,#311ac5",
    "success_url": "https://mywebsite.com/success?id={{id}}&anotherParam=hello",
    "cancel_url": "https://google.com",
    "webhook_url": "https://mywebsite.com/super-secret-webhook",
    "webhook_secret": "my-super-secret",
    "metadata": { "userId": "joe-mama" }
})
```

## Response:

```
{
    "id": "666ee7bf26a",
    "url": "https://nano.to/checkout/666ee7bf26a",
    "exp": "2021-09-23T01:51:23.853Z"
}
```

## Notifications

The recommended way to be notified of incoming payments is by passing a 'webhook_url' param in the body of a POST request. The JSON payload will look like this:

```javascript
{
    id: '6e9d1f58c40',
    status: 'complete',
    amount: 1,
    method: {
        symbol: 'nano',
        address: 'YOUR_ADDRESS',
        name: 'Nano',
        rate: '5.43262',
        amount: '0.18621',
        value: '1.01',
        raw: false
    },
    plan: {
        price: 1,
        name: '1 Month'
    },
    block: {
        type: 'pending',
        amount: '0.18621',
        hash: '6EE79D2BA2A8995179..',
        source: 'THEIR_ADDRESS',
        amount_raw: '1862100000000..'
    },
    metadata: {
        id: 'joe-mama'
    }
}
```

**Your server listening for POST request, would look like this:**

```js
// npm install fwd/server
const server = require('@fwd/server')

// listen at this path, with a POST method.
server.post('/super-secret-webhook', (req, res) => {
    console.log(req.body) // data from example above
    res.send("Ok")
})
// start server
server.start(8080)
```

## Multiple Currency Support

```
https://nano.to/Moon?currency=RUB
```

![](../assets/checkout-rub.png)

## Single Panel UI

When no ```plans``` are provided, there is no need for the left side of the Checkout UI. 

```
https://nano.to/Moon?pay=100
```

> When setting the price, you can use ```pay```, ```price``` or ```amount```. They all work the same.

![](../assets/checkout-single.png)

## Checkout Metadata

Pass a ```?json=true``` URL flag to the ```url``` in the Response to get a JSON object of the Checkout. 

> In most cases you do don't need this.

```
https://nano.to/checkout/666ee7bf26a?json=true
```

## Vanity Highlight

With ```vanity_start``` and ```vanity_end``` params, you can control how your address is presented.

```js
https://nano.to/Moon?vanity_start=10&vanity_end=4
```

![](../assets/address_highlight.png)

## Wallet Deep Linking

Clicking (or Tapping) the QR Code will open Natrium and automatically fill in amount and address, on most phones. 

## Github Markdown Support

When creating links in Markdown (or HTML), use **two** underscores (\_\_) instead of spaces, and it will read as spaces. Makes for cleaner links.

```
https://nano.to/Moon?title=I__Love__Apples
```

## Data Deletion Policy

Most of the data provided by Nano.to comes from the Nano Blockchain. Nano.to only stores Usernames leases and Checkout metadata. Checkout metadata is stored in-memory and is deleted after 24 hours. It's cheaper to NOT store your data. Who could have guessed. 