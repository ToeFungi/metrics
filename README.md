# Metrics Made Easy 

This is a simple docker based metrics system. It's as simple as running a single command and you're ready to start metric-ing your projects. With this, you can easily host your own Grafana with it's own sub-domain meaning no more accessing dashboards and what-not by IP and port number.

This system makes use of several different docker images which work together to provide a fairly powerful utility tool. Grafana and Chronograf for graphing the metrics that are collected by Telegraf and statsD which are stored in a very powerful, NoSQL database, InfluxDB.

## Pre-requisites

To get started using this simple system, all you will need to have is:

- [docker](https://docs.docker.com/)
- [docker-compose](https://docs.docker.com/)

When both of those are up and running, you are ready to move onto the next step.

## Setup

First of all, you'll need to clone the project. That should be simple enough...

```bash
$ git clone https://github.com/ToeFungi/metrics.git
$ cd metrics/
```

Next you'll need to start the docker containers. Very simply you'll need to run the following command:

```bash
$ docker-compose up -d
```

This will start the services contained within your `docker-compose.yaml` file. Upon first start of the containers, they will download the images they require to run.

### Grafana

This is how you are going to be configuring **Grafana** to pull data from influxDB. Very basic steps.

#### Login
By default the username and password are the same for Grafana. You will be prompted to change this upon first succesful login. You should probably do that.

| Variable      | Value                 |
|---------------|-----------------------|
| Username      | admin                 |
| Password      | admin                 |

#### Configure Data Source
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

// TODO - coming soon

## Usage

// TODO - coming soon

## Resources
[Telegraf](https://hub.docker.com/_/telegraf)
[Grafana](https://hub.docker.com/r/grafana/grafana/)
[Chronograf](https://hub.docker.com/_/chronograf)
[influxDB](https://hub.docker.com/_/influxdb)
[jwilder proxy](https://github.com/jwilder/nginx-proxy)
