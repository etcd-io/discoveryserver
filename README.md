# discovery.etcd.io

[![Docker Repository on Quay](https://quay.io/repository/etcd/discoveryserver/status "Docker Repository on Quay")](https://quay.io/repository/etcd/discoveryserver)

This code powers the public service at https://discovery.etcd.io. The API is
documented in the [etcd clustering documentation](https://github.com/coreos/etcd/blob/master/Documentation/dev-internal/discovery_protocol.md#public-discovery-service).

# Building with Docker

## Requirements

Docker, using one of the following configurations:
  * **macOS** You can either use Docker for Mac or docker-machine. See installation instructions [here](https://docs.docker.com/docker-for-mac/).
  * **Linux with local Docker**  Install Docker according to the [instructions](https://docs.docker.com/installation/#installation) for your OS.

To build the image with Docker run: 

`$ cd path/to/discoveryserver`

`$ docker build -t discoveryserver .`

To create and execute the discoveryserver container run: 

`docker run discoveryserver`

# Building on a local OS/shell environment

### Go

Discoveryserver is written in [Go](http://golang.org). If you don't have a Go
development environment, please [set one up](http://golang.org/doc/code.html).


| discoveryserver     | requires Go |
|---------------------|-------------|
|       0.1           | =>1.11      |

#### Go modules

Discovery server uses Go modules, so that we need a Go version greater than or equal to 1.11.

Build the binary:

`go build -v -o ./bin/discovery .`

#### Test

`./test.sh`

# Configuration

The service has three configuration options, and can be configured with either
runtime arguments or environment variables.

* `--addr` / `DISC_ADDR`: the address to run the service on, including port.
* `--host` / `DISC_HOST`: the host url to prepend to `/new` requests.
* `--etcd` / `DISC_ETCD`: the url of the etcd endpoint backing the instance.

# Production Configuration

See https://github.com/etcd-io/discovery.etcd.io for how the service is run on Kubernetes.

# History

This package implements a super minimal etcd v2 API built on the currently
incomplete [v2v3 package]. We need to do this because the public etcd discovery
service has been running on the inefficient v2 storage engine and causing
operational burden.

Further, to solve operational issues using the v3 API will enable us to use the
backup features of the etcd Operator.
