# Public RPC

Access to a public Nano node, without paying to host a node. 

![line](https://github.com/fwd/n2/raw/master/.github/line.png)

**Supported Actions:**
- pending
- process
- telemetry
- receivable
- account_key
- account_info
- nano\_to\_raw
- raw\_to\_nano
- [work_generate](/pow)
- work_validate
- account_history

![line](https://github.com/fwd/n2/raw/master/.github/line.png)

## Basic Usage

```js
axios.post('https://rpc.nano.to', { 
    action: "telemetry"
}).then((res) => {
    // console.log(res.data)
})
```

**Response (JSON):**
```json
{
    "block_count": "175503263",
    "cemented_count": "175503240",
    "unchecked_count": "158",
    "account_count": "30998653",
    "bandwidth_cap": "10485760",
    "peer_count": "217",
    "protocol_version": "19",
    "uptime": "3941513",
    "genesis_block": "991CF190094C00F0B68E2E5F75F6BEE95A2E0BD93CEAA4A6734DB9F19B728948",
    "major_version": "24",
    "minor_version": "0",
    "patch_version": "0",
    "pre_release_version": "0",
    "maker": "0",
    "timestamp": "1676833902409",
    "active_difficulty": "fffffff800000000"
}
```

![line](https://github.com/fwd/n2/raw/master/.github/line.png)

## Rate Limit

- 60 / Per Minute (1 / Second)
- Unlimited [Prepaid RPC](https://pow.nano.to) @ Ӿ 0.001/CALL

![line](https://github.com/fwd/n2/raw/master/.github/line.png)

## Errors Happen

- **Error 4XX**: Your fault.
- **Error 5XX**: Our fault.

**Code 400: Bad Request:**

```js
{ 
    "error": 400,  
    "message": "Bad action provided.",
    "docs": 'https://docs.nano.to/pow'
}
```

**Code 429: Exhausted Credits (No API Key):**

```js
{
    "error": 429,
    "message": "Too many requests. Please Wait."
}
```

**Code 500: No Node available:**

```js
{
    "error": 500, 
    "message": "No Node available. Try again in a few seconds."
}
```

**Code 501: Service Unavailable:**

```js
{
    "error": 501, 
    "message": "Service not available. Try again in a few minutes."
}
```

![line](https://github.com/fwd/n2/raw/master/.github/line.png)

## Nano.to Support

- Email: support@nano.to
- Twitter: [@nano2dev](https://twitter.com/nano2dev)
- @nano2dev on [Nano's Discord](https://discord.com/invite/RNAE2R9) 
