# Dibimbing Mini Project - Part I

## Description
This folder is meant for the first part of dibimbing mini project template (or helper). In this repo, you'll find everything you need to complete all 6 challenges.

## Setup
In order to use this template, first you must have docker installed in your local machine and internet connection.

After that you have to install `make` command. `make` is used to shorten and compact some commands in CLI. If you do not have `make` in your system, you can follow these articles ([mac](https://formulae.brew.sh/formula/make), [linux](https://linuxhint.com/install-use-make-ubuntu/), [windows](https://thrivemyway.com/how-to-install-and-use-make-in-windows/)).

Once you have installed it, go to the `mini_project_1` folder the run `make docker-build` to build all the images needed for the mini project. And for ARM processor, you can run `make docker-build-arm` 

### Postgres SQL
To spin up Postgres instance, you can run 
```sh
make postgres-create
```
it will take a while if you do not have Postgres SQL version 11 image in your local machine. Once you fetch it, the next command will run faster because it will use the existing image rather than pulling it from the Dokcer Hub.

### Spark Cluster
Related to Spark Cluster, you can run 
```sh
make spark
```
to spin up a cluster. This cluster will be consisted of 1 spark worker and 1 spark driver.

### Airflow
To spin up an Airflow container, first you have to make sure that your **Postgres container is up and running**. To spin up airflow, you can run
```sh
make airflow
```

### Kafka
To spin-up kafka, simply run
```sh
make kafka
```

## Challenges

### Challenge 1 - Spark RDD
**Goals**:Able to use Spark RDD to analyze CSV data locally \
**Container Needed**: Spark \
**Detail Challenges**:
- Given a CSV file (online-retail-dataset.csv), make a simple data analysis about the data.
- You can only use Spark RDD to do the analysis.
- Make it in python format file, and make sure it is submit-able to your spark cluster.
- You can read `spark-example.py` file in folder `spark-scripts` for the example spark script that is submit-able.

---
### Challenge 2 - Spark Dataframe
**Goals**:Able to use Spark Dataframe to analyze CSV data locally \
**Container Needed**: Spark \
**Detail Challenges**:
- Given a CSV file (online-retail-dataset.csv), make a simple data analysis about the data.
- Make sure the analysis is different from the previous challenge.
- You can only use Spark Dataframe (or SQL) to do the analysis.
- Make it in python format file, and make sure it is submit-able to your spark cluster.
- You can read `spark-example.py` file in folder `spark-scripts` for the example spark script that is submit-able.

---
### Challenge 3 - Spark Data Cleaning
**Goals**:Able to use Spark Dataframe to analyze Postgres SQL Database locally \
**Container Needed**: Spark, Postgres \
**Detail Challenges**:
- Given a CSV file (online-retail-dataset.csv), ingest the file into the a table in Postgres database.
- Make sure that you already have the database, schema, and table inplace before ingesting the CSV file.
- You can only use Spark Dataframe (or SQL) to do the ingestion.
- After the ingestion, make sure all the column has the right type based on the `online-retail-dataset.json` on folder `data`
- Once it mathces the `online-retail-dataset.json` schema, try to clean-up transactions that was happening before 2011 and happening outside of United Kingdom, and save it back to a different table in the same database.
- You can read `dibimbing-spark.ipynb` file in folder `notebooks` for the example spark script.

---
### Challenge 4 - Spark on Airflow (Local)
**Goals**:Able to submit a Spark job from Airflow locally \
**Container Needed**: Spark, Postgres, Airflow \
**Detail Challenges**:
- Just like the Challenge 2, but with Airflow.
- You can only use SparkSubmitOperator in the Airflow.
- Make sure the DAG scheduled was None.
- You can read `spark-dag-example.py` file in folder `dags` for the example Airflow DAG script.

---
### Challenge 5 - Spark Streaming
**Goals**:Able to submit a Spark Streaming job locally \
**Container Needed**: Spark, Postgres, Airflow, Kafka \
**Detail Challenges**:
- Run `make kafka-create-test-topic` to create a Kafka topic.
- Run `make spark-produce` to generate a fake data stream into the created kafka topic.
- To see the sample of the stream data, go to Kafka-UI at `localhost:8083`
- Based on the events data, create a running total for all the possible event key (column) using Spark Structured Streaming API.
- Make sure you only output it to `console` per 10 minutes trigger on `complete` mode.
- You can read `Dibimbing-spark-stream-1.ipynb` and `Dibimbing-spark-stream-2.ipynb` notebooks in folder `notebooks` for the example on how to process the streaming data.
