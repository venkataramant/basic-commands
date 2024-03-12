
Structured Data
Unstructured Data
Transactional Data
Relational Data

Cloud Storage
Cloud SQL
Cloud Spanner
Cloud FireStore
Cloud BigTable


Cloud Storage -- Object Storage
	File Storage (binary form of actual data, metadata, uuid) URLs
	5TB per Object
	PetaBytes
	BLOB --Binary Larget Object Storage
	ACL 
		IAM
		ACLs (Access Control list)
			Scope + Permission
	LIfecycle Policies
		Standard Storage (Hot data...for Brief for time)
		Nearline Storage (Frequent 30 ..once per month) [Data backup/archival]
		Coldline Storage (90 days
		Archive Storage (once a year...DR, online backup..data archiving)
	AutoClass
		transition between storage based upon access patterns
	Upload methods:
		Online Transfer
			Gcloud Storage
			Cloud Console (Drag and drop)
		Storage Transfer Service
		Transfer Applicance [High Capacity Storage Server on lease)
		
Cloud SQL
	upto 64 TB
Cloud Spanner
	upto 64 TB
	Scales horizontally
	Strong consistent
	Speaks SQL
	SQL Relations , joins and secondary indexes
	Global Consistency
	High Number of IOs

Cloud Firestore
	Terabyes
	1 mb per entity
	NoSQL Cloud database, Flexible,Horizontally scalable.
	Documents/Collections

Cloud BigTable
	PetaBytes
	10 mb per cell and 100MB per row.
	Google's NoSQL big data database service
	Data Service Layer
		Managed VMs
		Hbase REST Server
		Java Server
	Stream Processing Frameworks
		Hadoop MapReduce
		DataFlow
		Spark
		

Block Storage

