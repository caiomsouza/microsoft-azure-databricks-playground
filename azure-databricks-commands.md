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

# Apark SQL API 

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


Spark Code - Read a JSON File / Display / Write to JSON
```
from pyspark.sql import SQLContext
sqlContext = SQLContext(sc)

df = sqlContext.read.json("/example/data/people.json")

# Displays the content of the DataFrame to stdout
df.show()

df.write.json("/example/data/people_04/10/2018.json")
```

