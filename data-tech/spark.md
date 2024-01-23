Dask
pandas


Hadoop is a framework for distributed processing of large data sets across clusters of computers, consists of a large collection of open source projects. It uses the MapReduce algorithm.

MapReduce is a processing technique and program model for distributed computing based upon Java. Hard to write map-reduce programs. It needs expensive disk write for distribution tasks.

Hadoop DFS (Distributed  File System)
	Files reside on multiple/different computers.

HDFS 				-- S3 or GCS 

Processing Tasks

Hive (Meta)
	Data warehouse software project.
	Built on top of Hadoop
	Hive SQL
	Gives an SQL-like interface to query data.
	Data extraction from databases and file system that integrate with Hadoop

	Earlier, queries had to be implemented in MapReduce Java API.

		'HSQL
			SELECT year, AVG(age)
			FROM views.oly_players
			group by year
		'

Spark (Berkley --University of California)
	Distributed data processing tasks between clusters.
	Processing is done in memory.
	Faster processing as it avoids disk writes.
	It relied on resilient distributed datasets.(RDDs)

RDD - Resilient Distributed Dataset.
	Data structure that maintains data across multiple nodes.
	Immutable (read-only), partitioned collection of elments.
	No named columns, list of tuples.
	Tracks data lineage information to recover lost data.
	2 Operations: 
		Transformations 
			filter()
			map()
			groupByKey()
			union()
		Actions
			count()
			first()
			collect()
			reduce()
PySpark
	Pytohn API for Spark
	DataFrame abstractions (like pandas)
	encapsulates low level details and provides high level functions
		'HSQL
			SELECT year, AVG(age)
			FROM views.oly_players
			group by year
		'
		'python
		 oly_players_df.groupBy('Year').mean('Age').show()
		'
Airflow (AirBNB)
	DAG: Directed Acyclic Graph
		 A collecton of tasks/functions need to be executed and have depedency with each other.

Luigi
	??

ETL 'Extract Transformation Load'

	Extract from Files
		Unstructured
			Plain text
		Flat files
			Row is record
			.csv,.tsv
		JSON
			JavaScript Object Notation
			Semi-Structured
			Atomic types 
				number,string,bool,null
			Composite
				array,object
	Extract from Databases
		OLTP (Online Transaction Processing)
			Application databases
			Row Oriented/Stored per record
			Many transactions per second
		OLAP (Online Analytical Processing)

Data Extraction from SQL
	

	Transformers:
	Text Classification for NLP using BERT

	https://github.com/LinkedInLearning/building-apps-with-ai-tools-chatgpt-semantic-kernel-langchain-4469616

	https://github.com/LinkedInLearning/introduction-to-ai-native-vector-databases-4470531








