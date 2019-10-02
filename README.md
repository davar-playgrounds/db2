Local Development with DB2
--------------------------

## Environment File
File `.env` contains available variables used by DB2 container.


## Using the Container
- start the container:  
`$ docker-compose up -d`    

- tail the container logs:  
`$ docker logs -f db2-server`  

- log into the container:  
`$ docker exec -it db2-server bash -c "su - db2inst1"`    


## Using the DB2

- check that things are alright:  
`[db2inst1@db2-server ~]$ db2 list db directory`  

- check that db is active on tcp/ip port 50000:  
`[db2inst1@db2-server ~]$ db2set -all`  (search for `DB2COMM=TCPIP`)  
`[db2inst1@db2-server ~]$ db2 get dbm cfg | grep -i "db2c_db2inst1" && cat /etc/services | grep -i "db2c_db2inst1"`  
Tcp/ip service (SVCENAME) `db2c_db2inst1` should point to port `50000`:  

	```bash
	[db2inst1@db2-server ~]$ db2 get dbm cfg | grep -i "db2c_db2inst1" && cat /etc/services | grep -i "db2c_db2inst1"
 TCP/IP Service name                          (SVCENAME) = db2c_db2inst1
db2c_db2inst1	50000/tcp
	```

- start a db2 session:  
`[db2inst1@db2-server ~]$ db2`  

- connect to the sample database:  
`db2 => connect to sample`  

- list and describe some tables:  
`db2 => list tables`  
`db2 => describe table employee`  
`db2 => describe table product`  

- get some sample data:  
`db2 => select * from employees`  

- disconnect from the sample database:  
`db2 => disconnect sample`  

- quit db2:  
`db2 => quit`  

- disconnect from container:  
CTRL+d or `exit`  


## Available Variables:

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
How to View the Definition of a Table in IBM DB2: https://chartio.com/resources/tutorials/how-to-view-the-definition-of-a-table-in-ibm-db2/  
Confirming TCP/IP Configuration for a DB2 Instance: http://www.dbatodba.com/db2/problem-resolution/connectivity-errors/confirming-tcp-ip-configuration-for-a-db2-instance/. 
