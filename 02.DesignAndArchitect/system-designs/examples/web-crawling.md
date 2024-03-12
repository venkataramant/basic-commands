
# Material

[web-crawling by Narendra](https://www.youtube.com/watch?v=BKZxZwUgL3Y)

[Standford Book](https://nlp.stanford.edu/IR-book/html/htmledition/web-crawling-and-indexes-1.html)

[Priority Queue and Polite](https://nlp.stanford.edu/IR-book/html/htmledition/the-url-frontier-1.html)


# Goals
    Search  Engine
    Detections
        CopyRight Violation 
        Web Malware
    Keyword based finding
    Analytix
        Web Analytix
        DataScience Data
# Topics
    Politeness - Upper limit of visit frequency
    DSN Query
    Distributed Crawling
    Priority Crawling
    Detections
        Duplicate
        Copy Right Content
        Malware
    Server side Rendering
# Function And Non-Requirements
    Scalability
    Extensibility
    Freshness of Pages

    Storage Optimization

# Components
    Seed URLs
    URL Frontier
    Content Fetcher and Render
    Custom DSN Resolver (Not depending upon system DNS resolver)
    Storage (For Compressed data)
    Redis (For quick access, uncompress data)
    Message Queues 
    Detection Plugins (Consumer of MQ)
        Duplication Detector
        URL_Extractor
            Sub-Domain and Domain Mapping
            URL Normalization
    URL Filter
    URL Loader
        Is Crawled (Use Bloom Filter)
        Save in DFS

# URL Frontier
    a) Priority,Recrawl,Freshness
    b) Polite


    Front Queues
        No of Queue = No of Priorities
    Back Queue Router
    Back Queues
         1 Q per Host
         1 Q per Thread
         Not Empty
         Host_Name_QUEUE_ID_MAP_TABLE
    Back Queue Selector
    Heap

# Duplicate Detection Techniques

    BruteForce
    Hashing (MD5/SHA)
    MinHash
    SimHash (Google)
    Fuzzy Search
    Latent Sematic Indexing
    Standard Boolean module

# File Content Storage Options

    BigTable (GFS)
    S3 or Min.IO
    HDFS (64MB)
    HDFS Federation
    GlusterFS
    OrangeFS
    ExtremeFS

# Challenges
    Crawler Traps
    






    


