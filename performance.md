# What is an apdex score?

Apdex is a measure of response time based against a set threshold. It measures the ratio of satisfactory response times to unsatisfactory response times. The response time is measured from an asset request to completed delivery back to the requestor.

After you define a response time threshold T, all responses handled in T or less time satisfy the user.

# Client side rendering speed optimizations
  ## Bundling
    HTTP2
    multiplexing
    bundle splitting
    Inline critical scripts
    defer some scripts so they don't block first load
    
    https://www.infoq.com/articles/reduce-react-load-time/
    Setting up code splitting with SplitChunksPlugin was a breeze. It took a few iterations to get the number of chunks correct. Our initial bundle size for the entire applications was ~7MB. After code splitting, the initial bundles that load had a combined size of 230kb, a whopping 97% reduction in application bundle size!

  ## Compression
  gzip
  brottle

  ## Pagination
  cursor pagination
  offset pagination

# Fetching new data
Long polling
Websockets
SSE (Server side events)

# Image Optimization
optimized pngs, not to high res
svg icons
icon fonts

# JS performance
Caching
Reduce http requests

# CSS Naming strategy
Can effect performance (?)

# UI
Lazy load images
Spinners/placeholders

# GraphQL
https://blog.logrocket.com/graphql-vs-rest-what-you-didnt-know/
In GraphQL applications, client requests are all HTTP POST requests and completely bypass the standard HTTP caching mechanism. Because of this, GraphQL client applications tend to use a GraphQL client library like Apollo or Relay. These libraries provide a caching mechanism for queried data, which relies on globally unique IDs for queried object types (more info on GraphQL caching here).

# Service workers/PWA mode

# Good load times
https://www.pingdom.com/blog/website-load-time-in-2020/
Although website load time depends on various factors such as the hosting server, amount of bandwidth in transit, webpage design, page elements, browser, and device type, an ideal website load time should be no more than *2 seconds*. The probability of bounce rate increases by 32% if the page load time increases from 1 to 3 seconds.
JavaScript Issues
Unoptimized Image Content
Multiple HTTP Requests
Ignoring Caching Techniques
Unclean Code
Not Using Compression (GZIP)

https://www.machmetrics.com/speed-blog/average-page-load-times-for-2020/
Google’s best practice is to have a speed index under 3 seconds.

https://blog.newrelic.com/technology/pageloads-single-page-apps/
Understanding the “true” customer experience of your page load
Between dynamic content and SPAs, the gap between the window.load event and when a user can actually use the page becomes increasingly significant. A page may take only 200 ms for the onload event to fire, but by the time all the AJAX calls have finished and the DOM has settled, it may be 1000 ms (or even double that) before the page is fully rendered and usable. This later time is a more accurate representation of the customer experience.

And this is just a simplified example. Many modern web experiences employ several of these design use cases at once, which can further slow the “true” customer experience of the page. For companies that care about their digital customer experience, getting a true view of the customer experience of a page load can be an enlightening experience, uncovering how long it really takes for a user to start engaging with web content, not to mention the impact this can have on key metrics like conversions, engagement, and digital revenue.
