# Nano Email

Send Nano to any Email Address on the internet. 

Powered by Nano.to Enterprise API.

## Service Fee

- **Single Email**: Free
- **Batch Sending**: 0.1 NANO PER EMAIL

## Single Email

```bash
curl -d '{
  "action": "nano_email",
  "emails": "john@apple.com",
  "refund_address": "YOUR_NANO_ADDRESS",
  "amount": 10,
  "expire": "30 days"
}' \
-H "Content-Type: application/json" \
"https://rpc.nano.to"
```

**Response:**

```json
{
    "id": "d8d4c0c5",
    "address": "nano_3ah6roa747fcibspui3w41bp3qw96juxcozwi8n67kqe15cobec5imkkt9qu",
    "browser": "http://nano.to/id_d8d4c0c5",
    "check": "https://api.nano.to/confirm/d8d4c0c5",
    "amount": 10,
    "service_fee": 0,
    "qrcode": "data:image/png;base64,iVBORw0KGgoAAAAN...AAASUVORK5CYII=",
    "amount_raw": "10000000000000000000000000000000",
    "emails": [{
        "balance": 0,
        "address": "nano_15pcrp8qt3ohi7u4q14r3hccjcb1hfsoyk97p7ffm49hg7rft8b4a8znh7hf",
        "expiration": "in a month",
        "expiration_unix": 1713813910,
        "email": "john@apple.com",
        "amount": 10
    }]
}
```

## Batch Sending

```bash
curl -d '{
  "action": "nano_email",
  "emails": [ "john@apple.com", "jane@apple.com" ],
  "from": "ceo@apple.com",
  "message": "Free crypto from your favorite CEO",
  "refund_address": "YOUR_NANO_ADDRESS",
  "amount": 10,
  "expire": "30 days"
}' \
-H "Content-Type: application/json" \
"https://rpc.nano.to"
```

## Available Options

- **```emails```:** (*string or array*) Email of recipient(s).
- **```from```:** (*string*) Optional, Name or Email. Inform recipients who sent the Nano.
- **```amount```:** (*number*) Amount being sent. If multiple recipients, amount will be split evenly.
- **```message```:** (*string*) Add special message to email recipients.
- **```refund_address```:** (*string*) Your Nano address or @Username for refund of expired funds.
- **```expire```:** (*string*) Configure when funds expire and are returned to sender, in days.


**Response:**

```json
{
    "id": "f524bf87",
    "address": "nano_16bbqkd3umn6phhij19aq9zi6i5zstaeppz4i1i4b1qg5mjp8rc7pnt7shse",
    "browser": "http://nano.to/id_f524bf87",
    "check": "https://api.nano.to/confirm/f524bf87",
    "from": "ceo@apple.com",
    "message": "Free crypto from your favorite CEO",
    "subtotal": 10,
    "service_fee": 0.1,
    "amount": 10.1,
    "qrcode": "data:image/png;base64,iVBORw0KGgoA...SuQmCC",
    "amount_raw": "10100000000000000000000000000000",
    "emails": [{
        "balance": 0,
        "address": "nano_1ps6gf1uox5ep5cy93xr9fdswnguos86m3uthbusarmgy5ejx7cwpghx71ip",
        "expiration": "in a month",
        "expiration_unix": 1713814147,
        "email": "john@apple.com",
        "amount": 5
    }, {
        "balance": 0,
        "address": "nano_14jz9e3mgi95mw915yg1fysty86kazbszhsgbj13438if7uo3mcj1yf9yb6k",
        "expiration": "in a month",
        "expiration_unix": 1713814147,
        "email": "jane@apple.com",
        "amount": 5
    }]
}
```

## Confirm Payment

> Send funds to ```address``` and perform a GET request on ```check``` to complete.

```json
{
    "sent": true,
    "id": "35c89c84",
    "status": "https://api.nano.to/email/35c89c84"
}
```

![line](https://github.com/fwd/n2/raw/master/.github/line.png)

## Business Support

- Email: business@nano.to
- Twitter: [@nano2dev](https://twitter.com/nano2dev)
- @nano2dev on [Nano's Discord](https://discord.com/invite/RNAE2R9) 