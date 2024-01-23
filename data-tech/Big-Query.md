# What

	A Serverless, highly scalable and cost-effective multi-cloud data warehouse.

# Data Warehouse
	A System for reporting and data analysis which enables storing of large volumes of data from 
	disparate sources and quering them ot extract insights and drive business decisions

# 
	variety of data sources
	Legacy SQL
	High Performance
	Tost cost of ownership (LOW)


# others
	Amazon Redshift
	Snowflake
	Azure SQL datawarehouse

# Data Analysis and Business Intelligence (BI)

# Services (ISPaEv)

	Ingest
	Store
	Process and analyse
	Explore and Visualize

	Ingest
		App Engine
		Compute Engine
		GKE
		Cloud Functions
		Cloud Run
		Pub/Sub
		Logging
		Storage Transfer Service
		BQ Data Transfer Service
		Transfer Appliance
	Storage
		Cloud Storage
		Cloud SQL
		Datastore
		Cloud BigTable
		BigQuery
		CloudStorage for Firebase
		Cloud Firestore
		Cloud Spanner
	Process and Analyze
		DataFlow
		DataStreams (For CDC)
		DataProc
		Cloud Composer
		BigQuery
		AI Platform
		Cloud Vision API
		Translate API
		NL API
		Video Intelligence  API
		DataPrep
	Explore and Visualize
		Looker
		Datalab
		Data Studio
		BQ BI Engine
		Sheets
		Data Catalog

# Whats in BQ

	BigQuery - Store & Query
	BigQuery Data Transfer 
	BigQuery BI Engine - In-Memory analysis for sub-second query executions
	BigQuery Omni - Analyzing data across cloud platforms.
	Bigquery ML - Build and use ML models uisng SQL queries.

# Architecture of BQ 
	(BORG- Google Cluster Manager)

	4 Layers (Decoupled of Storage and Compute)
	    4. BORG Cluster management system for compute (Query Orchestration)
		3. Dremel	--		Query engine [Break up queries into pieces and assembles results of each run]
			Root Server
			Mixers
			Leaf Nodes
		2. Jupiter		- 	Networking infrastructure (Connecting Colossus and Dremel)
		1. Colossus	-	Storage Layer (Distributed File System)


# Data Arrangement
	
	Tables
		Columnar Model
			Rows and Columsn
			Each Column is stored in a separate file block [ Queries process only requested columns , good for OLAP use-cases]
		Mutations are also supported
		Split into segments called Partitions
			Integer,TS,DATE or datetime columns
			Ingestion time


	Views 
		Views (Abstracts query complexitiy. dont share data, enable restrictions of access to underlying tables)
		Materialized Views (results are Cached,refresh as per config, Pre-Aggregated data, query is fast, pre-filtered data, pre-joined data)
		Authorized Views
	Dataset
		Tables and Views
	Project
		Datasets


# Insights

	<<Streaming Ingest>>/<<Free Bulk Loading>> [Replicated,Distributed Storage]{Distributed Memory Shuffle tier connected by PetaBit Network} ][HA Cluster Compute by Dremel]

	SQL:2011 Compliant
	RESt APIs
	WEB,UI,CLI
	7 SDKS

	Batch Loading
		- Free when using shared slots
		- Dedicated slots can be purchased
	Streaming inserts
		- Charged for succesful inserts

	Sources:	
		CSV/JSON/AVRO/PARQUET  (Google Drive)
		Cloud Storage
		Data Fusion (Data Fusion Plug-ins)
		DataFlow (Beam Connectors)
		Parnter Integrations (Informatica Confluent/Kafka)
		BQ DTS (BQ DTS connectors/Partner DTS connectors[fivetran])

# Cost Categories

	Free Operations
		Batch Loading with a shared slot pool
		Deleting datasets/tables/views/functions/partitions
		Copying and exporting data 
		Metadata Operations
		first 10GB per month (storage)
		First 1TB per month(Query)

	Storage Pricing
		Active Storage (Modified in last 90 days)
			0.02 per GB
		Long-term storage (not modified in last 90 days)
			1/2 of Active Storage

	Analysis Pricing
		on-demand Analysis
			NoOfByes processed by queries
			2k slots shared by all queries in a project
			$5 per TB scanned by queries
			1TB is free
		Flast-rate Analysis
			Dedicated slots for a fixed monthly price
			Queries use available capacity
			Slots are for entire - Organization
			Costs are fixed/predictable


# creating table

	create table new_table
	as
	select name,company,cn,genre,dir,gross,budget, (gross-budget) as profit
	from old_table where gross>10000;

# BQ Caches

# BQ External Tables
	
	Google SpreadSheet
# Data Studio

# BQ Geographic 
	Select ST_GeogPoint(longitude,latitude) as geog,a,b,c from ds.tn


# BQ Shell
	
	bq ls 				[all datasets]
	bq ls <data_set>	[all tables]
	bq ls <data_set>:<table_name>
	bq show <data_set>
	bq show <data_set>:<table_name> --format=prettyjson
	bq query --dry-run ' select a,b,c from <data_set>.<table_name> where condition' 
	bq query --use_legacy_sql=false \
			 --parameter=aValue::abc \
			 --parameter=bValue:INT64:35 \
			 'select a,b,c from ds.tn where a=@aValue and b=@bValue'
	bq query --use_legacy_sql=false \
			 --parameter=aValue::abc \
			 --parameter=bValue:INT64:35 \
			 --flagfile=file_name.sql 

# BQ Views
	select t1.a, t2.c as new_c,t2.d,t2.b
	from ds1.tn1 as t1
	join ds2.tn2 as t2
		on t1.cn1=t2.cn2;

	create materialized_view ds_name.mv_view as
		select t1.a, t2.c as new_c,t2.d,t2.b
	from ds1.tn1 as t1
	join ds2.tn2 as t2
		on t1.cn1=t2.cn2;


	authorized_view
		select data from different dataset
	










