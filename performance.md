
# Performance: 
**: _Request lifecycle (from browser to server and back), Performance considerations and optimisations_**
By: 
    - Raymond
    - Kiya


## Important concepts:
* **HTML _[Hypertext Markup Language]_** : the most common language that web pages are written in.
* **HTTP _[Hypertext Transfer Protocol]_** : a common protocol to pass around HTML amongst other forms of data (JSON and Form data is also common).
    * It oversees the data exchange between a client & the server.
        * It is stateless, i.e. - treats each request as an independent transactions, unrelated to any previous requests. Thus, communication involves of independent pairs of requests & responses.
## Step by step walk through HTTP Request/Response Handling:
**Step 1**: Parsing the URL
* A URL is typed into the address bar of a web browser.
* The browser checks for the IP in its browser cache. If not found, it send a request to DNS.
* The browser parses the URL to find: 
    * the protocol type, 
    * the host, 
    * the port, and 
    * the request-URI path.
        * "[protocol]://[host]/[request-URI]"
**Step 2**: Sending the request
* A socket connection is opened from our user’s computer to the IP address.
* HTTP request is sent to the host & the machine waits to get a response back.
* Web server receives the request.

**Step 3**: The server response
* For static requests:
    * The server locates the html filename & sends that file back over the internet.
* For dynamic requests:
    * .php, .asp, .aspx, .jsp files, are processed by a separate engine. These will be partially complete, containing changeable
       sections depending on variable values given to the page on the server end. The dynamic data & the requested file will be 
       combined into a long string of text ( HTML, txt, XML) before its output is sent back over the internet.
* If successful, the server returns a 200 status code (as the resource was found), response headers, and the requested data back to the browser.
* If the server fails to process or complete the request, it returns an 404 error message instead.

**Step 4**: Browser rendering:
* The browser receives the response with a html document to parse into a DOM [Document Object Model]. For this, it translates html
elements & attributes into nodes with the "Document Object" set as the root of the tree.
* When external script, image, style sheets are parsed, new requests are made to the server.
* When stylesheets are parsed, each applicable styles gets attached to the matching node in the DOM tree.
* Javascript files are parsed & executed.
    * DOM nodes are updated.
* The browser renders the page. The page is viewable & interact-able.

**Step 5**: HTTP persistent connection
* 'Connection: Keep-Alive' header.
    * This initiates a single TCP [Transmission Control Protocol] connection for sending & receiving multiple HTTP requests / responses, instead of opening a new connection for every single request / response pair.
    * It is set from the initial browser request header, and informs the server to not drop this connection. When the client 
       sends another request, it uses the same connection. This will continue until either the client or the server decides to drop the
       connection.

## Performance considerations and optimisation

### 1. Using caches
    * What’s a Web Cache? Why do people use them?
        * A Web cache sits between one or more Web servers (also known as origin servers) and a client or many clients, and watches requests come by, saving copies of the responses — like HTML pages, images and files (collectively known as representations) — for itself. Then, if there is another request for the same URL, it can use the response that it has, instead of asking the origin server for it again.
    * There are two main reasons that Web caches are used:
        * To reduce latency — Because the request is satisfied from the cache (which is closer to the client) instead of the origin server, it takes less time for it to get the representation and display it. This makes the Web seem more responsive.
        * To reduce network traffic — Because representations are reused, it reduces the amount of bandwidth used by a client. This saves money if the client is paying for traffic, and keeps their bandwidth requirements lower and more manageable.

