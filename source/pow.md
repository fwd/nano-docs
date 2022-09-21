# Nano.to PoW API

Standalone, GPU powered proof of work API for the Nano blockchain.

Easily scale any Nano application.

## Basic Usage

```python
https://pow.nano.to/:HASH
```

**or POST request:**
```javascript
axios.post('https://pow.nano.to', { 
    hash: ':HASH'
}).then((res) => {
    // console.log(res.data)
})
```
**Response (JSON):**
```json
{
    "difficulty": "fffffffbc3b93c36",
    "multiplier": "1.888817235874546",
    "work": "157ad78255c73cae",
    "frontier": "277FD6365DF608D601F18F464926B600B15F6CD705A90E2239F55E9F86E7B38F",
    "remaining": 4,
    "cached": false,
    "duration": "0.201s",
    "server": "Nano.to/GPU-4"
}
```

## CURL Example

```
curl https://pow.nano.to/:HASH | jq '.work'
```

## Difficulty

Proof of work is  ```fffffff800000000``` (or higher). Good for any Nano block.

> Providing your own ```difficulty``` is not supported. 

## Rate Limit

- Unlimited 5 PoW / Per Minute.
- Unlimited 10 PoW / Per Minute with [Free API Key](https://pow.nano.to/).
- [Prepaid PoW](https://pow.nano.to) @ Ӿ 0.01/PoW

## Errors Happen

**Precache** work by requesting it, and storing it, before you need it.

- **Error 4XX**: Your fault.
- **Error 5XX**: Our fault.

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
- @nano2dev on [Nano's Discord](https://discord.com/invite/RNAE2R9) 
