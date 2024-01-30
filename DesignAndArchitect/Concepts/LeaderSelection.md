# Problem
    1. Picks 1 service instance to cordiante

    2. If leader dies, select next one.
# Use-Case
    1. Conserve resources by allocating who has to do what
    2. Aggregate results of multiple workers.
    3. Specific Special procedure

#  Leader election via a lease
    by SQL
    work_id | work_status | Lease | expriation_time
    wrk123  | NOT_DONE    | #0    | None
    wrk123  | NOT_DONE    | #1    | <time_stamp>

    all instances try to update lease(increment lease by +1) if expiration_time < current_time or expiration_time is None

# Leader election via queue_message
    try_dequeumMsg()
    if got_message
        do_actual_work()
        DeleteMsg()
    else
        retry

# Consensu Algorithm

    RAFT
    Zab
    Paxos
    Flood Max
    Gossip Algorithm
    
# RAFT (Replicated and Fault Tolerant)
        CoreOS (etcd)
        go-raft
        raft (Harshicorp)
        nuRaft (by Ebay C++)
    
    Leader
    Follower
    Candidate

    term =0

    Election process
        Candidate send the envelop 
            contains 2 important info [total no of entries in candiate's log and term of latest entry]
        every election term  increases
    
    Appendentries (RPC for interconnect communication for heart beat.)
    Log Replication
        Leader send appedentries to its followers
            only after majority of follower written writes
    
    Issues:
        all Client has to talk to leader for writing operations
        Leader has to get majority consenses/writing from followers to complete a write.
        Scaling is a issue with this approach
    


# Flood Max
    Diameter of Network
        the maximum distance between 2 nodes in the network.

    Every node has a random UID, knows the diameter of the network.

    In each round
        Every node keeps track of max UID seen so far and it broadcasts the max to all the nodes connected to it.
    After 'daimeter' number of rounds,
        every node has same max UID.
    Every Node compares Max UID and self UID and knows the leader.

    Time complexity
        time : o(Diameter)
        messages: o(Diameter x |E|)
    
    Optimizations
        dont send Max UID to the same NOde who sent max UID to the current Node.
        Only BroadCast If there is new Max UID.

# Paxos
    Roles:
                Client
                Proposer (Later Leader)
        Acceptor    Acceptor    Acceptor

        Leaner      Leaner      Leaner

# Others
    Proof of work is the underlying mechanism  for consensus in popular decentralized systems.
