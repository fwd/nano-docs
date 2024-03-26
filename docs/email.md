# Nano Email

Send nano to any email address(s) on the internet. 

Nano on-boarding made easy.

![line](https://github.com/fwd/n2/raw/master/.github/line.png)
<img src="https://github.com/fwd/nano-docs/raw/master/images/nano-email.png">
![line](https://github.com/fwd/n2/raw/master/.github/line.png)

## Online UI

[https://email.nano.to ](https://email.nano.to )

## Service Fee

- **Single Email**: FREE
- **Batch Sending**: 0.1 NANO / EMAIL

## Single Email

```bash
curl -d '{
  "action": "nano_email",
  "email": "john@apple.com",
  "refund_address": "YOUR_NANO_ADDRESS",
  "amount": 10,
  "expire": "30 days",
  "email_receipt": "OPTIONAL_YOUR_EMAIL"
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

## Available Options

- **```emails```:** (*string or array*) Email of recipient(s).
- **```from```:** (*string*) Optional, Name or Email. Inform recipients who sent the Nano.
- **```amount```:** (*number*) Amount being sent. If multiple recipients, amount will be split evenly.
- **```message```:** (*string*) Add special message to email recipients.
- **```refund_address```:** (*string*) Your Nano address or @Username for refund of expired funds.
- **```expire```:** (*string*) Configure when funds expire and are returned to sender, in days.
- **```email_receipt```:** (*string*) Get notified via email when funds are accepted.
- **```webhook_url```:** (*string*) Notify your app when funds are accepted.

## Webhook POST

```json
{
    "id": "f524bf87",
    "success": true,
    "checkout": "https://api.nano.to/checkout/f524bf87",
    "recipients": [
        {
            "email": "john@apple.com",
            "amount": 5,
            "hash": "E2FB233EF4554...78AB89917D3",
            "explorer": "https://nanobrowse.com/block/E2FB233EF4554...78AB89917D3"
        },
        {
            "email": "jane@apple.com",
            "amount": 5,
            "hash": "67D9F9F035...3CEA098FBF49D",
            "explorer": "https://nanobrowse.com/block/67D9F9F035...3CEA098FBF49D"
        }
    ]
}
```

![line](https://github.com/fwd/n2/raw/master/.github/line.png)

## Dedicated Support

- Email: business@nano.to
- Twitter: [@nano2dev](https://twitter.com/nano2dev)
- @nano2dev on [Nano's Discord](https://discord.com/invite/RNAE2R9) 