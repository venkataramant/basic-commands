# Definition
    More than 1 computer (Processes dont share resources)
    Acting as a cohesive System.
# Evolution of topology
    Single Computer (Single user)
    Multi Client - Single Server
    Multi Client - N tier Server setup
                 - MicroServices (Service oriented Architecture)
    Peer to Peer (Client becomes Node)


# DS Deployment topology
    Scalability as per user-base/needs of business
    Distribute GeoGraphy
    Latency
    High Availability (Tolerant to hardware failures)
    Regulations

# Complexities in Distributed System
        Consesus
        Logging and Monitoring
            Track everything unieuq UID
        Security
            end points to protect
        State
            Idempotency
            Stateless
# Data Layer Distribution
    Sharding - Decrease Latency
    Replication - Availability [ set of nodes have same/or about same copy]


# MS Application  Architecture
    Independent components
        development (rate of change)
        testing
        run time (Scaling)
    Isolated dependencies
    Circuit Breaker
    Configuration Server



# Links
    [SOA vs MicroServices](https://aws.amazon.com/compare/the-difference-between-soa-microservices/)