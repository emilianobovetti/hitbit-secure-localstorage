There are many<sup>[[1]](https://stackoverflow.com/a/44209185/3281770)</sup><sup>[[2]](https://auth0.com/docs/security/store-tokens)</sup><sup>[[3]](https://dev.to/rdegges/please-stop-using-local-storage-1i04)</sup><sup>[[4]](https://medium.com/hackernoon/all-you-need-to-know-about-user-session-security-ee5245e6bdad)</sup><sup>[[5]](https://stormpath.com/blog/where-to-store-your-jwts-cookies-vs-html5-web-storage)</sup> people on internet that think a [JWT](https://jwt.io) shouldn't be stored inside [localStorage](https://developer.mozilla.org/en-US/docs/Web/API/Window/localStorage).

In [SPA](https://en.wikipedia.org/wiki/Single-page_application)s, unfortunately, it may not be possible to use [HttpOnly](https://www.owasp.org/index.php/HttpOnly) cookies.

Here I use an `iframe` and [window.postMessage()](https://developer.mozilla.org/en-US/docs/Web/API/Window/postMessage) cross-origin communication to securely store the token and handle user login.

[Here](https://github.com/hitbit-app/backend/blob/master/priv/html/session-container.eex) you can find the code running inside the iframe.

This approach seems to expose less data in a possible [XSS](https://www.owasp.org/index.php/Cross-site_Scripting_(XSS)) attack: code that runs outside the iframe shouldn't have access to user credentials, shouldn't be able to use key loggers or stole the token. Anyway, due to the hacky implementation, it might not be a good idea to use in production.

Live demo: https://hitbit-secure-localstorage.netlify.com

*Please note that this is experimental work.*
