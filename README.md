# Micro [![License](https://img.shields.io/:license-apache-blue.svg)](https://opensource.org/licenses/Apache-2.0) [![GoDoc](https://godoc.org/github.com/micro/micro?status.svg)](https://godoc.org/github.com/micro/micro) [![Travis CI](https://travis-ci.org/micro/micro.svg?branch=master)](https://travis-ci.org/micro/micro) [![Roadmap](https://img.shields.io/badge/roadmap-in%20progress-lightgrey.svg)](https://github.com/micro/micro/wiki/Roadmap) [![Go Report Card](https://goreportcard.com/badge/micro/micro)](https://goreportcard.com/report/github.com/micro/micro)


Micro is a **microservice** toolkit. It's purpose is to simplify distributed systems development.

Check out [**go-micro**](https://github.com/micro/go-micro) if you want to start writing services in Go now. Examples of how to write services in other languages can be found in [examples/greeter](https://github.com/micro/micro/tree/master/examples/greeter).

Learn more about Micro in the introductory blog post [https://blog.micro.mu/2016/03/20/micro.html](https://blog.micro.mu/2016/03/20/micro.html) or watch the talk from the [Golang UK Conf 2016](https://www.youtube.com/watch?v=xspaDovwk34).

Follow us on Twitter at [@MicroHQ](https://twitter.com/microhq), join the [Slack](https://micro-services.slack.com) community [here](http://slack.micro.mu/) or 
check out the [Mailing List](https://groups.google.com/forum/#!forum/microhq).

# Overview
The goal of **Micro** is to provide a toolkit for microservice development and management. At the core, micro is simple and accessible enough that anyone can easily get started writing microservices. As you scale to hundreds of services, micro will provide the fundamental tools required to manage a microservice environment.

The toolkit is composed of the following components:

**Go Micro** - A pluggable RPC framework for writing microservices in Go. It provides libraries for 
service discovery, client side load balancing, encoding, synchronous and asynchronous communication.

**API** - An API Gateway that serves HTTP and routes requests to appropriate micro services. 
It acts as a single entry point and can either be used as a reverse proxy or translate HTTP requests to RPC.

**Web** - A web dashboard and reverse proxy for micro web applications. We believe that 
web apps should be built as microservices and therefore treated as a first class citizen in a microservice world. It behaves much the like the API 
reverse proxy but also includes support for web sockets.

**Sidecar** - A language agnostic RPC proxy which provides all the features of go-micro as a HTTP endpoints. While we love Go and 
believe it's a great language to build microservices, you may also want to use other languages, so the Sidecar provides a way to integrate 
your other apps into the Micro world. It can be used as a standalone way to build fault tolerant microservices.

**CLI** - A straight forward command line interface to interact with your micro services. 
It also allows you to leverage the Sidecar as a proxy where you may not want to directly connect to the service registry.

**Bot** A Hubot style bot that sits inside your microservices platform and can be interacted with via Slack, HipChat, XMPP, etc. 
It provides the features of the CLI via messaging. Additional commands can be added to automate common ops tasks.

## Getting Started

### Writing a service

Learn how to write and run a microservice using [**go-micro**](https://github.com/micro/go-micro). 

Read the [Getting Started](https://github.com/micro/micro/wiki/Getting-Started) guide or the blog post on 
[Writing microservices with Go-Micro](https://blog.micro.mu/2016/03/28/go-micro.html).

### Install Micro

```shell
$ go get github.com/micro/micro
```

Or via Docker

```shell
$ docker pull microhq/micro
```

### Quick start

We need service discovery, so let's spin up Consul (default discovery mechanism; checkout [go-plugins](https://github.com/micro/go-plugins) to switch it out).

```
$ go get github.com/hashicorp/consul
$ consul agent -dev -advertise=127.0.0.1
```

Alternatively we can use multicast DNS with the built in MDNS registry for a zero dependency configuration. Just pass `--registry=mdns` to the below commands e.g. `server --registry=mdns` or `micro --registry=mdns list services`.

Run the greeter example app
```shell
$ go get github.com/micro/micro/examples/greeter/server
$ server
2016/06/20 03:03:39 Listening on [::]:62525
2016/06/20 03:03:39 Broker Listening on [::]:62526
2016/06/20 03:03:39 Registering node: go.micro.srv.greeter-34c55534-368b-11e6-b732-68a86d0d36b6
```

List services
```shell
$ micro list services
consul
go.micro.srv.greeter
```

Get Service
```shell
$ micro get service go.micro.srv.greeter
service  go.micro.srv.greeter

version 1.0.0

Id	Address	Port	Metadata
go.micro.srv.greeter-34c55534-368b-11e6-b732-68a86d0d36b6	192.168.1.66	62525	server=rpc,registry=consul,transport=http,broker=http

Endpoint: Say.Hello
Metadata: stream=false

Request: {
	name string
}

Response: {
	msg string
}
```

Query service
```shell
$ micro query go.micro.srv.greeter Say.Hello '{"name": "John"}'
{
	"msg": "Hello John"
}
```

Read more on how to use the Micro [CLI](https://github.com/micro/micro/tree/master/cli)

## Sponsors

<a href="https://blog.micro.mu/2016/04/25/announcing-sixt-sponsorship.html"><img src="https://micro.mu/sixt_logo.png" width=150px height="auto" /></a>

## Community Contributions

Project		|	Description
-----		|	------
[Micro Dashboard](https://github.com/Margatroid/micro-dashboard)	|	Dashboard for microservices toolchain micro

## Contributing

1. [Join](http://slack.micro.mu/) the Slack to discuss
2. Look at existing coding style
3. Submit PR
4. ?
5. Profit

