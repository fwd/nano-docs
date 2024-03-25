# Nano Email

Send Nano to any email address on the internet. 

![line](https://github.com/fwd/n2/raw/master/.github/line.png)
<img src="https://github.com/fwd/nano-docs/raw/master/images/nano-email.png">
![line](https://github.com/fwd/n2/raw/master/.github/line.png)

## Online UI

[https://email.nano.to ](https://email.nano.to )

## Service Fee

- **Single Email**: FREE
- **Batch Sending**: 0.1 NANO PER EMAIL

## Single Email

```bash
curl -d '{
  "action": "nano_email",
  "email": "john@apple.com",
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
    "emails": [
        {
            "email": "john@apple.com",
            "amount": 5
        }, 
        {
            "email": "jane@apple.com",
            "amount": 5
        }
    ]
}
```

## Confirm Payment

> Send funds to ```address``` and perform a GET request on ```check``` to complete.

```json
{
    "sent": true,
    "id": "35c89c84"
}
```

## Available Options

- **```emails```:** (*string or array*) Email of recipient(s).
- **```from```:** (*string*) Optional, Name or Email. Inform recipients who sent the Nano.
- **```amount```:** (*number*) Amount being sent. If multiple recipients, amount will be split evenly.
- **```message```:** (*string*) Add special message to email recipients.
- **```refund_address```:** (*string*) Your Nano address or @Username for refund of expired funds.
- **```expire```:** (*string*) Configure when funds expire and are returned to sender, in days.


![line](https://github.com/fwd/n2/raw/master/.github/line.png)

## Business Support

- Email: business@nano.to
- Twitter: [@nano2dev](https://twitter.com/nano2dev)
- @nano2dev on [Nano's Discord](https://discord.com/invite/RNAE2R9) 