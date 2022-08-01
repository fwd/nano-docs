# Nano PoW API

Standalone GPU powered, [proof of work](https://github.com/nanocurrency/nano-pow) (PoW) API for Nano currency.

Easily scale any Nano application.

## Basic Usage

```bash
GET: https://pow.nano.to/:HASH
```

or POST request:

```javascript
axios.post('https://pow.nano.to', { 
    hash: 'HASH'
}).then((res) => {
    // console.log(res.data)
})
```

**Response (JSON):**

```json
{
    "difficulty": "fffffffd316c7962",
    "multiplier": "2.8500801896655417",
    "work": "14b651936a358ddc",
    "frontier": "8AF8007D1E31294232C62F4495E657C2A3CA80FA2A1B98ADE5B6E1336C722EC6",
    "remaining": 4,
    "cached": true,
    "duration": "0.334s"
}
```

## Flexible API

**Frontier Hash**

```text
https://pow.nano.to/7FA158DADE3082...
```

**Nano Address**

```text
https://pow.nano.to/nano_37y6iq8m1z..
```

**Nano.to Username**

```text
https://pow.nano.to/@esteban
```

## Curl Example

```
curl https://pow.nano.to/@fosse | jq '.work'
```

## Difficulty

Proof of work is  ```fffffff800000000``` (or higher). Good for any Nano block.

> Providing your own ```difficulty``` is not supported.

## Rate Limit

- Free 5 PoW / Per Minute for Testing.
- Pre-pay for Usage @ Ӿ 0.001/PoW (**Coming Soon**)

## Errors Happen

We recommend you **precache** work. By requesting it, and storing it, before you need it.

**Code 400: Bad Request:**

```js
{ 
    "error": 400,  
    "message": "Missing Hash.",
    "docs": 'https://docs.nano.to/pow'
}
```

**Code 429: Exhausted Credits:**

```js
{
    "error": 429,
    "message": "Too many requests. Please Wait."
}
```

**Code 500: No GPU available:**

```js
{
    "error": 500, 
    "message": "No GPU available. Try again in a few seconds."
}
```

**Code 501: Service Offline:**

```js
{
    "error": 501, 
    "message": "Service not available. Try again in a few minutes."
}
```

## Questions or Comments? 

- Email: support@nano.to
- Twitter: [@nano2dev](https://twitter.com/nano2dev)
- @nano2dev on [Nano Discord](https://discord.com/invite/RNAE2R9) 