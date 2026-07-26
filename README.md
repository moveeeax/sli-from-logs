# sli-from-logs

> Get a real SLO out of access logs today, plus the recording rules to keep it.

**Status:** 🚧 In development

## Overview

Derive availability and latency SLIs directly from access logs when there is no instrumentation yet, emitting Prometheus recording rules to keep them going.

## Features

- Parses common access log formats — nginx combined, Apache, JSON lines, Envoy — with a user-supplied field mapping for the rest
- Computes availability from status class and latency percentiles from request duration, per route and per method
- Normalizes high-cardinality paths into route templates so `/orders/8213` does not become its own SLI
- Reports the error budget already burned over the analysed window, with the worst offending routes
- Emits ready-to-load Prometheus recording rules and a burn-rate alerting rule set for the chosen objective
- Lets you exclude health checks, crawlers and client-cancelled requests before they distort the number

## Stack

Go + cobra, the prometheus/prometheus rule model and PromQL parser for emitting and validating rules, prometheus/client_golang for the optional exporter mode.

## Usage

```bash
sli-from-logs --input /var/log/nginx/access.log --format combined --objective 99.9 --latency-target 300ms --emit-rules slo-rules.yml
```

## License

MIT
