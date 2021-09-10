# grafana_demo

All persistent data is stored in a ```data``` folder generated on the first ```docker-compose up```.

## grafana config

The data source is set via ```grafana_provisioning/datasources/automatic.yml```.
In the demo, Grafana panel setup was done manually using the "mysql_global_status_threads_connected{}" metric and triggering an alert when the value goes above 1. This is of course always 1 because of mysqld-connector so connecting to the DB from the docker host using ```docker exec -it <container_id> mysql -uroot -p``` instantly triggered the alert.
