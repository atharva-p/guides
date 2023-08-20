# Importing large datasets using mysql

## create a new connection 

and use the configure server management to do the basic setup, then add the option to allow import using local files in the advanced tab

```
OPT_LOCAL_INFILE=1
```

test the connection and then switch to that connection 

## server side check for `--local-infile`

using the workbench, see the system variables and then search for `local_infile` and make sure it's set to ON

## create a new table

### cyclist dataset

use the create table interface or run sql commands directly. here are some that were used on the project datasets 

_**Worked with the least truncation warnings (1800) for the cyclist dataset**_. this was also done with [strict sql mode disabled](https://stackoverflow.com/questions/35037288/incorrect-decimal-integer-value-mysql). disable it by making `sql_mode = ` in the system variables of the sql server. 

```sql
CREATE TABLE `cyclist`.`test2` (
  `ride_id` VARCHAR(100) NOT NULL,
  `rideable_type` VARCHAR(100) NULL,
  `started_at` VARCHAR(100) NULL,
  `ended_at` VARCHAR(100) NULL,
  `start_station_name` VARCHAR(100) NULL,
  `start_station_id` VARCHAR(100) NULL,
  `end_station_name` VARCHAR(100) NULL,
  `end_station_id` VARCHAR(100) NULL,
  `start_lat` DECIMAL(65, 30) NULL DEFAULT 0,
  `start_lng` DECIMAL(65, 30) NULL DEFAULT 0,
  `end_lat` DECIMAL(65, 30) NULL DEFAULT 0,
  `end_lng` DECIMAL(65, 30) NULL DEFAULT 0,
  `member_casual` VARCHAR(100) NULL,
  PRIMARY KEY (`ride_id`));
```

some more that were used, they don't work just as well

```sql
CREATE TABLE `cyclist`.`test` (
  `ride_id` VARCHAR(100) NOT NULL,
  `rideable_type` VARCHAR(100) NULL,
  `started_at` VARCHAR(100) NULL,
  `ended_at` VARCHAR(100) NULL,
  `start_station_name` VARCHAR(100) NULL,
  `start_station_id` VARCHAR(100) NULL,
  `end_station_name` VARCHAR(100) NULL,
  `end_station_id` VARCHAR(100) NULL,
  `start_lat` DECIMAL NULL DEFAULT 0,
  `start_lng` DECIMAL NULL DEFAULT 0,
  `end_lat` DECIMAL NULL DEFAULT 0,
  `end_lng` DECIMAL NULL DEFAULT 0,
  `member_casual` VARCHAR(100) NULL,
  PRIMARY KEY (`ride_id`));

```

```sql
CREATE TABLE `202207-divvy-tripdata` (
  `ride_id` varchar(30) NOT NULL,
  `rideable_type` varchar(45) DEFAULT NULL,
  `started_at` varchar(45) DEFAULT NULL,
  `ended_at` varchar(45) DEFAULT NULL,
  `start_station_name` varchar(100) DEFAULT NULL,
  `start_station_id` varchar(45) DEFAULT NULL,
  `end_station_name` varchar(100) DEFAULT NULL,
  `end_station_id` varchar(45) DEFAULT NULL,
  `start_lat` decimal(65, 30) DEFAULT NULL,
  `start_lng` decimal(65, 30) DEFAULT NULL,
  `end_lat` decimal(65, 30) DEFAULT NULL,
  `end_lng` decimal(65, 30) DEFAULT NULL,
  `member_casual` varchar(45) DEFAULT NULL,
  PRIMARY KEY (`ride_id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci
```

### heartbeat dataset

```sql 
CREATE TABLE `cyclist`.`hearttest1` (
  `id` BIGINT(20) NOT NULL,
  `time` VARCHAR(200) NULL,
  `value` INT NULL);
```

check if all the columns are correct with their respective types

## starting the data import

```sql 
LOAD DATA LOW_PRIORITY LOCAL INFILE 'C:/Users/athar/Downloads/202207-divvy-tripdata.csv' 
INTO TABLE `cyclist`.`202207-divvy-tripdata` 
CHARACTER SET armscii8 
FIELDS TERMINATED BY ',' OPTIONALLY ENCLOSED BY '"' ESCAPED BY '"' LINES TERMINATED BY '\r\n' 
IGNORE 1 LINES;
```


