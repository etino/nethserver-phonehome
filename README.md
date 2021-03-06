# Phone Home

Tracking all NethServer's installations around the world.

  - Use API to get and set installation
  - Visualize the installations in Google Maps with nice markers

Files:
* ```root``` directory: contains alla data to create the client rpm
* ```server``` directory: contains all scripts for server-side installation

## Server

### Installation

You need to set the correct placeholder to get access of DataBase and REST API.

##### Change placeholders
File ```config.php``` line ```2``` change ```__dbhost__, __dbuser__, __dbpass__, __dbname__```
```sh
  // credentials
  $GLOBALS['$dbhost'] = "__dbhost__";
  $GLOBALS['$dbuser'] = "__dbuser__";
  $GLOBALS['$dbpass'] = "__dbpass__";
  $GLOBALS['$dbname'] = "__dbname__";
```

File ```widget_map.html``` line ```53``` change ```__serverip__```
```sh
// ip server with api
var server_ip = '__serverip__';
```

##### Create table and db
Simply run: (MySQL Syntax)

```sh
CREATE TABLE IF NOT EXISTS phone_home_tb (
  uuid                  VARCHAR(40) PRIMARY KEY, 
  release_tag           VARCHAR(10) NOT NULL,
  ip                    VARCHAR(16) NOT NULL,
  country_code          VARCHAR(5),
  country_name          VARCHAR(40),
  country_location_lat  VARCHAR(40),
  country_location_lng  VARCHAR(40),
  reg_date              TIMESTAMP
)
```

## Client

### Installation

#### Configuration file

Create file in ```/etc/sysconfig/``` named ```phone-home``` and set the correct infos
```sh
SERVER_IP=__serverip__
PROXY_SERVER=__proxyserver__
PROXY_USER=__proxyuser__
PROXY_PASS=__proxypass__
PROXY_PORT=__proxyport__
```
the variables ```PROXY_SERVER, PROXY_USER, PROXY_PASS, PROXY_PORT``` are not mandatory.

#### Add new record for phone-home

Simply run: 
```sh 
config set phone-home configuration status enabled
```

#### Run phone-home 

Copy the phonehome script to /etc/cron.weekly directory.
