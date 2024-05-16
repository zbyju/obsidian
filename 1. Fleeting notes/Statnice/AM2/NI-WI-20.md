**Mashup aplikace, pravidla same-origin policy. Protokoly CORS, JSONP, JWT.**

# Mashup application
Applications that combine data from multiple sources/APIs:
- Data Mashup - data integration/aggregation only (read only)
- Service Mashup - More sophisticated (read, write)
- Visualization - involes UI more

- Client-side mashup (in browser)
- Server-side mashup - server side integration

# Same Origin Policy
Browser can make requests only on the same domain (host, port)

There are 2 solution for this problem.

This is to prevent attacks:
- XSS (Cross-site scripting) attacks - injecting javascript to a website and then running a script utilizing the cookies and sessions the user has stored.
- CSRF (Cross-Site Request) attacks - injecting content to a website, when it loads it sends requests to another website to retrieve data
# CORS
![[Pasted image 20240516163718.png]]
# JSONP
# JWT
