# Create a new database and credentials for the microservice

Use the `mysql` command in the terminal to enter the MySQL interactive console.

```
mysql> CREATE DATABASE umet;
mysql> CREATE USER 'manning'@'localhost' IDENTIFIED WITH mysql_native_password BY 'WasmEdge';
mysql> GRANT SELECT, INSERT, UPDATE, DELETE, CREATE, INDEX, DROP, ALTER, CREATE TEMPORARY TABLES, LOCK TABLES ON umet.* TO 'manning'@'localhost';
```

Then, you start the `order_management` microservice like this:

```
cd order_management
wasmedge --env "SALES_TAX_RATE_SERVICE=http://127.0.0.1:8001/find_rate" --env "DATABASE_URL=mysql://manning:WasmEdge@127.0.0.1:3306/umet" target/wasm32-wasi/release/order_management.wasm
```
