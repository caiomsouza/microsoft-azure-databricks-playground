# Apache Spark Docker Image

https://hub.docker.com/r/sequenceiq/spark/

Pull Apache Spark 1.6.0
```
docker pull sequenceiq/spark:1.6.0
```

Run Docker Apache Spark 1.6.0 Image
```
docker run -it -p 8088:8088 -p 8042:8042 -h sandbox sequenceiq/spark:1.6.0 bash
```

# execute the the following command which should print the "Pi is roughly 3.1418" to the screen
```
spark-submit \
--class org.apache.spark.examples.SparkPi \
--master yarn-client \
--driver-memory 1g \
--executor-memory 1g \
--executor-cores 1 \
$SPARK_HOME/lib/spark-examples-1.6.0-hadoop2.6.0.jar
```

SPARK_HOME
```
bash-4.1# echo $SPARK_HOME
/usr/local/spark
bash-4.1# cd /usr/local/spark
bash-4.1# pwd
/usr/local/spark
bash-4.1# ls
CHANGES.txt  LICENSE  NOTICE  R  README.md  RELEASE  bin  conf  data  ec2  examples  lib  licenses  python  sbin  yarn-remote-client
bash-4.1#
```
