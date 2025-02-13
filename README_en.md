# Materials for the _Data processing using Apache Airflow in Yandex Cloud_ webinar

This repository contains materials for the [Data processing using Apache Airflow in Yandex Cloud](https://www.youtube.com/watch?v=jF3YemOVofQ) webinar.

This video covers the general setup architecture and data processing workflows.

Below, you will find two Airflow DAG files:
1. `DataProcProcessing.py`: Showcase of data processing on a temporary Data Proc cluster.
This requires creating the following Airflow variables: 
    - `DP_SA_AUTH_JSON_PATH`: JSON credential file for YC DataProc calls.
    - `DP_PUBLIC_SSH_KEY`: Public part of the SSH key required for creating DataProc cluster nodes.
    - `S3_KEY_ID`: Key for accessing the YC S3 buckets in use.
    - `S3_SECRET_KEY`: Secret part of the key.
These parameters are required to automatically create the connections to use. However, you can also create connections manually through the Airflow admin interface (with the relevant `conn_id` values). In this case, you do not need to create variables.  
In the DAG file, IDs, names, and URLs of linked resources are also stored as variables and should be replaced with your own values.
Note that this example uses an additional DataProc cluster as an external Metastore cluster, so make sure to create it in advance.
A PySpark job requires the `DataProcessing.py` script which must be placed in a dedicated S3 bucket.

2. `ETLOrchestration.py`: Showcase of ETL process orchestration in a Greenplum database.
Make sure to create the following Airflow variables in advance:
    - `DEMO_USER`:  PostgreSQL DB user for establishing a connection.
    - `DEMO_PWD`: Password for this user.
    - `DEMO_KEY`: Static access key for accessing S3 from ClickHouse.
    - `DEMO_SECRET`: Secret part of this key.
These parameters are required to automatically create the connections to use. However, you can also create connections manually through the Airflow admin interface (with the relevant `conn_id` values). In this case, you do not need to create `DEMO_USER` and `DEMO_PWD`.
Prior to running this scenario, make sure to create:
    - Greenplum cluster, including a stored procedure for ETL, as well as PXF tables for accessing S3 and Postgres DBs (the `etl_function.sql` and `pxf_tables.sql` files).
    - ClickHouse cluster used by the second DAG operator to build data marts.
