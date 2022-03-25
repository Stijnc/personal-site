---
draft: false
title: "Azure Static Web App URL shortener"
date: 2022-01-31T14:12:33+01:00
cover: 
      image: images/cut-grass.jpeg
      caption: Photo by <a href="https://unsplash.com/@bruno_kelzer">Bruno Kelzer</a>
      alt: cut grass
ShowToc: true
TocOpen: false
---

## TL;DR

Azure static web apss routing feature can be used as a quick URL shortener service.

## stijn.run, my personal URL shortener

I was on the look-out for a URL shortener with a custom domain for the smallest fee possible and stumbled upon [Netifly-URLShortener](https://github.com/kentcdodds/netlify-shortener).  

I find this a elegant solution through its simplicity, but at the same time, I wanted to experiment a bit with [Azure Static Web App](https://azure.microsoft.com/en-us/services/app-service/static/) as well.

[Azure Static Web App](https://azure.microsoft.com/en-us/services/app-service/static/) has a similar feature build in, using ` routes`.

### staticwebapp.config for all your configuration

[Azure Static Web App](https://azure.microsoft.com/en-us/services/app-service/static/) configuration file `staticwebapp.config.json` includes a routes section you can use to redirect a route to another URL.

All you need to do is add a link by modifying ```staticwebapp.config.json``` where ```route``` is the ```shorturl``` and ```redirect``` contains the ```destination```.

{{< gist stijnc 2b356b6591850f9dc5132d3a4853d65e  "00-routes.json" >}}


### Use aswa-shortener

Instead of manually updating your ``` staticwebapp.config.json ``` file, you could also use the aswa-shortener npm package.
Aswa (Azure Static Web App) shortener automatically generates a short code and checks if your route already exists. It will also push your changes to your origin, triggering a build of your Azure Static Web App.

> Note: It takes a minute or to for the build to complete, so your shortcode is not available in real-time.

#### Installation

This module is distributed via [npm][npm] which is bundled with [node][node] and
should be installed as one of your project's `dependencies`:

```sh

npm install --save asweb-shortener

```

#### Usage

Your project should have a `staticwebapp.config.json` file that looks like this:

```json
// example
{
  "routes": [
    {
      "route": "/me",
      "redirect": "https://callebaut.io",
      "statusCode": "301"
    }
  ],
  "navigationFallback": {
    "rewrite": "index.html",
    "exclude": ["/images/*.{png,jpg,gif}", "/css/*"]
  },
  "responseOverrides": {},
  "globalHeaders": {
    "content-security-policy": "default-src https: 'unsafe-eval' 'unsafe-inline'; object-src 'none'"
  }
}
```

This module exposes a binary that you should use in your `package.json` scripts.
You also need to add

- a `homepage` to your `package.json`
- a config setion to specify your appLocation (defaults to src)

```json

{
  "homepage": "https://stijn.run",
  "config": {
    "appLocation": "src"
  },
  "scripts": {
    "shorten": "asweb-shortener"
  }
}

```

Then you can run:

```sh

npm run shorten # simply formats your _redirects file
npm run shorten https://yahoo.com # generates a short code and adds it for you
npm run shorten https://github.com gh # adds gh as a short URL for you

```

The `asweb-shortener` does a few things:

1. generates a short code if one is not provided
2. validates your URL is a real URL
3. adds the URL to the `routes` section of `_redirects`
4. runs a git commit and push (this will trigger your Azure Static Web App CI/CD
   to deploy your new redirect)
5. Copies the short URL to your clipboard

This introduces some delay as the rebuild needs to be pushed.



#### Shell Function

If you want to be able to run this anywhere in the terminal, you can try making
a custom function for your shell.

##### Shell Agnostic

1. Add the following [executable definition][npm-bin] to your `package.json`:
   ```json

   {"bin": {"shorten": "cli.js"}}

   ```
2. Create the `cli.js` file:
   ```js

   #!/usr/bin/env node
   require('asweb-shortener')

   ```
3. From your project directory, run the following to register the command
   globally:
   ```sh

   npm link

   ```
