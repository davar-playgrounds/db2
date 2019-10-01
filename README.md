Local Development with DB2
--------------------------

## Environment File
File `.env` contains available variables used by DB2 container.

## Using the Container
`$ docker-compose up -d`  
`$ docker exec -it db2-server bash -c "su - db2inst1"`  

Available variables are:

- `DB2INSTANCE` (default: db2inst1) is to specify the Db2 Instance name  
- `DB2INST1_PASSWORD` (default: auto generated 12 character) is to specify the respective Db2 Instance Password  
- `DBNAME` creates an initial database with the name provided or leave empty if no database is needed  
- `BLU` can be set to true to enable BLU Acceleration for instance  
- `ENABLE_ORACLE_COMPATIBILITY` can be set to true to enable Oracle Compatibility on the instance  
- `SAMPLEDB` can be set to true to create a sample (pre-populated) database  
- `PERSISTENT_HOME` is true by default, only specify to false if you are running Docker for Windows.  
- `HADR_ENABLED` if set to true, Db2 HADR will be configured. The following three env variables depend on HADR_ENABLED to be true  
- `ETCD_ENDPOINT` is for specifying your own provided ETCD key-value store. Enter your endpoints with a comma as the delimiter and without a space. This env variable is needed if HADR_ENABLED is set to true  
- `ETCD_USERNAME` specify the username credential for ETCD. If empty, it will use your Db2 instance  
- `ETCD_PASSWORD` specify the password credential for ETCD. If empty, it will use your Db2 instance password  
- `TEXT_SEARCH` (default: false) Specify true to enable and configure text search  
- `ARCHIVE_LOGS` (default: true) Specify false to not configure log archiving (reduces start up time)  
- `AUTOCONFIG` (default: true) Specify false to not run auto configuration on the instance and database (reduces start up time)  

DB2 on Docker Hub: https://hub.docker.com/r/ibmcom/db2  