**Kinds of _Web Caches_**
    1. Browser Caches
        * If you examine the preferences dialog of any modern Web browser (like Internet Explorer, Safari or Mozilla), you’ll probably
          notice a “cache” setting. This lets you set aside a section of your computer’s hard disk to store representations that you’ve
          seen, just for you. The browser cache works according to fairly simple rules. It will check to make sure that the 
          representations are fresh, usually once a session (that is, the once in the current invocation of the browser).

         This cache is especially useful when users hit the “back” button or click a link to see a page they’ve just looked at. Also, 
         if you use the same navigation images throughout your site, they’ll be served from browsers’ caches almost instantaneously.

    2. Proxy Caches
        * Web proxy caches work on the same principle, but a much larger scale. Proxies serve hundreds or thousands of users in the 
          same way; large corporations and ISPs often set them up on their firewalls, or as standalone devices (also known as
          intermediaries).

          Because proxy caches aren’t part of the client or the origin server, but instead are out on the network, requests have to 
          be routed to them somehow. One way to do this is to use your browser’s proxy setting to manually tell it what proxy to use;
          another is using interception. Interception proxies have Web requests redirected to them by the underlying network itself, 
          so that clients don’t need to be configured for them, or even know about them.

          Proxy caches are a type of shared cache; rather than just having one person using them, they usually have a large number 
          of users, and because of this they are very good at reducing latency and network traffic. That’s because 
          popular representations are reused a number of times.

    3. Gateway Caches
        * Also known as “reverse proxy caches” or “surrogate caches,” gateway caches are also intermediaries, but instead of being 
          deployed by network administrators to save bandwidth, they’re typically deployed by Webmasters themselves, to make their sites
          more scalable, reliable and better performing.
        * Requests can be routed to gateway caches by a number of methods, but typically some form of load balancer is used to make one 
          or more of them look like the origin server to clients.
        * Content delivery networks (CDNs) distribute gateway caches throughout the Internet (or a part of it) and sell caching to
          interested Web sites. Speedera and Akamai are examples of CDNs.

### 2. Reduce HTTP Requests
    When your browser fetches data from a server it does so using HTTP (Hypertext Transfer Protocol). It is a request/response 
    between a client and a host. In general the more HTTP requests your web page makes the slower it will load.

    There are many ways you can reduce the number of requests such as:
        * Inline your Javascript (only if it is very small)
        * Using CSS Sprites
        * Reducing assets such as 3rd party plugins that make a large number of external requests
        * Don’t use 3rd party frameworks unless they are absolutely needed
        * Use less code!

### 3. Minify CSS and Javascript
    * Minification of resources means removing unnecessary characters from your HTML, Javascript, and CSS that are not required to load, such as:
        * White space characters
        * New line characters
        * Comments
        * Block delimiters

    This speeds up your load times as it reduces the amount of code that has to be requested from the server.

    * CSS
        * Properly call your CSS files
        * Use media queries to mark some CSS resources as non-render blocking
        * Lessen the amount of CSS files (concatenate your CSS files into one file)
        * Minify Your CSS (remove extra spaces, characters, comments, etc)
        * Use less CSS overall
    * Javascript
      When it comes to Javascript there are some best practices to always keep in mind.
        * Move your scripts to the bottom of the page right before your </body> tag.
        * Use the async or defer directive to avoid render blocking.
        * Concatenate your JS files into one file (with HTTP/2 this is no longer as important)
        * Minify your Javascript (remove extra spaces, characters, etc)
        * Inline your javascript if it is small

### 4. Avoid 301 Redirects
    * _Redirects are performance killers_. Avoid them whenever possible. A redirect will generate additional round trip times (RTT) and therefore quickly doubles the time that is required to load the initial HTML document before the browser even starts to load other assets.
### 5. Prefetch and Preconnect
    * Domain name prefetching is a good solution to already resolve domain names before a user actually follows a link. Here an 
      example how to implement it in the HEAD section of your HTML:
        `<link rel="dns-prefetch" href="//www.example.com">`
    * Preconnect allows the browser to set up early connections before an HTTP request is actually sent to the server. Connections 
      such as DNS Lookup, TCP Handshake, and TLS negotiation can be initiated beforehand, eliminating roundtrip latency for 
      those connections and saving time for users.

      The example below shows what it looks like to enable preconnect for the zone alias link for KeyCDN.
        `<link href='https://cdn.keycdn.com' rel='preconnect' crossorigin>`
### 6. HTTP/2
### 7. Enable Gzip Compression
    * Gzip is another form of compression which compresses web pages, CSS, and javascript at the server level before sending them over
      to the browser. 


# Reference: 
1. http://celineotter.azurewebsites.net/world-wide-web-http-request-response-cycle/
2. https://www.keycdn.com/blog/website-performance-optimization/
