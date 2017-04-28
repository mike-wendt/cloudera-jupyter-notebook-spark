# cloudera-jupyter-notebook-spark
Settings for using Jupyter hub/notebook with CDH and Spark 2.1

## Install Jupyterhub

https://github.com/jupyterhub/jupyterhub

## Add kernels

Kernels are located in `/usr/local/share/jupyter/kernels`

Move `pyspark16` and `pyspark21` folders into the above path

## Install Spark

1. Download Spark 2.1 for Hadoop 2.6: 
2. Extract tarball to `/opt/spark`

## Upload Spark libs

1. Upload Spark libs to HDFS for workers to pick up

```
hadoop fs -mkdir /lib
hadoop fs -put /opt/spark/jars/*.jar /lib
```

2. Upload YARN Shuffle jar

```
hadoop fs -put /opt/spark/yarn /lib
```

## YARN conf

Follow instructions here: http://spark.apache.org/docs/latest/running-on-yarn.html#configuring-the-external-shuffle-service

Add to `yarn-site.xml` for `yarn.application.classpath` - `hdfs://hdfs-cluster:8020/lib/yarn/*`

## Update `spark-defaults.conf`

Make sure the HDFS path is correct and adjust to your setup
