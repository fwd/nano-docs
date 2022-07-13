# Nano.to PoW API

Standalone GPU powered, [proof of work](https://github.com/nanocurrency/nano-pow) (PoW) API for the Nano crypto-currency.

Easily scale any Nano application.

## Basic Usage

```
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

```js
{
    "difficulty": "fffffff8c69dbf5b",
    "multiplier": "1.1073958803041113",
    "work": "6f5a647cfe4a5dc4",
    "frontier": "E4094A9ABA876DC3E...",
    "remaining": 4
}
```

## Flexible API

Any of these URLs work. 

**Frontier Hash**
```
https://pow.nano.to/7FA158DADE3082...
```

**Nano Address**
```
https://pow.nano.to/nano_37y6iq8m1z..
```

**Nano.to Username**
```
https://pow.nano.to/@esteban
```

> Nano.to [Usernames](/username) enjoy Free 30 PoW / Per Minute.

## Curl Example

```
curl https://pow.nano.to/@fosse
```

## Difficulty

Proof of work is  ```fffffff800000000``` (or higher). Good for any Nano block.

- Providing your own ```difficulty``` is not supported.

## Rate Limit

- Free 5 PoW / Per Minute for Testing.
- Free 30 PoW / Per Minute, for Nano.to Usernames.
- Pre-pay for Usage @ Ӿ 0.01/PoW (**Coming Soon**)

## Errors Happen

Be ready for them. We recommend you **precache** work. By requesting it, and storing it, before you need it.

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