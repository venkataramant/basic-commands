# CPU vs VCPU
    1 Core has capability of running 2 threads called vCPU.
    In cloud, Capacity is measured in vCPUs.
    Slot:: No of available threads on a Node.

# Cluster
    MPP - Massive Parallel Processor 
          Single Machine with Thousands of CPUs 
          (SIMD - Single Instruction Multiple Data)(MIMD- Multiple Instruction, Multiple Data)
          Ex: Snowflake [IBM Blue Gene](https://en.wikipedia.org/wiki/IBM_Blue_Gene)
          https://insightsoftware.com/blog/mpp-columnar-databases/
          https://afroinfotech.medium.com/the-rise-of-mpp-platforms-comparing-smp-to-mpp-architecture-e6305f332a1f
    Symmetric Multi Processor
        A tightly coupled multiprocessor system.
    
    HMR (Hadoop MapReduce)
    Spark 

    Master/Header Node (Single)
        Worker/Data Nodes (Multiple)

    Main difference between HMR and Spark : 
        HMR uses disk for intermeidate state (write/read)
        Spark uses memory (using Resilient Distrubted Datasets)
        RDD copies are immutable
            Because of Immutable, in case of any part of task is failed, it fetches relevant copy of RDD/Data and restart the task.

# HMR vs Spark
    Speed
        HMR depends on disk, cache intermediate data on disk (Disk IO makes it slower than Spark)
        Spark uses Memory, in-memory processing, run iterative algorithms in-memory, cache intermediate data in memory
    Flexibility:
        Spark is general purpose cluster computing framework. HMR is mainly for data processing jobs.
    Support:
        Spark provides out of box support for SQL,Streaming,ML,Graph
        HMR is mainly for batch mode and needs, external tools to integrate to extend other capabilities.
    Processing Type:
        Spark Stream/Batch, HMR is mailny Batch.
    Data Flow: 
        Spark uses DAG and HMR uses 2 step approach (Map and Reduce)
    Easy of Use:
        Writing MR job is hard and, written in Java and have API suport in other languages (Python and Ruby)
        Spark provides high leve APIs and written in Scala and support SDKS in mutiple languages (Java, Python and R)
    Resource Management
        HMR depends on Hadoop Eco system YARN or Mesos. Spark uses its own cluster-management.

# Spark Salient features  
    In-Memory Processing
    Resilient Distributed Datasets (RDDs)
        Used to distribute data across a cluster, enable parallel computing.
    Built-in Libraries
        SQL,Streaming,ML and Graph
    DAG
        For Data flow,enables flexible execution [Complex data pipelines]
    Support for Multiple SDKs
    Interactive Shell
    Cluster Manager
        in-built manager called Spark Standalone, can work with YARN,Mesos also.
    Built-in-DS-Connectors:
        Have many built-in data source connectors [HDFS,Cassandra,HBase,S3]
#  SparkCore Architecture
    Master Node and Multiple Data/Worker Nodes

                                Driver JVM (Master Node SparkCore)
                    /                       |                   \
 Data Nodes (JVMs)[ Executor (Task Task)]   Executor (Task Task)    Executor (Task Task)    ]

    LocalMode:
        Driver and Executors are working on a single Node
    MultiNode Cluster
        One Driver and Multiple Executors are running on separate individual nodes.

# Components

                                        SparkSession
               /                /             |            \           \ 
        SparkContext     Streaming Context   SQL Context     GraphX        MLLib  HiveContext
        (SparkCore and RDD)

        2.0 Just SparkSession instead of Different Context
            Variables
                spark --- SparkSession
                sc    --- SparkContext
                sqlContext
# RDD - Resilient Distributed Datasets
    Immutable
```python
    import spark
    rdd1=spark.parallelize([1,2,3,4,5])
    sc.parallelize([0, 2, 3, 4, 6], 5).glom().collect()
    rdd2=spark.sparkContext.parallelize(range(20),noOfParalleProcessors)
    rdd2.collect()
    rdd2.glom().collect() # glom provides data per partition
```

# Actions
    Transformations (DDL and DML)
        Process on an RDD and generate new RDD (Immutuable)
        Lazy evaluated (DAGs are defined and only after Action is triggered, DAG is executed)
    Actions (DRL - Data Retrieveal language)
        Display
        Save
    Exectuciton
        rdd2.collect() >> Trigger Spark Job
                                Job 0 (Stages (x/y)) [Contains 1 or y stages]
                                    Stage 0 (t1/t2 Tasks) [Contains 1 or t2 tasks]
    
        Stages are determined by Operations
            Narrow transformations
            Wide    transformations
        Tasks are decided by Partitions, one Task per 1 vCPU
        One Executor per 1 vCPU with 2 slots
        One Task is per 1 slot.
        Ex:
        glom()
        display()
        count() collect()
        min() max() mean(), stdev(), stats()
        top(n) take(4) first()

# Narrow and Wide Transformation
    Shuffle Read/Write

    Narrow:
        rdd.coalesec(c)
        Nearby Partitions are merged
    Wide:
        rdd.repartition(r)
        Recreate New Partitions
            shuffle write temporary writes in Memory
                    Create new Partions in Memory
            Shuffle Read





