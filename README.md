# EMQX MQTT broker and TDEngine on docker

This project simplifies the installation of TDEngine database and an EMQX MQTT broker

## Features

### Ingest MQTT Data into TDengine:
- EMQX supports integration with TDengine, allowing massive data transmission, storage, analysis, and distribution from numerous devices and data collectors.
- This integration provides real-time monitoring and early warning capabilities for business operations, offering valuable insights.
### How It Works:
- The integration combines EMQX’s real-time data capturing and transmission capabilities with TDengine’s data storage and analysis functionality.
- EMQX includes a built-in rule engine component that simplifies the process of ingesting data from EMQX to TDengine for storage and analysis.


## Installation

1. Clone this repository.
2. Run the docker compose file

## Usage

Store data from a specified MQTT topic to a TDEngine table:

###Create the database on TDEngine

```shell
# To start the TDengine docker image 
docker start tdengine_test

# Access the container
docker exec -it TDengine bash

# Locate the TDengine server in the container
taos
```
Once inside taos:
```sql

CREATE DATABASE mqtt;

use mqtt;
```

### Create Data Tables in TDengine

Before you create data bridges for TDengine, you need to create two data tables in TDengine database for message storage and status recording.

Use the following SQL statements to create data table t_mqtt_msg in TDengine database. The data table stores the client ID, topic, payload, and creation time of every message.
sql
```sql
   CREATE TABLE t_mqtt_msg (
       ts timestamp,
       msgid NCHAR(64),
       mqtt_topic NCHAR(255),
       qos TINYINT,
       payload BINARY(1024),
       arrived timestamp
     );
```
Use the following SQL statements to create data table emqx_client_events in TDengine database. This data table stores the client ID, event type, and creation time of every event.
sql

```sql
     CREATE TABLE emqx_client_events (
         ts timestamp,
         clientid VARCHAR(255),
         event VARCHAR(255)
       );
```



## Contributing

Contributions are welcome! If you'd like to contribute, follow these steps:
1. Fork the repository.
2. Create a new branch.
3. Make your changes.
4. Submit a pull request.

## License

This project is licensed under the MIT License - see the LICENSE file for details.
