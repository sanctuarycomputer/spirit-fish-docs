---
permalink: about
category: Getting started
---

# What is Spirit Fish?

Spirit Fish is a Cloud Hosted Serverside Renderer for your Single Page Applications. Put simply,
when a request hits Spirit Fish, we spin up your website in a Chrome Browser, and render the page.
We'll then wait until your page is ready (just like your users would), and snapshot the HTML to
send back to you.

## Why would I use this?

[warn]
Web Crawlers can't read Metatags that are populated with Javascript, and Initial Paints are slow in
Single Page Apps.
[/warn]

### SEO & Web Crawlers

When you make a single page app (with React, Ember, or friends), your website isn't active until it
has downloaded it's Javascript bundle, and had that JS start up.

However! Most Web Crawlers don't run the Javascript at all. That means if you're using something like
[react-helmet](https://google.com) to populate Metatags (like your facebook share cards or SEO data),
webcrawlers *probably* can't see them.

TODO: Unfurls Image

### Page Speed & Initial Paint

Because your single page app needs it's Javascript before it can show any content, you'll need to wait
until both your HTML *and* Javascript is present before users can see anything.

TODO: Page Speed Image

### No Servers Required

Most Serverside Rendering solutions out there require you to run a server that is in the request path,
to render your application on demand. This usually involves something like
[React Universal Component](https://github.com/faceyspacey/react-universal-component) or
[Ember Fastboot](https://www.ember-fastboot.com/). This means you're in charge of serverside deployment,
scaling, uptime, server upgrades, and all of the sysadmin that comes along with running an app in the cloud.

Instead, Spirit Fish handles all of that for you, allowing you to simply host static assets, while having
serving your users a fully renderered site.

### Caching Requests

If you're using a single page app framework, it's likely your app needs to make some web requests to
boot up. If those requests are always the same for all users, why not cache them with Spirit Fish?

A good example might be if you're using [Contentful](https://google.com). Contentful charges based on
requests, so if every page visit is requesting homepage content, and it's the same for every user,
why not cache that request in the HTML?

## But does it work with my JS Framework?

[tip]
If it works in Chrome, it works in Spirit Fish.
[/tip]

Because Spirit Fish renders your app or website in Chrome, it works with *any* framework - be it
React, Ember, Angular, Vue - the list goes on. It even works with your own hand spun, bespoke
framework, too.

TODO: Framework images

## So how do I use it?

[warn]
Spirit Fish requires some type of caching mechanism - it can not traffic directly.
[/warn]

Spirit Fish operates as an origin for your CDN or caching layer. Spirit Fish is loading all
of your assets, performing optimizations and transforms and waiting until Network Idle, **it
is too slow to serve all of your traffic**.

Instead, Spirit Fish is designed with [CDN]() use-cases in mind.

[Take a look at our Deployment section for more info]().
