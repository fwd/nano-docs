# Welcome to NANO

Nano.to is a general purpose API for the NANO blockchain. Use this API to check USD price, create hosted payment links (like Stripe Checkout) for your NANO address and more. Accessible from any internet connected device with a modern web browser.

Launched **September 15th, 2021**. Platform is in Beta, but stable. 

**Anonymous, no account or API key required to use.**

**Note: We did not build or own NANO. We simply built a service on top of it.**

## Quick Start

Let's say you have following files in `./my-docs` folder:

```bash
https://nano.to/[NANO_ADDRESS_OR_USERNAME]
```

The `index.html` looks like:

```html {highlight:[7,'10-16']}
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1, shrink-to-fit=no">
    <title>My Docs</title>
    <link rel="stylesheet" href="https://unpkg.com/docute@4/dist/docute.css">
  </head>
  <body>
    <div id="docute"></div>
    <script src="https://unpkg.com/docute@4/dist/docute.js"></script>
    <script>
      new Docute({
        target: '#docute'
      })
    </script>
  </body>
</html>
```

Then you can serve this folder as a static website on your machine using:

- Node.js: `npm i -g serve && serve .`
- Python: `python -m SimpleHTTPServer`
- Golang: `caddy`
- ..or whatever static web server

Next, you may want to use [sidebar](./options.md#sidebar), [nav](./options.md#nav) or other [options](./options.md) to customize the website.

Here's a [REPL](https://repl.it/@egoist/docute-starter) where you can try Docute online or [download](https://repl.it/@egoist/docute-starter.zip) it to run locally.

## Comparisons

### VuePress / GitBook / Hexo

They all generate static HTML at build time, which is good for SEO.

If you care about SEO, you may like using [presite](https://github.com/egoist/presite) to prerender your website.

### Docsify

[Docsify](https://docsify.js.org/#/) and Docute are pretty much the same, but with different UI and different usages.

Docute (60kB) is 3 times bigger than Docisfy (20kB), because we use Vue, Vue Router and Vuex while Docsify uses vanilla JavaScript under the hood.

## Browser Compatibility

Docute supports all ever-green browsers, i.e. No IE support!
