# Metrics Made Easy 

## Setup

### Grafana
#### Login
By default the username and password are the same for Grafana.
Username: admin
Password: admin

You will be prompted to change this upon first succesful login. You should probably do that.

#### Configure datasource
You will need to setup the datasource so that Grafana knows where it will be pulling the data from.

Navigate to Settings -> Data Sources -> Add Data Source

The following are the variables you will need to configure your datasource with

**HTTP**
| Variable      | Value                 |
|---------------|-----------------------|
| URL           | http://influxdb:8086  |

**InfluxDB Details**
| Variable      | Value                 |
|---------------|-----------------------|
| Database      | datasource            |
| User          | root                  |
| Password      | root                  |

| Tables        | Are           | Cool  |
| ------------- |:-------------:| -----:|
| col 3 is      | right-aligned | $1600 |
| col 2 is      | centered      |   $12 |
| zebra stripes | are neat      |    $1 |

### Chronograf

## Usage


## Resources
[Telegraf](https://hub.docker.com/_/telegraf)
[Grafana](https://hub.docker.com/r/grafana/grafana/)
[Chronograf](https://hub.docker.com/_/chronograf)
[influxDB](https://hub.docker.com/_/influxdb)
[jwilder proxy](https://github.com/jwilder/nginx-proxy)
