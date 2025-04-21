# Keycloak with OpenTelemetry (OTEL/OTLP)

This repo is an example for Keycloak 17+ (Quarkus based distribution, not for 
Keycloak legacy 17+ or Keycloak 17-).

Single click provisioning 
[![Gitpod ready-to-test](https://img.shields.io/badge/Gitpod-ready--to--test-blue?logo=gitpod)](https://gitpod.io/#https://github.com/jangaraj/keycloak-with-opentelemetry/) 
- Keycloak login: `admin/admin`
- Cribl login: `admin/adminadmin`

## Stack

![Infrastructure](https://raw.githubusercontent.com/jangaraj/keycloak-with-opentelemetry/main/doc/diagram.png)

### Metrics

[OTEL Java agent with autoinstrumentation](https://github.com/open-telemetry/opentelemetry-java-instrumentation)
generates OTLP metrics and pushs them to 
[OTEL collector](https://github.com/open-telemetry/opentelemetry-collector-contrib). 
Keycloak exports metrics to `/metrics` endpoint and 
[OTEL collector](https://github.com/open-telemetry/opentelemetry-collector-contrib)
scrapes them.
[OTEL collector](https://github.com/open-telemetry/opentelemetry-collector-contrib)
exports all collected metrics to [Prometheus](https://github.com/prometheus/prometheus)

### Traces

[OTEL Java agent with autoinstrumentation](https://github.com/open-telemetry/opentelemetry-java-instrumentation)
generates traces and sends them to [OTEL collector](https://github.com/open-telemetry/opentelemetry-collector-contrib)
which exports them to [Jaeger](https://github.com/jaegertracing/jaeger)

### Logs

Keycloak generates JSON logs, which are processed by Logspout/Logstash and inserted to Elasticsearch.

### Visualization

All observability sources (metrics, traces, logs) are aggregated/visualized 
in the [Grafana](https://github.com/grafana/grafana).



{"timestamp":"2025-04-21T15:12:01.643Z","sequence":145796,"loggerClassName":"org.jboss.logging.DelegatingBasicLogger","loggerName":"org.hibernate.internal.util.EntityPrinter","level":"DEBUG","message":"org.keycloak.models.jpa.entities.UserEntity{lastName=user1, federatedIdentities=<uninitialized>, realmId=af7d1c42-ab1d-42be-a349-21416d2e4baa, credentials=<uninitialized>, createdTimestamp=1745248321516, serviceAccountClientLink=null, enabled=true, notBefore=0, emailConstraint=user1@gmail.com, emailVerified=true, firstName=user1, requiredActions=[], federationLink=null, attributes=[], id=de3467f6-19ba-4b3d-8df0-e344d89ddcaa, email=user1@gmail.com, username=user1}","threadName":"executor-thread-14","threadId":114,"mdc":{"trace_flags":"01","trace_id":"5d6dfa5c20d19a764f3e3249bec071c9","span_id":"4e56682b1586700f"},"ndc":"","hostName":"33ec215164c5","processName":"QuarkusEntryPoint","processId":1}


