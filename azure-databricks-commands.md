# Azure Databricks (Spark) Commands

Some commands:

# Linux Commands in Spark 
Run Shell commands
```
%sh
! pwd
```

See files/folders commands (Azure Databricks)
```
%%sh
ls -lh
```

Download a file 
```
%sh
! wget http://files.grouplens.org/datasets/movielens/ml-latest.zip
```

Unzip a file
```
%sh
! unzip ml-latest.zip
```

Tail a file
```
%sh
! tail ml-latest/tags.csv
```

# Spark SQL API 

Show databases in Spark
```
spark.sql('show databases').show()
```

Show tables in Spark
```
spark.sql('show tables').show()
```

Create a DB in Spark
```
spark.sql('create database londonintel')
```

Use DB
```
spark.sql('use londonintel')
```

```
spark.sql('create table movies \
         (movieId int,title string,genres string) \
         row format delimited fields terminated by ","\
         stored as textfile')                                              # in textfile format

spark.sql("create table ratings\
           (userId int,movieId int,rating float,timestamp string)\
           stored as ORC" )  

spark.sql("create table genres_by_count\
           ( genres string,count int)\
           stored as AVRO" ) 
```

Describe a table
```
spark.sql("describe formatted ratings").show(truncate = False)
```

Select a table
```
spark.sql("select * from movies").show()
```

Drop a table
```
spark.sql("DROP TABLE IF EXISTS movies")
```

Spark Code - Read a JSON File / Display / Write to JSON
```
from pyspark.sql import SQLContext
sqlContext = SQLContext(sc)

df = sqlContext.read.json("/example/data/people.json")

# Displays the content of the DataFrame to stdout
df.show()

df.write.json("/example/data/people_04/10/2018.json")
```

### Connect Azure Data Lake with Azure Databricks 

Read first: <BR>
https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-create-service-principal-portal <BR>
https://hadoop.apache.org/docs/r2.8.0/hadoop-azure-datalake/index.html <BR>
         
Tips:
* Application ID = Client ID
* Credential = 
* dfs.adls.oauth2.refresh.url = Go to Azure Active Directory -> App registrations -> Endpoints -> OAUTH 2.0 TOKEN ENDPOINT


There are two options to read and write Azure Data Lake data from Azure Databricks:

* DBFS mount points
* Spark configs

Using DBFS mount points
```
val configs = Map(
  "dfs.adls.oauth2.access.token.provider.type" -> "ClientCredential",
  "dfs.adls.oauth2.client.id" -> "b0c9a068-e32e-4636-b50d-7f2d667a00bc",
  "dfs.adls.oauth2.credential" -> "rj+IAKT7TcZSdoVhLfi2R0QBJvJqeOtLd3++DuwNdUk=",
  "dfs.adls.oauth2.refresh.url" -> "https://login.microsoftonline.com/16f460a0-7ffc-453a-9e41-71cc13e29e52/oauth2/token")

dbutils.fs.mount(
  source = "adl://adlsdemocaio.azuredatalakestore.net/",
  mountPoint = "/mnt/adlsdemocaio2",
  extraConfigs = configs)
```

Using DBFS mount points
```
spark.conf.set("dfs.adls.oauth2.access.token.provider.type", "ClientCredential")
spark.conf.set("dfs.adls.oauth2.client.id", "b0c9a068-e32e-4636-b50d-7f2d667a00bc")
spark.conf.set("dfs.adls.oauth2.credential", "rj+IAKT7TcZSdoVhLfi2R0QBJvJqeOtLd3++DuwNdUk=")
spark.conf.set("dfs.adls.oauth2.refresh.url", "https://login.microsoftonline.com/16f460a0-7ffc-453a-9e41-71cc13e29e52/oauth2/token")
```

List files
```
%fs ls /mnt/adlsdemocaio2/
```


# Create a Spark Dataframe based on CSV

```
sparkDF = spark.read.format('csv').options(header='true', inferSchema='true').load('dbfs:/mnt/adlsdemocaio2/azuredatabricks/voa-average-rent-borough.csv')
```

Show Dataframe
```
sparkDF.show()
```

Create a table based on Azure Data Lake Store
```
spark.sql("CREATE TABLE rent USING CSV LOCATION 'dbfs:/mnt/adlsdemocaio2/azuredatabricks/voa-average-rent-borough.csv'")
```

Select using Spark SQL
```
spark.sql("select * from rent").show()
```






