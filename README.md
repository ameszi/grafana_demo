# grafana_demo

All persistent data is stored in a ```data``` folder generated on the first ```docker-compose up```.

## First time setup

### MySQL

After the first deployment, the monitoring user is set up by entering the MySQL container and adding a dedicated user (instead of using root).
```
docker exec -it <mysql_container_id> mysql -uroot -p
```

Then issue the following commands in the DB:
```
CREATE USER 'exporter'@'%' IDENTIFIED BY 'exporterpassword' WITH MAX_USER_CONNECTIONS 3;
GRANT PROCESS, REPLICATION CLIENT, SELECT ON *.* TO 'exporter'@'%';
```

### grafana

The data source is set via the config file ```grafana_provisioning/datasources/automatic.yml```.
In the demo, Grafana panel setup was done manually using the "mysql_global_status_threads_connected{}" metric and triggering an alert when the value goes above 1. This is of course always 1 because of mysqld-connector so manually connecting to the DB from the docker host using ```docker exec -it <container_id> mysql -uroot -p``` instantly triggered the alert.
