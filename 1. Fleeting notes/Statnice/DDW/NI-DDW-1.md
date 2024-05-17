**Struktura a vazby na webu: principy procházení a získávání obsahu webu, grafové reprezentace - charakteristiky a využití, metriky centralit, PageRank, detekce komunit, predikce linků, afiliační sítě.**

# Crawlers
Crawlers are used to get data from the web in an automated way.
- Batch crawler - create snapshot of some web space
- Incremental crawler - continuously crawl web space, revisit to refresh data
- Focused/Topical crawler - crawl specific websites, topics

## Terminology
- Seed pages - initial pages to crawl from
- Frontier/Queue - list of unvisited URLs
- Fetcher - gets the data of a URL
- Link extractor - parses the HTML to get the links
- URL filter - check if URL is blacklisted
- Duplicate eliminator - eliminates already visited URLs
- URL prioritiser - assigns priority to URLs and sorts them by it
## Algorithms for crawling
### Breadth-first crawl
Visit pages in the order in which they are seen
It's highly correlated with their popularity, bias to index well connected sites.
### Backlink based crawl
Sort the URLs in the queue based on t