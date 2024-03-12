# Partioning and Clustering

Table
    product_id product_type description price
    1          ChocolateBar    myDesc  1
    2          Cycle           myDesc  100
    3          Computer        myDesc  1500
    14         ChocolateBar    myDesc  1

Partitioning::
    Tables are split into smaller "segments" based on the value in a column.Collat
    Improve query performance
    Reduce data processing costs.
    Based upon 
        TimeUnit (TimeStamp,Date,DateTime)
        Integer
        Ingestion time
Clustering::
    Cluster Order determines the sort order of the data.
    Partiting based upon a text column is not allowed but clustering is allowed.
    Can be applied on multiple columns
    Costs canot be estimated like partionining

# Sources
    Empty Table
    GCS
    Upload
    Google Drive
    Gogole BigTable
    Amzaon S3
    Azure Blob Storage

# File Formats
    CSV JSONL
    Arvo 
    Parquet
    ORC 
    Iceberg

# Table Types
    Native Table
    External Table
# Collation
    Collatin determins how strngs are sorted and compared in collation-supported operations.
```sql
    create table table_a
    (
        col_a STRING COLLATE 'und:ci',
        col_b STRING COLLATE '',
        col_c STRING COLLATE ,
        col_d STRING COLLATE 'und:ci',
    );
    SELECT STARTS_WITH(col_c_expression,COLLATE(col_b_expression, 'und:ci'))
    FROM table_a;
```
    Specification:-> language_tag:collation_attribute [und:ci]
                     und -> a special language tag defined in IANA language subtag registry.
                     ci ->  Case Insensitive
# SQL Syntax
    
```sql
    CREATE TABLE 'DATASE1.NEW_TABLE2'
    PARTITION BY Date -- type by date, time, month, year
-- PARTION BY RANGE_BUCKET(integer_column, GENERATE_ARRAY(start:1,end:10,interval:5)) [1 to 5,6 to 9]
-- PARTION BY _PARTITIONDATE
    OPTIONS( 
        require_partion_filter=true
        partition_expiration_days=30
        )
    AS
    SELECT c1,c2,c4,c5,DATE,Time
    FROM 'DATASET1.TABLE2'
```

# Composite Data
    Column Types
            Records   - to Store a structure of data [Struct or Object]
            Repeated  - to make array
            UNNEST    - to flatten hierarchical data in queries.
            ARRAY_AGG   - aggregate values into arrays.

    Define:
        struct key word
    Functions::
         
```sql 
    CREATE TABLE IF NOT EXIST mydataset.myaddress (
        id STRING,
        f_name STRING,
        l_name STRING,
        dob DATE,
        address RECORD
        street  String
        city    String
        county  String
    phonenumbers String REPEATED

    INSERT INTO dataset1.table1 (c1,c2,c3,r3,rept4)
    values ( 1,'fname','lastname', 
             STRUCT('v1','v2','v3'),
             ['pnumber1','pnumber2']
            );
    SELECT c_1,c2,
        pnumbers[OFFSET(0)] AS primaryP,
        (CASE WHEN ARRY_LENTH(payments) > 0
              THEN payments[OFFSET(0)].p_cname,
              ELSE NULL
         END) as p_type,
         ph_number
    from dataset1.table2,
        UNNEST(pnumbers) as ph_number;

- UNNEST is used from FROM, to unpack a composite value.
```


# ARRAY_AGG
    - aggregates values into an array
```sql

    SELECT add.city,COUNT(*) AS count
    FROM 'dataset1.table1'
    GROUP BY add.city

    SELECT add.city,
           ARRAY_AGG(c1) as cname1,
           ARRAY_AGG(c2) as cname2
    FROM 'dataset1.table1'
    GROUP BY add.city



```
# WINDOW funcs

```sql
    SELECT cname1,c2,date3
        RANK() OVER (PARTITION BY brand ORDER BY price ) AS rnk
    FROM 'dataset1.table1'
    ORDER BY maker, rnk
```


# Operations
    - Load data
        BQ Data Transfer Service 
            Cloud Storage - GCS/S3
            Google Services - Google Play, Google Ads
            External WareHouses  - Teradata, Amazon Redshift

    - Monitor and optimize query performance and execution costs
        - Query execution times
        - Slot utilization
        - Number of jobs created over time period
    - Backup data/Snapshot
    - ACL setup

# Permissions
    Project Level
        Viewer
        Editor
        Owner
        Browser
    DataSet Level
        BQ Data Viewer
        BQ Job User
    Table Level
        BQ Data Editor

# Derived Data/Table (From Query)
    Restrict columns and allow only subset of data

    Query result --> Destination Table
    View also Destination Table
    Where email= SESSION_USER()
# Authiorzed Views/Routines/Datasets


# Snapshots

# ServiceAccount


```python
# pip install google-cloud-bigquery
from google.cloud import bigquery
from google.oauth2 import service_account
credentials= service_account.Credentials.from_service_account_file("path2")
client=bigquery.Client.(credentials=credentials)

query="SELECT * FROM dataset1.table1 where c1=cvalue"
q_job=client.query(query)
rows=q_jobs.result()
for row in rows:
    print(row)

```