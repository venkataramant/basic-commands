# DataFrames
	Data sets organized into columns
	Columns have names
	Rows have a schema

	df.select("c_name").show()
	df.groupby("c_name").count().show()

# Spark SQL
	SQL queries executed on DataFrames as registered as tables

	spark.sql("select c_n1,c_n2 from table_name")
	spark.sql("select count(*) from table_name group by c_name")

	pyspark [Opens jypter notebook]

	```python
		from pyspark.sql import SparkSession
		ss=SparkSession.builder.getOrCreate()
		data_path="/mydata"
		csv_path=data_path+ "/my.csv"
		df1=ss.read.format("csv").option("header",True).load(csv_path)
		df1.head()
		df1.show()

		df2=ss.read.format("csv").option("header",False).option("inferSchema",True).load(no_header_csv_path)
		df2.printSchema()
		df2.columns # its variable
		df2.withColumnRenamed("_old_cname","_new_cname")
	```
# Advance SQL
	```python
		df2.sample(withReplacement=False,fraction=0.10) #   False alawys unique
		df2.sort("c_name")
		df2.filter(df2["c_name"]=="value").show()
		df2.groupBy("c_name").count() # 
		df2.groupBy("c_name").agg({"c_name2":"mean"}).show()
		# mean, max, min
		df.write.csv()
		df.write.json()

		df.createOrReplaceTempView("new_table_name')
		df_sql_result=spark.sql('select * from new_table_name')
		df_sql.result.show()

		from pyspark.sql import Row,SparkSession
		from pyspark.sql.functions import lit
		from pyspark.sql.types from StringType

		sc # a globla variable spark context
		# creating dynamic temp table with data
		sc.parallelize([Row(c_name1=v1,c_name2=v2),Row(c_name1=v1,c_name=v2)]).toDF()

		df.drop_duplicates()
		df.drop_duplicates(["c1","c2"])
		# Add a new Column
		df.withColumn('new_c_name',lit(None).cast(StringType))
		# fillnulls
		df.fillna('A')
		df.na.drop()
		df.union(df2)
		df.describe()
		# statistic functions
		df.stat.corr('col1','col2') # 0 no Correlation
		# functions max/min/stddev/floor/ceil
		df.stat.freqItems((col1,col2))
		# OVER (PARTITION BY)

		# SLIDING WINDOW
		`SELECT ts,c1,c2, avg(c2) OVER (PARTITION BY c_name ORDER BY ts BETWEEN 1 PRECEDING AND 1 FOLLOWING) avg_c2 FROM t_name`

		# VECTOR
		from pyspark.ml.linalg import Vectors
		from pyspark.ml.feature import VectorAssembler
		from pyspark.ml.clustering import KMeans
		# input Columns, transformers
		va=VectorAssembler(inputCols=["c1","c2","c3"],outputCols=features)
		va.transform(df1)

		kmns=KMeans.setK(3)
		kmns.setSeed(1)

		kmodel=kmns.fit(v_df) # take features and fit into kmeans model
		kmodel.clusterCenters()

		from pyspark.ml.regression import LinearRegression
		lr=LinearRegression(featuresCol="f_col",labelCol="predict_col")
		lrModel=lr.fit(df)
		lrModel.intercept
		lrModel.coefficients
		lrModel.summary.rootMeanSquaredError
		


	```
	