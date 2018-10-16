# Azure Databricks (Spark) Commands

Some commands:

Spark Code - Read a JSON File / Display / Write to JSON
```
from pyspark.sql import SQLContext
sqlContext = SQLContext(sc)

df = sqlContext.read.json("/example/data/people.json")

# Displays the content of the DataFrame to stdout
df.show()

df.write.json("/example/data/people_04/10/2018.json")
```

