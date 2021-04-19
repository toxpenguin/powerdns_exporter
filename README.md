# PowerDNS Exporter

[![Travis](https://img.shields.io/travis/janeczku/powerdns_exporter.svg)](https://travis-ci.org/janeczku/powerdns_exporter)

[PowerDNS](https://www.powerdns.com/) exporter for [Prometheus](http://prometheus.io/)

Periodically scrapes metrics via the [PowerDNS HTTP-API](https://doc.powerdns.com/md/httpapi/README/) and exports them via HTTP/JSON for consumption by Prometheus.

## The following PowerDNS products are supported

* [Authoritative Server](https://www.powerdns.com/auth.html)
* [Recursor](https://www.powerdns.com/recursor.html)
* [Dnsdist](http://dnsdist.org/) (coming soon)

---

## Flags

Name | Description | Default
---- | ---- | ----
listen-address | Host:Port pair to run exporter on | `:9120`
metric-path | Path under which to expose metrics for Prometheus | `/metrics`
api-url | Base-URL of PowerDNS authoritative server/recursor API | `http://localhost:8001/`
api-key | PowerDNS API Key | `-`

The `api-url` flag value should be passed in this format:

* PowerDNS server/recursor 3.x: `http://<HOST>:<API-PORT>/`
* PowerDNS server/recursor 4.x: `http://<HOST>:<API-PORT>/api/v1/`

## Build powerdns_exporter

Typical way of installing in Go should work.

        go mod init
        go mod tidy
        make

Specify with golang version, os and arch

        GO_VERSION=1.16.2 GOOS=linux GOARCH=amd64 make

A Makefile is provided in case you find a need for it.

## Usage

[See here](https://doc.powerdns.com/md/httpapi/README/) for instructions on how to enable the HTTP API in PowerDNS.

Then run the exporter like this:

        go run powerdns_exporter api-url="http://<HOST>:<API-PORT>/" -api-key="<YOUR_API_KEY>"

Show help:

        go run powerdns_exporter --help

## Docker

To run the PowerDNS exporter as a Docker container, run:

        $ docker run -p 9120:9120 janeczku/powerdns-exporter -api-url="http://<HOST>:<API-PORT>/" -api-key="<YOUR_API_KEY>"
