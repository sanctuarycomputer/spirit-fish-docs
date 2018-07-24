---
permalink: quickstart
category: Getting started
---

# Quickstart

Know your way around CDNs and static deployments? Follow the high level instructions
and Spirit Fish will be up in no time.

## Up & Running

[warn]
This guide assumes you've deployed your static assets to an origin like S3,
and you've got a CDN in place that can route requests to different origins
based on the request headers.
[/warn]

1. Setup a Spirit Fish renderer to point to your CDN
2. Route HTML requests with the `X-SPIRIT-FISH` header to your Asset Host Origin
3. Route all other HTML requests to your Spirit Fish renderer

For example, you may use the following [Origin Request Lambda@Edge](https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/lambda-examples.html#lambda-examples-content-based-routing-examples) function to do just this:

```js
const path = require('path');

const spiritFish = ({ rendererURI, event, ssl }) => {
    const request = event.Records[0].cf.request;

    const notFromSpiritFish =
        !request.headers['x-spirit-fish'];
    const consideredHTMLRequest =
        ['.html', '.htm', ''].includes(path.extname(request.uri.split('/').pop()));

    if (consideredHTMLRequest && notFromSpiritFish) {
        request.origin = {
            custom: {
                customHeaders: {},
                domainName: rendererURI,
                keepaliveTimeout: 5,
                path: '',
                port: (ssl ? 443 : 80),
                protocol: (ssl ? 'https' : 'http'),
                readTimeout: 30,
                sslProtocols: [ 'TLSv1', 'TLSv1.1', 'TLSv1.2' ]
            }
        };
        request.headers.host = (request.headers.host || [{key: 'Host', value: ''}]);
        request.headers.host[0].value = rendererURI;
    }

    return request;
};

exports.handler = async (event) => {
    return spiritFish({
        rendererURI: "{YOUR RENDERER URI HERE}",
        ssl: true,
        event: event
    });
};
```

[warn]
If you're using Lambda@Edge, you'll need to Whitelist the custom header `X-SPIRIT-FISH`.
[/warn]
