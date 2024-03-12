# Data WareHouse Vs DataLake Vs LakeHouse

    SQL Databases (OLTP)                    NoSQL (Document-Store,K-V,WideColumn-Store,Graph-Store)
        DB2                                     MarkLogic
        Oracle                                              MongoDB
        MySQL                                                       Amazon DynoDB         neo4j,InfiniteGraph 
        PostgreSQL                                          HyperTable  Redis   Riak    CouchDB
        Sybase
        SAP S/4 HANA
        [Critical Data, Detailed DAta. Operational Data]      [Historical Data, Mutli sourced data]
        [Latest Data, Consistency and Availability]           [Business Insights and Reports]


    DataWare houses

        Teradata        Amazon-Redshift
        Vertica         Google BigQuery
        Netezza(IBM)     SnowFlake
        Hive            Azure SQL DWH

        DWH support Structured data
        No support for video ,audio or text
        No support for Data science, ML

# Difference
    Database :: InBuilt Storage and Compute (Server/Processing Engine)
    DataLake :: Storage and Compute are separated
      

# Data Lake -- Big Data Storage (DFS- Distributed File Storage)
   

    DataLake :: Storage and Compute are separated
                HDFS        Spark
                GCS         MapReduce
                S3      
    BI + Reports + Data Science + Machine Learning 
    Advantage:
        Any file format (structured,semi-structured and unstructured)
        Any size
        Cost Saving
        Ingest Speed
        Accessibility and Advanced algorigthms

    Disadvantage
        Data Appending/Ingestion is time consumed and error-prone process.
        GDPR/CCPA compliance
        Too many files (Big/Small)
        Low Data Quality
            No metadata
            No Constraints

    Separate data lake and data house process and storage.
# LakeHouse

    Data is stored as Big-Data

    Middle Layer contains 
        both DataLake and Datahouse Features
    
    Databrics
    Delta Lakehouse
    Iceberg (Opensource)
    Apache hudi 
    Azure Fabric


    Advantages
        ACID compliant
        Strong data storage [versioned parquet files]
        Supports Apache Spark
        Audit Logs(Json)
        Time Travel Support
