---
permalink: cdn
category: Getting started
---

# What is a CDN?

CDN stands for Content Delivery Network. Almost all serious web applictions use
a CDN to speed up the delivery of their content (be it HTML, CSS, JS, images or JSON)
by caching it in cloud, and serving from that cache rather than asking the application
or asset server for a response.

## Why do I need a CDN with Spirit Fish?

Spirit Fish is a service that will run your application on the cloud, wait until the
network becomes idle, run your javascript, perfrom some transforms, and then send the
resulting HTML back. Because it's doing so much, it's too slow to actually serve your
users head-on. In some cases, it can take 3 - 5 seconds to render a page (depending
on how many resources it needs).

By using a CDN, and configuring it to pull and cache HTML from Spirit Fish, you're
getting the best of both worlds: a blazing fast HTML pages that have dynamic content
renderered.

[warn]
Spirit Fish is too slow to serve traffic head-on.
[/warn]

## How do I deploy my app to a CDN?

Technically, you don't "deploy" to a CDN - you instead deploy to an asset store, like
AWS S3, Google Cloud Storage, Digital Ocean Volumes, etc. Your CDN recieves traffic,
and forwards that traffic to your asset store (if necessary).

Head over to our [deployment section](/docs/master/deployment) for more info.

## OK, so which CDN should I use?

Put simply - we recommend [AWS Cloudfront](https://aws.amazon.com/cloudfront/). That's
what we use for all of our clients in house at [Sanctuary Computer](http://sanctuary.computer),
mostly because we deploy our static website assets to [AWS S3](https://aws.amazon.com/s3/), and
the two play nicely together.

That said, Spirit Fish works with most CDNs. Check out our guides for:
- [AWS Cloudfront](https://aws.amazon.com/s3/)
- [Fastly](https://www.fastly.com/)
- [Cloudflare](https://www.cloudflare.com/)
- [Google Cloud CDN](https://cloud.google.com/cdn/docs/)

You can also "roll your own" with something like [Redis, Memchached, etc]().

[tip]
Spirit Fish works with pretty much anything!
[/tip]

## Breaking the Cache

If the content of your website changes, or you deploy new changes, you'll want to clear
(or invalidate) your CDN cache, so that your CDN will ask Spirit Fish to re-render those
pages.

Right now, this is an excersize left to the developer. Check the Spirit Fish guide for your
CDN for more info.

[warn]
It's up to you to decide when and how to implement behavior that will break the cached HTML in your CDN. If you never break the cache, your CDN will keep serving the same HTML, even if the content changes.
[/warn]
