

Hadoop
	Data Layer
		HDFS (Hadoop Distributed File System)
		(GFS--Google File System)
		Name Node
			Data Node
			Data Node
	Processing Layer
		(MapReduce/Spark)
		Job Tracker
			Task Tracker
			Task Tracker

	Architect
		Master
			NameNode
			Resource Manager
		Worker
			Data Node
			Node Manager
			Map
			Reduce 
	YARN (Yet Another Resource Negotiator)
		YARN is the resource manament and job scheduling technology.

Hadoop and JVMS
	Hadoop processes run in separate Java Applications(JVM Daemons)
	JVMs dont share share state
	Functional Programming Model

File Systems
	HDFS
		Distributed or Pseduo-distributed
	Regular File System
		Standalone
	Cloud File Systems
		Amazon S3 (Hadoop-S3A client)
		Azure Blob Storage
		Google GCS

	Data Shuffle
		Local Disk
		SSD

Files and JVMS

	Single Node
		Local File System
		Single JVM
	Pseduo-distributed
		Uses HDFS
		JVM Daemons run processes
	Fully distributed
		Uses HDFS - 3 replicated
		JVM Daemons run processes


Hadoop Jobs

	Types
		Hadoop
		Spark
		SparkR
		PySpark
		Hive
		SparkSQL
		Pig

Hadoop Interafaces
	Web Interfaces
		HDFS NameNode
		YARN ResourceManager
		MapReduce Job History
		Spark History Server
		YARN Application TimeLIne
		Tez
		Jupyter
		Juypter Lab


MapReduce
	A programming paradigm -- Compute plus storage
	Designed initially as distirubte job to splitting massive datasets.

	Compute API
	
		Map
			Shuffle (Sort, Copy and Merge)
		Reduce
			Save

	Job - Unit of MapReduce Work/Instance
	Input Data - HDFS or (Cloud Storage)
	Map Task - runs on each worker Node
		Executes the Map function on DATA on EACH Node
		Produces <k, value> pairs on each node.
	Reduce Task - runs on DATA.
		Executes the Reduce function on DATA on SOME Node
		Produces Aggregates sets of <K,Value> pairs on SOME Nodes.
		Outputs a combined List


	Input ==> Split (Based on Partition/Range) ==> Map[Parallel execution] ==>Shuffle (Based on Key) ==> Reduce (Parallel execution)[List] ==> Publish Results [Aggregate List]

	MapReduce Daemons and Services
		JVMs or services - isolated processes
		Job Tracker - one (Controller and Scheduler)
		Task Trackers - one per Cluster (Monitor Tasks)
	Job Configurations
		Provide input/output locations for job instances.
		Job Clients submits job for execution
	MR Job Status and Logs
		Monitoring Job run status
		Local websites
		Logs


	Java Programming Concepts
		Input/Output(data)
		Mapper
		Reducer
		Partitioner
		Reporter
		OutputCollector

Optimizations
	
	Before Running a Job
		File Sizes
		Compression
		Encryption
		Preprocessing
		Chaining Jobs
	DataTyes
		Writable Types
			Text(String) IntWritable(4)/DoubleWritable(4)/LongWritable(8)/FloatWritable(4)/BooleanWritable(1)/ByteWritable(1)

		WritableComparable for Keys

		Custom Types Supported

			Custom Comparator
			Custom Input split
			Custom Partitioner
		InputTypes
			TextInputFormat
			KeyValueTextInputFormat
			SequenceFileInputFormat<K,V>
			NLineInputFormat
		OutputTypes
			TextOutputFormat
			KeyValueTextOutputFormat
			SequenceFileOutputFormat<K,V>
			NullåOutputFormat
Understanding Reducers

	Shuffle/Sort
	Reduce
	Aggregrate

	LocalReducers/Intermeidate Reducers
		Do a pre-aggregation

MR 2.0/3.0
	1.0 Only Batch Processing (Not Interactive)

	2.0













