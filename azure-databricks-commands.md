# Azure Databricks (Spark) Commands

Some commands:

Run Shell commands (HD Insight/Spark)
```
%sh
!pwd
```

Run Shell commands (Azure Databricks)
```
%sh
pwd
```

See files/folders commands (Azure Databricks)
```
%%sh
ls -lh
```

Show databases in Spark
```
spark.sql('show databases').show()
```

Show tables in Spark
```
spark.sql('show tables').show()
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

