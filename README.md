<a href="https://dub.sh">
  <img alt="Dub – an open-source link shortener SaaS with built-in analytics + free custom domains." src="/public/_static/thumbnail.png">
  <h1 align="center">Dub</h1>
</a>

<p align="center">
  An open-source link shortener SaaS with built-in analytics + free custom domains.
</p>

<p align="center">
  <a href="https://twitter.com/dubdotsh">
    <img src="https://img.shields.io/twitter/follow/dubdotsh?style=flat&label=%40dubdotsh&logo=twitter&color=0bf&logoColor=fff" alt="Twitter" />
  </a>
  <a href="https://news.ycombinator.com/item?id=32939407"><img src="https://img.shields.io/badge/Hacker%20News-255-%23FF6600" alt="Hacker News"></a>
  <a href="https://github.com/steven-tey/dub/blob/main/LICENSE">
    <img src="https://img.shields.io/github/license/steven-tey/dub?label=license&logo=github&color=f80&logoColor=fff" alt="License" />
  </a>
</p>

<p align="center">
  <a href="#introduction"><strong>Introduction</strong></a> ·
  <a href="#deploy-your-own"><strong>Deploy Your Own</strong></a> ·
  <a href="#tech-stack"><strong>Tech Stack</strong></a> ·
  <a href="#implementation"><strong>Implementation</strong></a> ·
  <a href="#contributing"><strong>Contributing</strong></a>
</p>
<br/>

## Introduction

Dub is an open-source link shortener with built-in analytics + free custom domains. Built with [Vercel Edge Functions](http://vercel.com/edge), [Upstash Redis](https://docs.upstash.com/redis), and [Planetscale MySQL](https://planetscale.com/).

Here are some of the features that Dub provides out-of-the-box:

### Built-in Analytics

Dub provides a powerful analytics dashboard for your links, including geolocation, device, and browser information.

![Analytics Dashboard](/public/_static/landing/analytics.png)

### Custom domains

You can easily configure custom domains on Dub – just add an A/CNAME record to your DNS provider and you're good to go. This is built on the [Vercel Domains API](https://domains-api.vercel.app/).

![Custom Domains](/public/_static/landing/domains.png)

### QR Code Generator

You can easily generate and customize QR codes for your links, which can be used for flyers, posters, powerpoint presentations, etc.

![QR Code](/public/_static/landing/qr.png)

### OG Image Proxy

Add a custom OG image in front of your target URL. Bots like Twitter/Facebook will be served this image, while users will be redirected to your target URL.

![OG Image Proxy](/public/_static/landing/og-image-proxy.gif)

## Deploy Your Own

You can deploy your own hosted version of Dub for greater privacy & control. Just click the link below to deploy a ready-to-go version of Dub to Vercel.

[![Deploy with Vercel](https://vercel.com/button)](https://dub.sh/deploy)

## Tech Stack

- [Next.js](https://nextjs.org/) – framework
- [Typescript](https://www.typescriptlang.org/) – language
- [Tailwind](https://tailwindcss.com/) – CSS
- [Upstash](https://upstash.com/) – redis
- [Planetscale](https://planetscale.com/) – database
- [NextAuth.js](https://next-auth.js.org/) – auth
- [Vercel](https://vercel.com/) – hosting
- [Stripe](https://stripe.com/) – payments

## Implementation

Dub is built as a standard Next.js application with [Middleware](https://nextjs.org/docs/advanced-features/middleware) to handle multi-tenancy, inspired by [the Vercel Platforms Starter Kit](https://github.com/vercel/platforms).

[Redis](https://redis.io/) is used as the caching layer for all short links. Redis also has the Sorted Set data type, which is perfect for storing & retrieving time-series analytics data. Here's the full schema:

- `{domain}:{key}` – string containing a JSON object with the target URL and password (optional). Also has an optional TTL.
- `{domain}:clicks:{key}` – sorted set of all clicks for a given link (e.g. `dub.sh:clicks:github`)
- `{domain}:root:clicks` – sorted set of all root link clicks for a given domain (e.g. `dub.sh:root:clicks`)

[MySQL](https://www.mysql.com/) is used as the database for storing user data, project data, and link metadata. You can refer to the Prisma schema [here](/prisma/schema.prisma).

## Contributing

We love our contributors! Here's how you can contribute:

- [Open an issue](https://github.com/steven-tey/dub/issues) if you believe you've encountered a bug.
- Make a [pull request](https://github.com/steven-tey/dub/pull) to add new features/make quality-of-life improvements/fix bugs.

<a href="https://github.com/steven-tey/dub/graphs/contributors">
  <img src="https://contrib.rocks/image?repo=steven-tey/dub" />
</a>

## Author

- Steven Tey ([@steventey](https://twitter.com/steventey))

## License

Inspired by [Plausible](https://plausible.io/), Dub is open-source under the GNU Affero General Public License Version 3 (AGPLv3) or any later version. You can [find it here](https://github.com/steven-tey/dub/blob/main/LICENSE.md).
