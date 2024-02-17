# Nano Names

Open source, non-custodial name service for the Nano blockchain.

**Register Online**

- [Nano.to](https://nano.to)

**Or via RPC**

```bash
curl -d '{
  "action": "get_name",
  "name": "NanoBull"
}' \
-H "Content-Type: application/json" \
"https://rpc.nano.to"
```

![line](https://github.com/fwd/n2/raw/master/.github/line.png)

## Simple Usage

**Name:**
```python
https://nano.to/Fosse
```

**Raw Address:**
```python
https://nano.to/:ADDRESS
```

![line](https://github.com/fwd/n2/raw/master/.github/line.png)

## Single Panel

```python
https://nano.to/Fosse?amount=50
```

<img src="https://github.com/fwd/nano/raw/master/dist/images/single-ui.png" alt="Single Panel UI" />

![line](https://github.com/fwd/n2/raw/master/.github/line.png)

## Double Panel

```bash
https://nano.to/Moon?plans=Tip:0.133,Small:1,Medium:10,Large:20,Gigantic:100
```

<img src="https://github.com/fwd/nano/raw/master/dist/images/double-ui.png" alt="Single Panel UI" />

![line](https://github.com/fwd/n2/raw/master/.github/line.png)

## Customize Colors

```bash
https://nano.to/Moon
?background=$0057b7:$ffd700
&color=$FFF:$000
&highlight=white
&vanity=$0057b7
&qrcode=white:$0057b7
&logo=https://nano.to/dist/logo/cyber.png
```

![line](https://github.com/fwd/n2/raw/master/.github/line.png)

## Available Options

- ```title``` (string) : Replace checkout title.
- ```amount```, **p** (number) : Single panel, No plans.
- ```body``` (string) : Custom checkout text body.
- ```plans``` (string) : Plans separated by commas. Ex. Tip:30,Small:5
- ```goal``` (string) : Show a funding meter based off balance.
- ```image``` (image/url) : Display Image. Image URL.
- ```color``` (string) : Text color. Ex red:blue
- ```background``` (string) : Background color. Ex white:gray
- ```highlight``` (string) : Box backgrounds value. Ex blue:red
- ```qrcode``` (string) : Replace QR Code color. Ex white:black
- ```active``` (string) : Background color of active plan.
- ```logo``` (image/url) : Replace QR Code logo. Image URL.
- ```cancel``` (string) : Redirect URL when pressed 'Cancel'
- ```redirect``` (string) : Redirect URL on success.
- ```currency```, **c** (string) : ISO Currency Symbol. Ex JPY
- ```notify```, (string) : Email(s) or Discord Webhook URL

![line](https://github.com/fwd/n2/raw/master/.github/line.png)

## Funding UI

Easily show a meter of progress for any Nano fundraiser. 

```python
https://nano.to/@Basedlemahieu?goal=100:Funding Goal
```

<img src="https://github.com/fwd/nano/raw/master/dist/images/funding.png" alt="Single Panel UI" />

![line](https://github.com/fwd/n2/raw/master/.github/line.png)

## Update Name

You can update your data anytime. 

```python
https://nano.to/:USERNAME/update
```

> Only original address may update. You can pre-configure URL params in the metadata field of update UI.

## Renew Name

You can extend registration anytime. 

```python
https://nano.to/:USERNAME/renew
```

> Only original address may add time.

![line](https://github.com/fwd/n2/raw/master/.github/line.png)

## Grace Periods

Usernames have **10 day** after expiration, regardless of duration leased. Only the original address may renew.

![line](https://github.com/fwd/n2/raw/master/.github/line.png)

## Checkout API

If you'd like receive notifications and private webhooks, try the [Checkout API](/checkout)

## Reseller API

See our [Developer Page](/developer) for docs on reselling Nano.to Names.

## Usage License

**Limited Commercial**

- ✅ Personal & Open Source
- ✅ Commercial use where Nano.to Usernames / Checkout is a means.
- ❌ Commercial use where Nano.to Usernames / Checkout is re-sold.

Contact [support@nano.to](mailto:support@nano.to) for questions.

![line](https://github.com/fwd/n2/raw/master/.github/line.png)

## Nano.to Support

- Email: support@nano.to
- Twitter: [@nano2dev](https://twitter.com/nano2dev)
- @nano2dev on [Nano's Discord](https://discord.com/invite/RNAE2R9) 