# Paste Bin

# 1. Requirements
    Functional Requirements
        save the content (Max 10 MB) [Only Text]
        Generate unique URL and support Custom-URL
        Expiry after Default time (Support to extend expiry time)
    Non-Functional Requirements
        Durable [ Persisited]
        Available
        Low Latency

# 2. Capacity Estimations
    Traffic 10:1 (Read:Write)
        expected Writes 100K  Per day 
                        [Estimate per Second]  (Average and Peek hour - 30%)
                 Reads  1000k Per day 
                        [Estimate per Second]   (Average and Peek hour - 30%)
    Paste Storage
        Worst   100k * 10MB = 1000GB = 1.0 TB [365 * 5  ] []
        Average 100k * 2B   =  200GB = 0.2 TB [365 * .2 ] []

        Metadata 100k * 1kB

# References
[Narendra](https://www.youtube.com/watch?v=josjRSBqEBI)