# Nano Aliases

Open source, alias service for the Nano blockchain.

**Register Online**

- [nanoBrowse.com](https://nanobrowse.com)
- [Nanolooker.com](https://nanolooker.com) (**Coming Soon**)

**Or via RPC**

```bash
curl -d '{
  "action": "get_alias",
  "alias": "My Custom Alias"
}' \
-H "Content-Type: application/json" \
"https://rpc.nano.to"
```

**Response:**

```json
{
    "id": "60749b48",
    "address": "nano_371muxntgdckg3wfrisatirzb8prmifromr6jkuoii9nzqspjyca57tqgacw",
    "browser": "http://nano.to/id_60749b48",
    "check": "https://api.nano.to/confirm/60749b48",
    "amount": 1,
    "amount_raw": "100000000000000000000000000000",
    "created_at": 1710865376655,
    "qrcode": "data:image/png;base64,iVBORw...FTkSuQmCC"
}
```

## Confirm Payment

> Send 1 NANO to provided ```address``` and do a GET request on ```check``` URL to confirm payment.

**Payment Found:**

```json
{
    "id": "35c89c84",
    "success": true,
    "block": "8CE82716B4B431A229...50174F2444E7B24EFD",
    "alias": "My Custom Alias",
    "address": "YOUR_ADDRESS"
    // ...
}
```

![line](https://github.com/fwd/n2/raw/master/.github/line.png)

## NanoPay Support

[NanoPay.js](/nanopay) makes it easy to register Nano Aliases on any website. 


```html
<script src="https://pay.nano.to/latest.js"></script>
<script>
  NanoPay.open({ 
      alias: true,
      address: 'WEBSITE_ADMIN_ADDRESS', // Revenue share system
      success: (block) => {
        console.log(block)
      }
  })
</script>
```

<img src="https://github.com/fwd/nano-docs/raw/master/images/nanopay-alias.png" alt="line" style="
    height: auto;
    max-width: 510px;
">

## Nano.to Support

- Email: support@nano.to
- Twitter: [@nano2dev](https://twitter.com/nano2dev)
- @nano2dev on [Nano's Discord](https://discord.com/invite/RNAE2R9) 