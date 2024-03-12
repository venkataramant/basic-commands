# Steps

    1. Requirements Clarifications
        "Ask Questions" 
            Scope out Problem Statement
        "Clarify Ambiguities"
        Goal: Define the end goals of System    
              Functional Requirements
              Non-functional Requirements

    2. Define System Interface
        Establish contract from Application.
    3. BallPark Estimations
        Estimates Scale of System
            No of API calls (Read/Write calls per Second)
        Storage
            a) Based on Data Model and No of Writes estimate how much storage is required for next 5 years
            b) What types of Storage are required
                SQL/NoSQL
                Cloud storage [For Images/files]
        Network BandWidth
            How much of Data is flowing in and out of System through API calls
    4. Design Data Model
        a) Design Data Classes and relatinship to reflect actors and actions of System
        b) Based upon Storage requirements 
            finout any limitations and their remediations (Partitioning and Sharding)
        c) Data management policies
            Encryption,Retension and Governance.
        
    5. High Level Designs
        a) Entity Relation Diagrams (ER)
           Identify Entity and Their Relations [Data Model]
        b) Component Diagram 
            High level blackbox for major functionalities
                (Database, Application Server, LB, MQ..etc)
        
        
    6. Detailed/Low Level Design
        a) Pickup 2 or 3 components for deep drive
        b) Flow/Interaction Diagram to simulate different business cases/flow in a given functionality
        c) Provide different approaches for the flows and their pros and cons.

    7. Bottlenecks Identification and Remediation
        a) System level Issues
            Single point of failures - (One component failure should not bring down the entire system)
            Data Redunancy and Replicas
            Resilence and fault tolerance
        b) Monitoring and Operation (SRE perspective)
        c) Indivdiaul Component Level issues
            Data Partioning and Consistent Hashing
            Data Replications
            Cache/Memecahe [Handling of Stale data/Eviction Policies/Race Conditions/Data Integrity]

# Esitmate Calculations
    1 Byte = 8 Bit
    8 Byte  = 64 Bit

    2^64-1 =2 power 63 = Max Integer value [18.45 M]

    8 Byte Number 18,446.74 billion
    4 byte Number 4300 M


# System APIs parameters
    api_key
    maximum_results_to_return
    sort
    page_token
    