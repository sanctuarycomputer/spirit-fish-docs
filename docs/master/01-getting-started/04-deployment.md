---
permalink: deployment
category: Getting started
---

# Deployment

There's a multitude of ways to deploy a single page application. Spirit Fish
works great with most of them, but is designed with a specific type of deployment
in mind. Specificially - Spirit Fish works best when you host static assets behind
a CDN.

## Deployment Overview

In order to deploy your Single Page App, you'll do the following:

1. Host your built assets somewhere (Like AWS S3)
2. Put a CDN in front of the asset host (Like AWS Cloudfront)
3. Route uncached requests from your CDN to Spirit Fish
4. Allow requests to your CDN from Spirit Fish to hit your asset host
5. Point your domain at your CDN, and you're live!

[tip]
Important: Your CDN should be setup to recognize a request from Spirit Fish by the `X-SPIRIT-FISH` header, and serve the raw assets for rendering.
[/tip]

## Request Lifecycle

When a request for HTML hits your CDN, the following logic runs:

1. The CDN checks if the request is cached (and returns cached requests instantly)
2. If it is not, it forwards the request to Spirit Fish
3. Spirit Fish recieves the forwarded request, and asks your CDN for the raw assets
4. The CDN knows it is a Spirit Fish request by the `X-SPIRIT-FISH` header, and serves Spirit Fish the raw HTML assets from your asset host.
5. Spirit Fish renderers the page, and returns it to your CDN
6. Your CDN caches the renderered HTML, and serves it to users going forward!

[tip]
Spirit Fish should be the only CDN viewer that sees your un-rendered HTML assets. All other viewers will see a version of your HTML that has been renderered by Spirit Fish.
[/tip]
