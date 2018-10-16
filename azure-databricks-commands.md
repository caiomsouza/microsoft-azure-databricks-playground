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


Spark Code - Read a JSON File / Display / Write to JSON
```
from pyspark.sql import SQLContext
sqlContext = SQLContext(sc)

df = sqlContext.read.json("/example/data/people.json")

# Displays the content of the DataFrame to stdout
df.show()

df.write.json("/example/data/people_04/10/2018.json")
```

