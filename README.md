# Object store proof of concept demonstations


## CSV to geoparquet

The notebook `glodap_to_geoparquet.ipynb` demonstrates converting a CSV download of the GLODAPv2.2023 Merged Master file data to geoparquet 

To recreate the environment on a system  with docker installed  e.g. linux or WSL(windows subystem for linux) with docker community edition
```console
cd glodap_to_geoparquet
docker compose build
docker compose up
``` 

## Apache Iceberg open Data Lakehouse format proof of concept

This is based on the [Apache Iceberg Spark Quickstart](https://iceberg.apache.org/spark-quickstart/)

The Quick start `docker-compose.yml` file can be used to spinup 4 containers on a Docker Instance.
This consists of:
- A Minio object store container
- A minio helper container that creates the Data Lakehouse S3 bucket
- A pyspark enabled Jupyter lab environment 
- A container running an Apache Iceberg REST catalog


We have also amended the docker compose to add a Trino container to show how a Trino Query engine can be connected to the Apache Iceberg Lakehouse, created by the quick start. 

```console
cd iceberg_trino_demo
docker compose pull
docker compose up
```

Do look at the examples provided by the [Apache Iceberg Spark Quickstart](https://iceberg.apache.org/spark-quickstart/)

When the containers are up and running, in a browser open the url: http://localhost:8888 to see the Jupyter lab environment

In particular "Iceberg - Getting Started.ipynb" to demonstrate the features of Apache Iceberg
and "PyIceberg - Getting Started.ipynb" which also demonstrates querying usign DuckDB in a notebook.

You can also upload notebooks to the Jupyter lab environment

Upload the notebook "Glodap_iceberg.ipynb" this demonstrates creating an Iceberg table from a Data Frame in which the GLODAP parquet file was loaded.

This Data Frame could also have been populated from the original GLODAP 2023 CSV datafile

Pyspark and spark sql is used to create the GlODAP table.

You can also browse to the local Minio container object store http://localhost:9000 and login using the user and password in the compose file and see the "warehouse" bucket with any Iceberg table files you create. 


We intend to further enhance the demo by providing and an example of publishing the GLODAP dataset via ERDDAP using  the Trino JDBC 
connector to show how ERDDAP and other systems can use Legacy data access protocols to publish tabular data from a Data lakehouse on an Object Store 


