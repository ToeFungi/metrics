# Metrics Made Easy 
This is a simple docker based metrics system. It's as simple as running a single command and you're ready to start metric-ing your projects. With this, you can easily host your own Grafana with it's own sub-domain meaning no more accessing dashboards and what-not by IP and port number.

This system makes use of several different docker images which work together to provide a fairly powerful utility tool. Grafana and Chronograf for graphing the metrics that are collected by Telegraf and statsD which are stored in a very powerful, NoSQL database, InfluxDB.

## Pre-requisites
To get started using this simple system, all you will need to have is:

- [docker](https://docs.docker.com/)
- [docker-compose](https://docs.docker.com/)

When both of those are up and running, you are ready to move onto the next step.

## Setup
### Cloning
First of all, you'll need to clone the project. That should be simple enough...

```bash
$ git clone https://github.com/ToeFungi/metrics.git
$ cd metrics/
```

Next you'll need to start the docker containers. Very simply you'll need to run the following command:

```bash
$ docker-compose up -d
```

This will start the services contained within your `docker-compose.yaml` file. Upon first start of the containers, they will download the images they require to run, don't worry too much about this.

### Grafana
This is how you are going to be configuring **Grafana** to pull data from InfluxDB. Very basic steps.

#### Login
By default the username and password are the same for Grafana. You will be prompted to change this upon first succesful login. You should probably do that.

| Variable      | Value                 |
|---------------|-----------------------|
| Username      | admin                 |
| Password      | admin                 |

#### Configure Data Source
You will need to setup the datasource so that Grafana knows where it will be pulling the data from.

*Navigate to Settings -> Data Sources -> Add Data Source*

The following are the variables you will need to configure your datasource with:

**HTTP**

It is important to note that all of these variables are default and can be re-configured in the `docker-compose.yaml` file.

| Variable      | Value                 |
|---------------|-----------------------|
| URL           | http://influxdb:8086  |

**InfluxDB Details**

It is important to note that all of these variables are default and can be re-configured in the `docker-compose.yaml` file.

| Variable      | Value                 |
|---------------|-----------------------|
| Database      | datasource            |
| User          | root                  |
| Password      | root                  |

You can now test your connection by clicking **Save & Test**. You should get a notification stating that your data source is working. You're now ready to start graphing using Grafana. When you start a new graph, just remember to set your data source to the data source configured in this section!

To find out more about how to graph using Grafana, you can check out their documentation [here](http://docs.grafana.org/features/panels/graph/).

### Chronograf
You will need to configure the connection for Chronograf. While this tool isn't strictly speaking necessary, it is helpful for debugging and/or simply checking what data has been stored in InfluxDB. To get started here you're going to want to navigate to:

*Configuration -> Add Connection*

It is important to note that all of these variables are default and can be re-configured in the `docker-compose.yaml` file.

| Variable      	| Value                 |
|-------------------|-----------------------|
| Connection URL    | http://influxdb:8086  |
| Username        	| root                  |
| Password      	| root                  |
| Database Name 	| datasource 			|

Next you will be prompted to selected what type of dashboard you would like to create, you're going to want to selected *InfluxDB*. After that you can skip the Kapacitor connection and you're done! Now your Chronograf is configured to read data from InfluxDB.

If you're not familiar with how Chronograf is supposed to work, then you can find out more from their documentation [here](https://docs.influxdata.com/chronograf/v1.7/guides/querying-data/).

## Usage
We're going to be sending packets over data over UDP with a statsD client. Telegraf, which uses a statsD plugin, will be listening for the packets being sent and then perform it's necessary procedures when a packet is received. You'll need to configure your statsD client with the following settings:

It is important to note that the `host` is the `service` name of the container running `telegraf`. Some docker network resolution magic.

| Variable      | Value                 |
|---------------|-----------------------|
| host      	| telegraf 	 	        |
| port          | 8125                  |

Let's take a look an extremely over simplified example shall we? 

By the way, should probably note that this example is in [TypeScript](https://www.typescriptlang.org/).
The statsD client I am using for this example can be found [here](https://www.npmjs.com/package/@types/statsd-client).
There is no obligation to be using TypeScript, I just am. You can find the normal Node statsD client [here](https://www.npmjs.com/package/statsd-client).

Let's say I have a `.env` file containing:

```env
STATSD_HOST='telegraf'
STATSD_PORT=8125
```

Then I can have a basic metrics class that looks as follows:

```typescript
class Metrics {
  private statsdClient: StatsdClient

  constructor () {
    this.statsdClient = new StatsdClient({
      host: process.env.STATSD_HOST,
      port: process.env.STATSD_PORT
    })
  }
}
```

This is very simple and straight forward but that client will allow you to metric your application quite well most of the time when it comes to hobby projects.

## Resources
[Telegraf](https://hub.docker.com/_/telegraf)

[Grafana](https://hub.docker.com/r/grafana/grafana/)

[Chronograf](https://hub.docker.com/_/chronograf)

[influxDB](https://hub.docker.com/_/influxdb)

[jwilder proxy](https://github.com/jwilder/nginx-proxy)
