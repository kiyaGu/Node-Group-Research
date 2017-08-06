
#**Performance**: Request lifecycle (from browser to server and back), Performance considerations and optimisations

##Important concepts:
* HTML [Hypertext Markup Language] : the most common language that web pages are written in.
* HTTP [Hypertext Transfer Protocol] : a common protocol to pass around HTML amongst other forms of data (JSON and Form data is also common).
    *It oversees the data exchange between a client & the server.
        *It is stateless, i.e. - treats each request as an independent transactions, unrelated to any previous requests. Thus, communication involves of independent pairs of requests & responses.
##Step by step walk through HTTP Request/Response Handling:
Step 1: Parsing the URL
* A URL is typed into the address bar of a web browser.
* The browser checks for the IP in its browser cache. If not found, it send a request to DNS.
* The browser parses the URL to find: 
    * the protocol type, 
    * the host, 
    * the port, and 
    * the request-URI path.
        * "[protocol]://[host]/[request-URI]"\


# Reference: 
1. http://celineotter.azurewebsites.net/world-wide-web-http-request-response-cycle/
