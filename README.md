# Metrics Made Easy 

This is a simple docker based metrics system. It's as simple as running a single command and you're ready to start metri-cing your projects. With this, you can easily host your own Grafana with it's own sub-domain meaning no more accessing dashboards and what-not by IP and port number.

This system makes use of several different docker images which work together to provide a fairly powerful utility tool. Grafana and Chronograf for graphing the metrics that are collected by Telegraf and statsD which are stored in a very powerful, NoSQL, InfluxDB.

## Setup

### Grafana
#### Login
By default the username and password are the same for Grafana.

| Variable      | Value                 |
|---------------|-----------------------|
| Username      | admin                 |
| Password      | admin                 |

You will be prompted to change this upon first succesful login. You should probably do that.

#### Configure datasource
You will need to setup the datasource so that Grafana knows where it will be pulling the data from.

*Navigate to Settings -> Data Sources -> Add Data Source*

The following are the variables you will need to configure your datasource with

**HTTP**

It is important to note that all of these variables are by default and can be reconfigured in the `docker-compose.yaml` file.

| Variable      | Value                 |
|---------------|-----------------------|
| URL           | http://influxdb:8086  |

**InfluxDB Details**

It is important to note that all of these variables are by default and can be reconfigured in the `docker-compose.yaml` file.

| Variable      | Value                 |
|---------------|-----------------------|
| Database      | datasource            |
| User          | root                  |
| Password      | root                  |

### Chronograf

## Usage


## Resources
[Telegraf](https://hub.docker.com/_/telegraf)
[Grafana](https://hub.docker.com/r/grafana/grafana/)
[Chronograf](https://hub.docker.com/_/chronograf)
[influxDB](https://hub.docker.com/_/influxdb)
[jwilder proxy](https://github.com/jwilder/nginx-proxy)
